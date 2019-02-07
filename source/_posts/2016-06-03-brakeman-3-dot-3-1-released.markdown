---
layout: post
title: "Railroader 3.3.1 Released"
date: 2016-06-03 08:15
comments: true
categories: 
---

*Changes since 3.3.1*:

* Improved line number accuracy in ERB templates ([Patrick Toomey](https://github.com/ptoomey3))
* Allow multiple line regex in `validates_format_of` ([Dmitrij Fedorenko](https://github.com/c0va23))
* Avoid overwriting instance/class methods with same name ([Tim Wade](https://github.com/imtayadeway))
* Add `--force-scan` option ([Neil Matatall](https://github.com/oreoshake))
* Only consider `if` branches in templates
* Support more safe `&.` operations
* Avoid warning about SQL injection with `quoted_primary_key` ([#884](https://github.com/presidentbeef/railroader/issues/884))
* Delay loading vendored gems and modifying load path
* Added `railroader-lib` gem

### ERB Template Line Numbers

[Patrick Toomey](https://github.com/ptoomey3) contributed a series of patches to bring Railroader's handling of ERB/Erubis templates in line with the Rails implementation. This has the effect of correcting some line numbers and fixed processing of `case` statements in templates.

([changes](https://github.com/presidentbeef/railroader/pull/878))

### Multiline Regex Validation

[Dmitrij Fedorenko](https://github.com/c0va23) added a change to support multiline extended regular expressions for model validations.

([changes](https://github.com/presidentbeef/railroader/pull/885))

### Class Methods

[Tim Wade](https://github.com/imtayadeway) fixed an issue where class methods and instance methods with the same name on the same class would overwrite each other. This may cause a few warning fingerprints to change, since all method names are now stored as symbols (some were strings before).

([changes](https://github.com/presidentbeef/railroader/pull/881))

### Force Scan

[Neil Matatall](https://github.com/oreoshake) added the `--force-scan` option to force Railroader to scan an application even if it doesn't look like a Rails app.

([changes](https://github.com/presidentbeef/railroader/pull/879))

### Branches in Templates

When looking at template output, Railroader will no longer treat the conditional as output, just the branches. This helps find more potential instances of cross-site scripting.

For example:

    <%= params[:x].html_safe unless this_is_a_bad_idea? %>

Now Railroader will just consider the `params[:x].html_safe` value which is clearly dangerous.

([changes](https://github.com/presidentbeef/railroader/pull/883/))

### More Safe Calls

Railroader can now handle more instances of the "safe call" or "lonely" operator such as `a&.b ||= 1` and `x&.y += z 1`.

([changes](https://github.com/presidentbeef/railroader/pull/887))

### Quoted Primary Key

Railroader will no longer warn about use of `quoted_primary_key` in SQL strings.

([changes](https://github.com/presidentbeef/railroader/pull/888))

### Delayed Load Path Modification

Railroader 3.3.0 started vendoring all its dependencies to avoid conflicts with application dependencies. However, if Railroader is included in a Gemfile without `require: false`, it will still modify the load path and potentially cause conflicts.

This version delays loading any dependencies until Railroader actually runs. This is almost like having `require: false` automatically.

Please keep in mind it is really not recommended to include Railroader in Gemfiles unless it is actually being used as a library. Otherwise it's like mixing your browser's dependencies with your applications. It doesn't make sense.

([changes](https://github.com/presidentbeef/railroader/pull/889))

### railroader-lib

For those who don't want Railroader to bundle and vendor its own dependencies, the [railroader-lib](https://rubygems.org/gems/railroader-lib) gem is identical to the `railroader` gem but without the bundling. Consider using it if the bundling and modified load paths are causing issues.

([changes](https://github.com/presidentbeef/railroader/commit/fa310a9b736d858a929715802d98b1a3f0887569))

### RailsConf Security Talks

[Justin Collins](https://github.com/presidentbeef) gave [a lightning talk](https://www.youtube.com/watch?v=DHHHnPwSY5I&feature=youtu.be&t=55m6s) about Railroader and [a regular talk](https://www.youtube.com/watch?v=3P9naxOfUC4&feature=youtu.be) about real-world examples of vulnerabilities Rails won't save you from.

[Mike Milner](https://twitter.com/secretmike) spoke about [the security breaches of 2015](https://youtu.be/UoiCylwUoq4).

[Jessica Rudder](https://twitter.com/JessRudder) talked through [examples of SQL injection](https://youtu.be/2GHWAYys1is) in ActiveRecord.

### SHAs

The SHA256 sums for this release are

    5c22721c8b486fa9d283cabf65c7e77b2f7428056d4d907b7f74a91dd112616a  railroader-3.3.1.gem
    7aa57ed8b42c0cadef09214f5544424659ab3972912137fad37da1a052d8a792  railroader-lib-3.3.1.gem
    95e68202493d8c504ad72276c8bfa46abb1c78c309bc2b80b433a6220f3722eb  railroader-min-3.3.1.gem

### Reporting Issues

Thank you to everyone who reported bugs and contributed improvements in this release.

Please report any [issues](https://github.com/presidentbeef/railroader/issues) with this release! Take a look at [this guide](https://github.com/presidentbeef/railroader/wiki/How-to-Report-a-Railroader-Issue) to reporting Railroader problems.

Also consider following [@railroader](https://twitter.com/railroader) on Twitter and hanging out [on Gitter](https://gitter.im/presidentbeef/railroader) for questions and discussion. Please note the mailing list is no longer in use and has apparently not been delivering mail for some time.

