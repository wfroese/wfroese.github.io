---
layout: post
title: "Pull Request Review Checklist"
excerpt_separator: <!--end_excerpt-->
tags: code best-practices software-teams
image: /assets/images/pr-review.jpg
cover_image: /assets/images/pr-review.jpg
cover_alt_text: a screen showing some code
description: A reference checklist for reviewing pull requests
---
In any organization, there are certain requirements that code has to meet before it's considered production ready.
I find it helpful to have an explicit documented checklist that is the base for reviewing any pull request.

<!--end_excerpt-->

Not only does this help reviewers so they don't forget to consider something, but it also makes it easier for developers to know when something they're working on is actually ready for production. This helps increase the overall quality of pull requests and helps them get merged & deployed quicker.

This is not a full, comprehensive list, of course - it's just a base that covers the most common requirements.

1. Correctness: does the code, you know, work? And has that been proven by testing in a QA environment, somewhere other than the developer's machine? Does it pass all automated tests?
2. Maintainability: is the code reasonably easy to understand? Any parts that are unclear may need refactoring, or at the very least, some documentation.
3. Coding standards: are coding standards followed? Your standards may vary, but this is where we check for naming conventions, class/method sizes, etc.
4. Tests: are the required tests present? Unit tests, integration tests, whatever happens to be relevant for the specific pull request.
5. UI: if there is a UI component to this pull request, is it visually consistent with the rest of the application?
6. Compatibility: if applicable, has it been tested on all supported browsers?
6. Database migrations: are migrations included for deploying and rolling back?
7. Exception/error handling: exceptions and errors should be handled in a way that is appropriate to the context (including logging)
8. Logging: is adequate logging included, again appropriate to the context?
9. Documentation: is documentation included and adequate, both for developers as well as Operations, Management, etc as needed?
10. Performance and scalability: are current performance requirements met, and have future performance requirements been considered?
11. Deployment: if the application/service is new, is it set up for auto-deployment?


