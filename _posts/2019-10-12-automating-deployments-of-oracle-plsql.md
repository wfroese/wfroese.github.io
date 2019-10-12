---
draft: true
layout: post
title: "Automating Deployments of Oracle PL/SQL"
excerpt_separator: <!--end_excerpt-->
tags: code oracle best-practices
cover_image: /assets/images/oracle.jpg
cover_alt_text: oracle database logo
description: How we handle automating deployments involving Oracle PL/SQL procedures, packages, etc.
---

Some time ago I found myself taking over an existing set of systems built on top of a lot of Oracle PL/SQL, with no automated deployments in sight. I didn't quite have enough sense to run in the opposite direction, so instead I built an automated deployment system.

<!--end_excerpt-->

Our requirements were as follows:
1. We need to be able to handle database changes like adding/removing columns, creating new tables, etc.
2. We need to be able to handle updating the many stored procedures and packages.
3. We have a small team (&gt; 3 and &lt; 10) of developers who all need to be able to make database modifications for whatever feature/bug they happen to be working on.
4. We use a [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) with a QA environment, so we need to be able to easily merge database changes from feature branches together into a QA environment, or separately into master for production deployment.
5. We need to be able to automate the deployment of these changes to QA and production environments.
6. We need to be able to implement a rollback where we undo all code changes as well as database changes

## Standard Migrations
For starters, we implemented [Fluent Migrator](https://fluentmigrator.github.io/). I've used Fluent Migrator very successfully on previous projects, and it's always a pleasure to use. With Fluent Migrator a migration is defined as follows:

{% highlight csharp %}

[Migration(20191011121800)]
public class AddLogTable : Migration
{
    public override void Up()
    {
        Create.Table("Log")
            .WithColumn("Id").AsInt64().PrimaryKey().Identity()
            .WithColumn("Text").AsString();
    }

    public override void Down()
    {
        Delete.Table("Log");
    }
}

{% endhighlight %}

We created a .NET console application where we add a new class for each of these types of migrations. The console application accepts two parameters: a command (migrate/rollback), and a connection string.

The code of the console application is almost verbatim from [Fluent Migrator's Quick Start Guide](https://fluentmigrator.github.io/articles/quickstart.html?tabs=runner-in-process) so I won't repeat it here.

## PL/SQL
For the next step, we need a way to handle Pl/SQL - stored procedures and packages of stored procedures. This we solved by deciding to treat PL/SQL code just like any other code.

In our migrations console app we created in the previous step, we added a couple folders for procedures and packages, and then added a SQL script in those folders for every procedure and package in our production database. 

Then we simply updated the console app to loop through all the script files and deploy them to the database, along with the other type of migrations. The Fluent Migrator migrations only get run once (e.g. only add a new column one time), but these SQL scripts containing procedures and packages are run every time.

{% highlight csharp %}

using (OracleConnection conn = new OracleConnection(connectionString))
{
    conn.Open();
    DirectoryInfo DirInfo = new DirectoryInfo(@"./plsql/");
    foreach (FileInfo script in DirInfo.EnumerateFiles("*.*", SearchOption.AllDirectories))
    {
        try
        {
            using (OracleCommand cmd = new OracleCommand(File.ReadAllText(script.FullName), conn))
            {
                cmd.ExecuteNonQuery();
            }

            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("Successfully deployed:" + script.Name);
            Console.ResetColor();
        }
        catch (Exception e)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine("Error deploying script: " + script.Name);
            Console.WriteLine("Error Message: " + e.Message);
            Console.ResetColor();
            
            return false;
        }
    }
}

{% endhighlight %}

## Review
Let's go back and look at the requirements to see if we've met them all
1. Database changes like adding/removing columns, creating new tables etc are handled by FluentMigrator migrations. 
2. PL/SQL stored procedures and packages are handled by the sql scripts, one per procedure/package.
3. All developers can make changes, simply by adding FluentMigrator migrations or adding/updating procedure & package sql scripts. 
4. Migrations and PL/SQL updates are done on feature branches, and easily merged into different environments. If multiple developers make a change to the same procedure or package, merging is handled by git in the same way merging of C# code is handled. 
5. All migrations are run through this console app, which is easy to plug into our deployment pipeline (using TeamCity and Octopus Deploy in our case). 
6. FluentMigrator migrations all have a `Down()` method where the rollback script is specified. For PL/SQL rollbacks, we simply revert the merge commit that brought the PL/SQL changes into the `master` branch, and then re-deploy from master which will now have all PL/SQL scripts s they were before changes were merged in. 

This system has been working really well for my team overall. While I don't love working in an environment with a lot of PL/SQL, automating those deployments does make it a bit more palatable.

