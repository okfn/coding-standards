# Open Knowledge International Coding Standards

This document outlines coding standards for use at Open Knowledge International. It is a living document, and we encourage pull request and issues to improve on or contest ideas as expressed.

## Related documents

* [Code reviews](sections/reviews.md): A description of our general code review process at Open Knowledge International.

## TL;DR

* We use Python and Javascript (Node.js). If you plan to develop in another language please flag this and discuss.
* Tests are required. Unit tests, as well as functional and integration tests. Aiming for test coverage of 80% and above is desirable.
  * Tests must be automated via a continuous integration platform that is triggered when code is pushed to the canonical repository. 

* Documentation is required for all code. Documentation is just as important as tests.
  * Document functions, classes, modules and packages with docstrings.
  * Provide a great `README.md` file with examples of how to use the code.
  * Only use documentation builders like Sphinx for large projects; prefer `README.md` files for brevity and accessibility of documentation.

* Use spaces and never tabs.
  * Javascript, HTML and CSS: 2 space indentation.
  * Python: 4 space indentation.
* Strictly enforce a 79 character line limit.
* Lint Javascript with `eslint`; Lint Python using `pylint`.
* Use common language conventions for naming functions, classes and variables.

* Code should be submitted via pull requests, which another person should merge.
* Use continuous deployment.
  * Apps should be deployed from Travis when a successful build is made on the branch used for production.
  * Packages should be published to the respective package registry when a tag is pushed.
* Write small, reusable libraries where possible. There are many opportunities for reuse across our different products.

---

## Languages

Our work is done in Python and Javascript (Node.js). There can be good reasons for writing a particular library or app in another language, but if you think this is the case, please raise this issue directly before starting any work.

For example apps that implement the OKI preferences, see the following:

* [opendata lib in Javascript](https://github.com/okfn/opendata-js)
* [opendata lib in Python](https://github.com/okfn/opendata-py)

## Style and linting

### Python

1. Follow the Python Style Guide (PSG) as formulated in PEP-8: http://www.python.org/dev/peps/pep-0008/
2. Use `pylint` to lint code.

The critical points are:

* Use spaces; never use tabs
* 4 space indentation
* 79 character line limit
* Variables, functions and methods should be `lower_case_with_underscores`
* Classes are `TitleCase`

And other preferences:

* Use ' and not " as the quote character by default
* When writing a method, consider if it is really a method (needs `self`) or if it would be better as a utility function
* When writing a `@classmethod`, consider if it really needs the class (needs `cls`) or it would be better as a utility function or factory class

### Javascript

1. Use `eslint` to lint code.
2. Prefer to write all new code in `ES6` and compile/transpile with Webpack or Browserify. This applies to frontend and backend code. In some cases, the cost of transpilation (inflated file size) is too great (for small utility libraries), so use judgement.

The critical points are:

* Use spaces; never use tabs
* 2 space indentation
* 79 character line limit
* Variables, functions and methods should be `camelCase`
* Classes are `TitleCase`

And other preferences:

* Don't use semi-colons in `ES6` or any code that you are transpiling - it is quite unnecessary.

## Testing

### Python

1. Use `tox` with `py.test` to test code.

### Javascript

1. Use `mocha` to test code.
2. Use `Zombie.js` or `jsdom` for tests that require a DOM.

## Documentation

### Python

#### Docstrings

Use Sphinx-style or Google-style documentation conventions.

* http://packages.python.org/an_example_pypi_project/sphinx.html#function-definitions
* https://google.github.io/styleguide/pyguide.html#Comments

#### User documentation

Prefer to make really good `README.md` files, rather than implementing a full documentation framework.

### Javascript

#### Docstrings

Use Google-style documentation conventions.

* https://google.github.io/styleguide/javascriptguide.xml#Comments

#### User documentation

Prefer to make really good `README.md` files, rather than implementing a full documentation framework. 

## Frameworks

We prefer the following frameworks and libraries. If you want to use an *alternative to one of these please flag this before starting any work.

### Python

* Flask
* Click

### Javascript

* lodash
* Express
* React
* Angular

## Version control

We use Git for all projects.

### Branch management

We generally follow Git Flow, with some modifications, and some flexibility per project. The following should hold true for pretty much all projects:

* Have a `master` branch
* Never commit directly to `master`
* Always work from a `feature/{}` or a `fix/{}` branch that is checked out from `master`
* Always reference issues from Git messages using `#{issue_id}`, and the various other related conventions used by most Git hosts.
* Properly describe changes in commit messages: "Fixes database migration script failure on Python 2.7", not "Fix."

## Continuous integration and deployment

All projects must be configured with a CI server. We use Travis CI by default. The CI server must run the test suite with linting.

## App deployment

All apps must be deployed from the CI server.

## Package publication

All packages must be published to npm and pypi from the CI server.

## Web apps

### URLs

* In general do not use trailing slash on urls (but ensure you redirect 301 from trailing slash to non-trailing slash)
  * e.g.: /work not /work/, /work/9 not /work/9/

### RESTful APIs

* Use plural versions of entities names for endpoints
* When implementing RESTful APIs, keep them RESTful, but don't hesitate to create endpoints that are not RESTful when it is practical
