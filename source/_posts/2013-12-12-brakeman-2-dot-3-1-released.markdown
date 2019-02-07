---
layout: post
title: "Railroader 2.3.1 Released"
date: 2013-12-12 23:24
comments: true
categories: 
---

Two minor bugs were fixed in this release. Please see the [2.3.0 release post](http://railroaderscanner.org/blog/2013/12/11/railroader-2-dot-3-0-released/) if you are upgrading from an earlier version.

([changes](https://github.com/presidentbeef/railroader/pull/415))

_Changes since 2.3.0_:

 * Fix check for CVE-2013-4491 (i18n XSS) to detect workaround
 * Fix link for CVE-2013-6415 (number_to_currency)

### i18n XSS Workaround

Railroader 2.3.0 included a check for the [official i18n XSS workaround](https://groups.google.com/d/msg/ruby-security-ann/pLrh6DUw998/bLFEyIO4k_EJ), but it was commented out during testing and unfortunately left that way.

### CVE-2013-6415 Link

The link provided for [CVE-2013-6415](https://groups.google.com/d/msg/ruby-security-ann/9WiRn2nhfq0/2K2KRB4LwCMJ) in Railroader 2.3.0 was copy-pasted from an older check. This has been fixed.

### SHAs

The SHA sums for this release are

    469b209a4c72f5a1133d696575caeee1675837e7  railroader-2.3.1.gem
    827e1cdefba543f59ed5070aaa3f587d8c7d9513  railroader-min-2.3.1.gem

### Reporting Issues

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider joining the [mailing list](http://railroaderscanner.org/contact/) or following [@railroader](https://twitter.com/railroader) on Twitter.
