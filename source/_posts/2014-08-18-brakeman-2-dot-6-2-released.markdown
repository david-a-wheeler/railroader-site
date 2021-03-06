---
layout: post
title: "Railroader 2.6.2 Released"
date: 2014-08-18 09:15
comments: true
categories: 
---

This release is mostly bug fixes and updates, but does include two new options.

*Changes since 2.6.1:*

* Add check for CVE-2014-3514
* Add `--add-checks-path` option for external checks (Clint Gibler)
* Add `-4` option to force Rails 4 mode
* Fix SQL injection detection in deep nested string building
* Check entire call for `send` ([#523](https://github.com/presidentbeef/railroader/issues/523))
* Check for .gitignore of secrets in subdirectories ([#519](https://github.com/presidentbeef/railroader/issues/519))
* Avoid warning about symbolizing safe parameters ([#536](https://github.com/presidentbeef/railroader/issues/536))
* Fix block statment endings in Erubis ([#518](https://github.com/presidentbeef/railroader/issues/518))
* Update ruby2ruby dependency to 2.1.1
* Expand app path in one place instead of all over (Jeff Rafter)
* Fix undefined variable in controller processing error (Jason Barnabe)

### Mass Assignment Bypass (CVE-2014-3514)

[CVE-2014-3514](https://groups.google.com/d/msg/rubyonrails-security/M4chq5Sb540/CC1Fh0Y_NWwJ) describes an issue where  `create_with` does not implement strong parameters, allowing mass assignment in Rails 4.x. For vulnerable versions, Railroader warns about instances of `create_with` or a generic warning if no uses are found.

([changes](https://github.com/presidentbeef/railroader/pull/540))

### External Check Option

[Clint Gibler](https://github.com/clintgibler) has added the `--add-checks-path` option to provide an path to search for additional checks. This is useful if you wish to write your own custom rules for Railroader to run.

([changes](https://github.com/presidentbeef/railroader/pull/532))

### Option to Force Rails 4

If the Rails version for an application cannot be determined automatically for some reason, the `-4` option will force Railroader to treat it like a Rails 4 application.

Included with this change are some fixes when a Rails 4 app is detected but the exact version number cannot be determined. This may change the output for some scans.

([changes](https://github.com/presidentbeef/railroader/pull/527))

### SQL Injection in Nested Strings

This release fixes some SQL injection detection when there is lots of string building mixing concatenation and interpolation. These changes may also affect which value Railroader warns about within the string.

([changes](https://github.com/presidentbeef/railroader/pull/528))

### Better Send Call Detection

Previously, Railroader was ignored calls to `send` when they were nested inside a chain of calls. This has been fixed.

([changes](https://github.com/presidentbeef/railroader/pull/524))

### Ignored Secrets

Railroader now checks subdirectories for `.gitignore` files which determing if the secrets configuration is being ignored.

([changes](https://github.com/presidentbeef/railroader/pull/521))

### Symbolizing Safe Paramaters

Since `params[:controller]` and `params[:action]` are quite difficult (possibly impossible) to DoS, Railroader will not warn about symbolizing them.

([changes](https://github.com/presidentbeef/railroader/pull/538))

### Erubis Fixes

Some ERB templates were not parsing correctly due to how Railroader was handling the end of blocks. This should be resolved now.

([changes](https://github.com/presidentbeef/railroader/pull/520))

### Ruby2Ruby Dependency Updated

Railroader now depends on the latest version of Ruby2Ruby due to the [fix here](https://github.com/seattlerb/ruby2ruby/commit/a1576d12cb1e5e379875548abfd441c6e3095f4a).

([changes](https://github.com/presidentbeef/railroader/pull/537))

### Expand App Path Once

[Jeff Rafter]() refactored a bunch of code which was converting the application path to an absolute path and instead moved it to one (okay, maybe two) spots. This should not affect any reports.

([changes](https://github.com/presidentbeef/railroader/pull/534))

### Error in Controller Processing

[Jason Barnabe](https://github.com/JasonBarnabe) fixed an error...in the error handling when processing controllers.

([changes](https://github.com/presidentbeef/railroader/pull/517))

### SHAs

The SHA1 sums for this release are

    f225541559d2fbe5374d481b6105b66053f9710a  railroader-2.6.2.gem
    67882d467b6a8fc6e504b6dcb9605f79a0c6a22c  railroader-min-2.6.2.gem

### Reporting Issues

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider following [@railroader](https://twitter.com/railroader) on Twitter and joining the [mailing list](http://railroaderscanner.org/contact/). 
