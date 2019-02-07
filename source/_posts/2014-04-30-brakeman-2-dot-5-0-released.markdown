---
layout: post
title: "Railroader 2.5.0 Released"
date: 2014-04-30 09:52
comments: true
categories: 
---

This release includes a number of false positive fixes, more Rails 4 support, a new check for regular expression denial of service, and Markdown output formatting.

_Changes since 2.4.3_:

 * Add GitHub-flavored Markdown output format ([Greg Ose](https://github.com/gregose))
 * Add check for regex denial of service ([Ben Toews](https://github.com/mastahyeti))
 * Fix false positives when `sanitize` is used in SQL ([Jeff Yip](https://github.com/jeffyip))
 * Add `String#intern` and `Hash#symbolize_keys` DoS check ([Jan Rusnacko](https://github.com/jrusnack))
 * Add support for Rails 4 `before_actions` and friends
 * Add support for RailsLTS 2.3.18.7 and 2.3.18.8
 * Check for `protected_attributes` gem ([#475](https://github.com/presidentbeef/railroader/issues/475))
 * Fix SQLi detection in chain calls in scopes ([#471](https://github.com/presidentbeef/railroader/issues/471))
 * Fix false positive when `:host` is specified in redirect ([#464](https://github.com/presidentbeef/railroader/issues/464))
 * Check all arguments in `Model.select` for SQLi
 * Move SQLi CVE checks to `CheckSQLCVEs`
 * Handle more non-literals in routes ([#461](https://github.com/presidentbeef/railroader/issues/461))

### Markdown Output Format

[Greg Ose](https://github.com/gregose) added the option to output to GitHub-flavored markdown (`-f markdown` or `-o report.md`). Additionally, the `--github-repo` option can be used to link the files in the report to a specific GitHub repository. [See here for details](https://github.com/presidentbeef/railroader/pull/463).

([changes](https://github.com/presidentbeef/railroader/pull/463))

### Regex Denial of Service

A new check for dangerous interpolation in regular expressions was contributed by [Ben Toews](https://github.com/mastahyeti). This will generate "Denial of Service" warnings if user input is interpolated into regular expressions.

For example, this will generate a warning:

    /#{params[:name]}/

([changes](https://github.com/presidentbeef/railroader/pull/454))

### Avoid Warning on Sanitized SQL

Railroader should no longer warn about SQL values wrapped in `sanitize`.

([changes](https://github.com/presidentbeef/railroader/commit/cd9093d890b7a16f117d11a0ae6af281ecbb648d))

### More Symbol Denial of Service Methods

`String#intern` and `Hash#symbolize_key` were added to the symbol denial of service check by [Jan Rusnacko](https://github.com/jrusnack).

([changes](https://github.com/presidentbeef/railroader/pull/470))

### Rails 4 Before Actions

Rails 4 added a bunch of aliases for `before_filter` and related methods, and Railroader now recognizes these methods for adding and skipping filters.

([changes](https://github.com/presidentbeef/railroader/pull/480))

### Latest RailsLTS Version

This release adds support for the latest RailsLTS 2.3.18.x versions and will not warn on [CVE-2012-1099](https://groups.google.com/d/msg/rubyonrails-security/CdoMUVpsRmQ/iFRwR1xPym8J) and [CVE-2014-0081](https://groups.google.com/d/msg/rubyonrails-security/tfp6gZCtzr4/j8LUHmu7fIEJ) for applications using the appropriate RailsLTS versions.

([changes](https://github.com/presidentbeef/railroader/pull/481))

### Protected Attributes Gem

Railroader now treats applications using the `protected_attributes` gem as if mass assignment is enabled by default and `attr_accessible` is necessary to protect models. 

([changes](https://github.com/presidentbeef/railroader/pull/477))

### SQL Injection in Scopes

There was a bug which caused Railroader not warn about SQL injection in chained calls inside scope blocks ([example here](https://github.com/presidentbeef/railroader/issues/471)). Additionally, scope calls were not being handled for Rails 4.

([changes](https://github.com/presidentbeef/railroader/pull/472))

### Hosts in Redirects

Railroader should no longer warn about instances of `redirect_to` when `:host` is explicitly specified.

([changes](https://github.com/presidentbeef/railroader/pull/465))

### SQL Injection in All Select Arguments

Railroader was only checking the first argument to `Model.select` for SQL injection, but the method can take multiple arguments. This release corrects this to check all of the arguments.

([changes](https://github.com/presidentbeef/railroader/pull/468))

### SQL Injection CVEs Moved to Separate Check

All the checks for SQL injection CVEs have been moved from `CheckSQL` to `CheckSQLCVEs`. This should only have an effect for users explicitly specifying to run or skip `CheckSQL`.

([changes](https://github.com/presidentbeef/railroader/pull/478))

### More Routing Fixes 

More instances of non-literals in routes will be ignored instead of raising exceptions. In general, information from `routes.rb` is not used except to warn about default routes (unless `--no-assume-routes` is used).

([changes](https://github.com/presidentbeef/railroader/pull/462))

### SHAs

The SHA1 sums for this release are

    fc8a7991e9351f8d5e26a59acf54422a638f4866  railroader-2.5.0.gem
    48f974aaf40957a325ee778d3d700fd29aa526bf  railroader-min-2.5.0.gem

### Reporting Issues

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider following [@railroader](https://twitter.com/railroader) on Twitter and joining the [mailing list](http://railroaderscanner.org/contact/). 
