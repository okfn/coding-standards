# Open Knowledge Coding Standards and Style Guide

# General Principles

* Testing: Code should be tested and we recommend test-driven (or test-oriented) development.
* Continuous Integration: wherever possible testing should be automated and part of push to the main repo
* All code should be kept in a distributed version control system (git)
* Languages: we have two "approved" languages: Python and Javascript (NodeJS).
  If you plan to develop in another language please flag this and discuss.

----

# Python

In general follow the python style guide (PSG) as formulated in PEP 8: http://www.python.org/dev/peps/pep-0008/

## Formatting

* Tabs vs. Spaces
  * Spaces
  * 4 spaces for a tab
* 79 character limit: in general all lines should be wrapped at 79 characters
* Quote character: use ' not " wherever possible (including docstrings)

## Coding

As in PSG, e.g.:

* all variables and method names are lower_case_with_underscores
* class names: capital camel case
* do not make extra functions or methods to wrap one line statements or calls to well known libraries unless there is a very good reason
* if a method does not use the 'self' or 'cls' parameter, think: should it really be a method? most likely it should be a utility function as it has nothing to do with the class in question.
* the @classmethod decorator should be used sparingly, consider is it really necessary? could its job be accomplished with a simple function or a factory class?
* the first argument to a classmethod should be 'cls' not 'self'. 'self' is for instances.
* for paste or pylons derived applications, use 'paste.deploy.converters.asbool' to check boolean configuration variables. do not try to rewrite this function or "set config variable to any value (e.g. false) to enable".

## Documentation

* Use sphinx style documentation conventions
  * See for function/method parameters: http://packages.python.org/an_example_pypi_project/sphinx.html#function-definitions
* All arguments and return values of public apis *should* be documented

## Checking

Use pylint: http://www.logilab.org/857

## Frameworks

* WebApps: we prefer Flask (though we have many legacy apps in Pylons)

## Testing

* Use nosetests

## External Resources

* http://lists.osafoundation.org/pipermail/dev/2003-March/000479.html - David Jeske post - very good.
* http://epydoc.sourceforge.net/epytextintro.html epytext

----

# Javascript and NodeJS

We follow these existing recommendations:

* http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
* http://javascript.crockford.com/code.html

Specific items:

* Indentation: 2-spaces (not tabs)
  * See e.g. http://nodeguide.com/style.html#tabs-vs-spaces
* Line-length: 80 characters
* [Not yet consensus on] leading-commas - https://gist.github.com/357981

## Testing

* Use mocha or QUnit (Mocha for NodeJS)
* Sinon for mocking

## Documentation

We do not have strong recommendations here but if you are using a parameter convention we recommend JSDoc: http://jsdoc.sourceforge.net/#usage

* See also: JS Doc Toolkit: http://code.google.com/p/jsdoc-toolkit/wiki/TagReference

## Frameworks

* NodeJS: we use Express by default
* Javascript: we use Backbone by default
  * Toolbelt library: jQuery + Underscore (or lodash)


----

# CSS

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

# Distributed Version Control

We use git for all projects.

## Commit Messages

* Recommend use of github convention of using `#{issue-id}` in commit messages
  (along with `fixes #19`
* [Optional]: Convention of including tag and size of commit at start of
  summary using `[]` e.g. `[ux][m] This commit does X` - here the tag is "ux"
  (relates to ux) and size of commit is "m" (medium). Sizes are `xs,s,m,l`. It
  is also possible just to use size specifiers and drop the tag i.e. `[xs] fix
  whitespace`.

## Branch-per-feature (and per-bug)

This approach is frequently recommended and may be adopted on a per-project
basis, and is especially recommended for larger projects:

* Create a branch for each feature of bug. Naming convention: bug-{bug-name}, feature-{feature-name}
* Close and merge into default once QA is done

For more discussion of how this works:

* http://forceten.tidalwave.it/development/mercurial-best-practices/
* http://www.rabbitmq.com/mercurial.html#branchperbug

----

# Continuous Integration

* We use Travis by default - get in touch if you need access to okfn account

----

# Web Applications

## URL Structure

* In general do not use trailing slash on urls (but ensure you redirect 301 from trailing slash to non-trailing slash)
  * e.g.: /work not /work/, /work/9 not /work/9/

## RESTFul Services

* Singular is preferred to plural for entity names - person vs person (or people), record vs records etc
  * No clear decision on this AFAICT on the wb
  * http://microformats.org/wiki/rest/urls - prefers plurals
  * http://blog.roberthahn.ca/articles/2007/04/06/url-design/ - prefers singulars
* Searching/filtering should generally be done outside of REST
  * If done via REST must be done via url fragments and '''not''' via query parameters: e.g. /api/rest/person/age/39 (not /api/rest/person?age=39)


