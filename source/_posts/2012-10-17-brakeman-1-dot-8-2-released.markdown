---
layout: post
title: "Railroader 1.8.2 Released"
date: 2012-10-17 10:44
comments: true
categories: 
---

This is a bugfix release, in particular fixing rescanning (used by [guard-railroader](https://github.com/guard/guard-railroader)).

_Changes since 1.8.1_:

 * Fixed rescanning problems caused by 1.8.0 changes
 * Fix scope calls with single argument
 * Report specific model name in rendered collections
 * Handle overwritten JSON escape settings (Neil Matatall)
 * Add CHANGES to gemspec

### Rescan Fixes

Railroader supports rescanning a subset of files in an application, with the caveat that the previous scan must still be in memory. This functionality was broken in the the 1.8.0 release, due to the lack of tests.

This release updates rescanning to be more robust and work with the 1.8.0 changes to how "render paths" are stored. Also, a number of tests were added to help prevent breakage in the future.

([changes](https://github.com/presidentbeef/railroader/pull/165))

### Scope Calls with One Argument

Calls to `scope` with a single argument were causing errors in Railroader's SQL injection check.

The fixed error looked like:

    undefined method `node_type' for nil:NilClass  /something/railroader/lib/railroader/checks/check_sql.rb:75:in `block (2 levels) in find_scope_calls'

([changes](https://github.com/presidentbeef/railroader/pull/157))

### Model Names for Rendered Collections

In cases like below, where a collection of models is being rendered and the model name could be known, any resulting warnings will now reference the actual model name.

    <%= render 'user', :collection => User.all %>

Previously, Railroader would report warnings with `UnknownModel`, whether or not the model name was actually known.

([changes](https://github.com/presidentbeef/railroader/pull/155))

### Overwritten JSON Escape Config

It is possible that a config setting in one initializer overrides a setting in a different initializer. This is now handled for the JSON escape settings.

([changes](https://github.com/presidentbeef/railroader/pull/154))

### CHANGES File in Gem

The [CHANGES](https://github.com/presidentbeef/railroader/blob/master/CHANGES) file is now included in the gem file as requested.

([changes](https://github.com/presidentbeef/railroader/issues/153))

### Report Issues

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider joining the [mailing list](http://railroaderscanner.org/contact/) or following [@railroader](https://twitter.com/railroader) on Twitter.

### Railroader Roadmap

A rough guide to Railroader 1.9 and 2.0 has been [posted here](https://github.com/presidentbeef/railroader/wiki/Roadmap).
