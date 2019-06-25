# Code reviews

At Open Knowledge Foundation (OKF) all code must be reviewed by a colleague before merging into the main branch of the repository (usually `master`). This short document examples how to do code reviews, and why we do it.

## How

The process for code reviews is straight forward as long as you are already following our coding standards for working with version control, and in particular our git flow-influenced process of branch management. The bottom line is that, before any code hits `master`, it must be reviewed by a colleague.

### Submitting code for review

Submitting code for review should follow these steps:

1. Always, always work from a feature or fix branch that is checked out of `master`.
2. Each feature or fix branch should be focused on a discrete unit of work.
3. When your unit of work is complete, submit a pull request against the `master` branch on `origin`. Ensure your [commit message](https://github.com/okfn/coding-standards#version-control) is communicative.
4. Wait for the CI server to run, validating your tests pass on all target environments. If you do not have tests, or have not configured CI, do that immediately before proceeding.
5. If CI is green, ask a colleague to review your pull request (we will automate this in the near future). This preferably will be a colleague who is not working on your project.
6. Address any questions from the code review. Sometimes this will involving refactoring, other times it will just mean answering questions.
7. When the reviewer indicates that the pull request is ready to merge, you may merge into `master`. It is *recommended* that the developer merge her own branch into master, due to the cross-project review process (the developer can decide the best time to merge, after the review has approved the merge).
8. **If** your branch was a branch on the main repository (usually `origin`), then you must also remove your branch to reduce clutter. 

### Reviewing code in a pull request

Reviewing someone else's code should follow the following steps:

1. Respond to a request for a code review immediately. Indicate when you can do it ("now", "in the next hour", and so on).
2. Review the pull request, using inline commenting for specific issues.
3. If you are satisfied with the pull request (without any questions, or after your questions have been answered), then explicitly state that the pull request is ready to be merged as a comment on the pull request.

### A simple checklist for reviewers

Remember that the primary reason for doing code reviews at Open Knowledge Foundation is to distribute knowledge across our team. This does mean identifying areas the code could be improved and asking useful questions, but it does not mean you go too deeply on issues that are clearly subjective.

Here are some points to hold in mind and guide the review process:

* What is the context for the code in this pull request (what does the app/library actually do)?
* What is the desired functionality being introduced or fixed?
* Is the code idiomatic for the language and/or framework it is written in?

There are some clear red flags that, on seeing any of them, you should immediately ask your colleague to address before continuing with any code review:

* There is no CI
* There are no tests
* There are tests that fail
* There is code that is not linted

### Prioritizing code reviews

Code reviews should take the highest priority of work during the day. When a colleague asks for a review, s/he is asking for work to be validated, and to be unblocked in order to move forward to other tasks. Respect this and address the code review as soon as possible.

Sometimes, you will be asked to review and you are simply not available (due to meetings or deadlines on the same day - not due to "having your own work to do"). In such cases, communicate immediately with the colleague requesting review so that s/he can find an alternative.

### Effort, distraction, and code reviews

Considering the priority given to code reviews, it could be easy to fall into seeing them as a distraction, or a wasted effort. Try to avoid this way of thinking, and relate to the reasons why we are actually doing code reviews (outlined in "Why") below.

### Expertise

A situation may occur where you are reviewing a language that you do not feel skilled enough in. This does not prevent your ability to review. Ask the developer simple questions, try to understand the general flow. There is an important learning element in this process - languages, techniques, projects, requirements - so lack of familiarity with a language is not a blocker to being a reviewer.

### Responsibility

Reviewers don't hold final responsibility for code - the person who wrote the code does. Reviewing is a best effort endeavour. 

## Why

There are many reasons to do code reviews, some technical and some social (in fact, all the reasons are a mix of both). 

Here are the reasons that are important for us to do code reviews at OKI now:

* We have a diverse team of developers with a wide range of professional experience: code reviews are an avenue for knowledge sharing.
* We have a great number of projects and products, but most of us work in particular areas: code reviews provide visibility and insight into what else is happening with our technical product beyond what any one person directly works on.
* It can be easy to get stuck in patterns when writing code and focused on delivery: code reviews open the possibility for collaborative problem solving.

