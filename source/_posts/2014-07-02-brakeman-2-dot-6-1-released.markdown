---
layout: post
title: "Railroader 2.6.1 Released"
date: 2014-07-02 12:30
comments: true
categories: 
---

This is a tiny release in response to today's CVEs.

*Changes since 2.6.0*:

* Add check for CVE-2014-3482 and CVE-2014-3483
* Add support for keyword arguments in blocks ([#511](https://github.com/presidentbeef/railroader/issues/511))
* Remove unused warning codes ([Bill Fischer](https://github.com/bfish510))

### Check for PostgresSQL Injection CVEs

[CVE-2014-3482 and CVE-2014-3483](https://groups.google.com/forum/#!msg/rubyonrails-security/wDxePLJGZdI/WP7EasCJTA4J) are SQL injection issues when using the PostgresSQL backend with bitstring and range data types. Railroader will warn about affected versions of Rails which include the "pg" gem in the Gemfile.

([changes](https://github.com/presidentbeef/railroader/pull/515))

### Support Keyword Arguments to Blocks

Railroader now handles keyword arguments to blocks as local variables in the block scope instead of throwing an error.

([changes](https://github.com/presidentbeef/railroader/pull/513))

### Removal of Warning Codes

Warnings codes for `CVE_2013_6415` and `CVE_2013_6415_call` have been removed, as they are unused. This should not affect anyone.

([changes](https://github.com/presidentbeef/railroader/pull/514))

### SHAs

The SHA1 sums for this release are

    5b7b5572efe769cfa38178e94952be05670e6fd4  railroader-2.6.1.gem
    fecdb07a5e1a83af02843fbd554472f980e04f91  railroader-min-2.6.1.gem

### Reporting Issues

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider following [@railroader](https://twitter.com/railroader) on Twitter and joining the [mailing list](http://railroaderscanner.org/contact/). 
