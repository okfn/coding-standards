# Open Knowledge Coding Standards and Style Guide

This document describes coding standards and style guides for use at Open Knowledge International.

## General Principles

* **Testing**: Code should be tested and we recommend test-driven (or test-oriented) development.
* **Continuous Integration**: wherever possible testing should be automated and part of push to the main repo
* **Versioning**: All code should be kept in a distributed version control system (git)
* **Languages**: we have two "approved" languages: Python and Javascript (NodeJS). If you plan to develop in another language please flag this and discuss.

----

## TL;DR

* Use spaces and never tabs
* Javascript, HTML and CSS with 2 space indentation; Python with 4 space indentation
* 79 character line limit
* Lint Javascript with `jscs` using `esnext`; Lint Python using `pylint`
* Use language conventions for naming functions, classes and variables. These conventions are quite clear for both Python and Javascript
* Code should be submitted via pull requests, which another person should merge
* Tests are required. Unit tests, as well as functional and integration tests.
* Aiming for 80% and above test coverage is desirable
* Write small, reusable libraries as possible
* Documentation is just as important as tests.
  * Document your code with docstrings
  * Provide great `README` files with examples of how to use
  * Only use documentation builders like Sphinx for large projects; prefer to document projects really well in README files

## Python

In general follow the python style guide (PSG) as formulated in PEP 8: http://www.python.org/dev/peps/pep-0008/

### Formatting

* Tabs vs. Spaces
  * Spaces
  * 4 spaces for a tab
* 79 character limit: in general all lines should be wrapped at 79 characters
* Quote character: use ' not " wherever possible (including docstrings)

### Coding

As in PSG, e.g.:

* all variables and method names are lower_case_with_underscores
* class names: capital camel case
* do not make extra functions or methods to wrap one line statements or calls to well known libraries unless there is a very good reason
* if a method does not use the 'self' or 'cls' parameter, think: should it really be a method? most likely it should be a utility function as it has nothing to do with the class in question.
* the @classmethod decorator should be used sparingly, consider is it really necessary? could its job be accomplished with a simple function or a factory class?
* the first argument to a classmethod should be 'cls' not 'self'. 'self' is for instances.
* for paste or pylons derived applications, use 'paste.deploy.converters.asbool' to check boolean configuration variables. do not try to rewrite this function or "set config variable to any value (e.g. false) to enable".

### Documentation

* Use sphinx style documentation conventions
  * See for function/method parameters: http://packages.python.org/an_example_pypi_project/sphinx.html#function-definitions
* All arguments and return values of public apis *should* be documented

### Checking

Use pylint: http://www.logilab.org/857

### Frameworks

* WebApps: we prefer Flask (though we have many legacy apps in Pylons)

### Testing

* Use nosetests

### External Resources

* http://lists.osafoundation.org/pipermail/dev/2003-March/000479.html - David Jeske post - very good.
* http://epydoc.sourceforge.net/epytextintro.html epytext

----

## Javascript and NodeJS

Write `es6` in all new libraries, and compile with WebPack or Browserify. See some [existing](https://github.com/okfn/gobetween) [examples](https://github.com/okfn/spend-publishing-dashboard) of OKI codebases using `es6` on for both backend and frontend code.

Specific items:

* Indentation: 2-spaces (not tabs)
  * See e.g. http://nodeguide.com/style.html#tabs-vs-spaces
* Line-length: 79 characters
* Don't use commas in `es6` - let the compiler take care of that stuff

### Testing

* Use `mocha` for tests
* Use `Zombie.js` or `jsdom`, when tests require a browser

### Documentation

We do not have strong recommendations here but if you are using a parameter convention we recommend JSDoc: http://jsdoc.sourceforge.net/#usage

* See also: JS Doc Toolkit: http://code.google.com/p/jsdoc-toolkit/wiki/TagReference

### Frameworks

* NodeJS: we use Express by default
* Javascript: we've historically used Backbone. We have not yet settled on moving forward with React or Angular.
  * Toolbelt libraries: `jQuery`, `lodash`

----

## CSS

* Indent: 2-space spaces
* open bracket on same line as css-selector
* space after selector before bracket


```
body {
  font-family: Arial;
}

body, h1, h2 {
}
// or
body,
h1
h2 {
  display: block;
}
```

----

## Distributed Version Control

We use git for all projects.

### Commit Messages

* Commit messages should be written in plain sentences that describe the change made and what area of the code it relates to. The following style guide has good recommendations for formatting commit messages: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
* If a project is hosted on GitHub, it is recommended that relevant issue numbers are referenced in the commit message where appropriate. Use the convention of `#{issue-id}` in commit messages to automatically link back to issues. Issues can also be closed via commit messages, e.g. "... fixes #123" (https://help.github.com/articles/closing-issues-via-commit-messages/).

### Branch-per-feature (and per-bug)

This approach is frequently recommended and may be adopted on a per-project
basis, and is especially recommended for larger projects:

* Create a branch for each feature of bug. Naming convention: bug-{bug-name}, feature-{feature-name}
* Close and merge into default once QA is done

For more discussion of how this works:

* http://forceten.tidalwave.it/development/mercurial-best-practices/
* http://www.rabbitmq.com/mercurial.html#branchperbug

----

## Continuous Integration

* We use Travis by default - get in touch if you need access to okfn account

----

## Web Applications

### URL Structure

* In general do not use trailing slash on urls (but ensure you redirect 301 from trailing slash to non-trailing slash)
  * e.g.: /work not /work/, /work/9 not /work/9/

### RESTful Services

* Singular is preferred to plural for entity names - person vs person (or people), record vs records etc
  * No clear decision on this AFAICT on the wb
  * http://microformats.org/wiki/rest/urls - prefers plurals
  * http://blog.roberthahn.ca/articles/2007/04/06/url-design/ - prefers singulars
* Searching/filtering should generally be done outside of REST
  * If done via REST must be done via url fragments and '''not''' via query parameters: e.g. /api/rest/person/age/39 (not /api/rest/person?age=39)
