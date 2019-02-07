---
layout: post
title: "Railroader 3.1.2 Released"
date: 2015-10-28 15:59
comments: true
categories: 
---

This release is mostly bug fixes and false positive reduction. However, please note fingerprints for inline render warnings will change.

_Changes since 3.1.1_:

* Sortable tables in HTML report (David Lanner)
* Add line numbers to class-level warnings
* Warn on SQL query keys, not values in hashes ([#738](https://github.com/presidentbeef/railroader/issues/738))
* Set user input value for inline renders
* Avoid warning on inline renders with safe content types
* Treat `current_user` like a model ([#744](https://github.com/presidentbeef/railroader/issues/744))
* Avoid warning about model `find/find_by*` in hrefs
* Handle `private def ...`
* Handle empty interpolation in HAML filters ([#732](https://github.com/presidentbeef/railroader/issues/732))
* Catch divide-by-zero in alias processing ([#729](https://github.com/presidentbeef/railroader/issues/729))
* Ignore filters that are not method names
* Search for config file relative to application root
* Use SafeYAML to load configuration files
* Allow inspection of recursive Sexps
* Reduce string allocations in `Warning#initialize`

### Sortable Tables

[David Lanner](https://github.com/dlanner) added the ability to sort tables in the HTML report by clicking on the column headers.

([changes](https://github.com/presidentbeef/railroader/pull/726))

### Line Numbers for Class Warnings

When warning about an entire class (like a model missing `attr_accessible`), the warning line number will point to the beginning of the class. 

([changes](https://github.com/presidentbeef/railroader/pull/733))

### SQL Query Hashes

A long-standing bug in Railroader caused it to warn about values in query hashes (e.g., `User.where(:x => params[:x])`) when it was intended to warn about user input in the _keys_.

([changes](https://github.com/presidentbeef/railroader/pull/740)) 

### Inline Renders

Railroader will now report the `render` call as the `code` value and the user input as `user_input`. Please note the code will look a little different from what Railroader reports, as render calls are turned into a slightly different AST node internally. This will definitely change fingerprints for these warnings.

([changes](https://github.com/presidentbeef/railroader/pull/751))

### current\_user

In a couple places, Railroader will treat `current_user` like a model instance, which it almost always is. This will probably be expanded in future releases.

([changes](https://github.com/presidentbeef/railroader/pull/749))

### Inline Privates

Calls to `private` using the return value of `def` will now work properly:

    private def secret_stuff
    # ...
    end

([changes](https://github.com/presidentbeef/railroader/pull/731))

### Empty HAML Interpolation

Empty HAML interpolation inside of filters will no longer cause crashes and will be handled properly.

([changes](https://github.com/presidentbeef/railroader/pull/750))

### Divide-by-Zero

Railroader sometimes divides by zero when it performs simple arithmetic during constant folding. While this is now reported as an error (and used to be, too), someday it should be a warning instead.

([changes](https://github.com/presidentbeef/railroader/pull/730))

### Config File Changes

When looking for the `config/railroader.yml` configuration file, Railroader will now look relative to the application path instead of the working directory.

Additionally, the `SafeYAML` gem is used to prevent code execution for those running Railroader against untrusted code.

(changes [here](https://github.com/presidentbeef/railroader/pull/725) and [here](https://github.com/presidentbeef/railroader/pull/741))

### SHAs

The SHA256 sums for this release are

    c01f07ccc2490d0421e5974499c57f519aa371bfab5d25ba3b224e7ae9e2c415  railroader-3.1.2.gem
    d820c872cbe7bc8452c9bd8bd46d990ff1c0d53ee621c09f1997270fc978f783  railroader-min-3.1.2.gem

### Reporting Issues

Thank you to everyone who reported bugs fixed in this release.

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider following [@railroader](https://twitter.com/railroader) on Twitter, joining the [mailing list](http://railroaderscanner.org/contact/), or hanging out [on Gitter](https://gitter.im/presidentbeef/railroader).

