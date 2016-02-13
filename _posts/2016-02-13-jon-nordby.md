---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - maliit
  - build-bot
  - automating
  - variations
  - testing
  - instance
  - build
  - etc
  - meta-builds
  - components
description: 'After having set up the typical things open source projects needs like a website/wiki, mailing-list and bug-tracker, Maliit now also has something not so common: a build-bot. As Maliit consists of several components that can be built in several different ways (and for several different platforms), we wanted to automate the build and tests of the different variations to ensure that we do not break any of them.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:13:25.202Z'
dateModified: '2016-02-13T18:05:32.810Z'
sourcePath: _posts/2016-02-13-jon-nordby.md
published: true
inFeed: true
hasPage: true
inNav: false
url: jon-nordby/index.html
_context: 'http://schema.org'
_type: Article

---
# Jon Nordby

After having set up the typical things open source projects needs like a website/wiki, mailing-list and bug-tracker, [Maliit][0] now also has something not so common: [a build-bot][1].

As Maliit consists of several components that can be built in several different ways (and for several different platforms), we wanted to automate the build and tests of the different variations to ensure that we do not break any of them. This is especially important for variations which are not easy to test for the individual developers, like for instance [Maliit on Qt 5][2].

The software chosen to help with this task was [Buildbot][3]. Getting an initial instance it up and running was very quick and pain-free, especially thanks to packages being easily available and the [excellent documentation][4]. The current setup now builds, tests and installs the two major components we have: Maliit Framework and Maliit (Reference) Plugins, in the most important build/config variations we have. A total of 12 individual build jobs, plus 2 meta-builds. The configuration for the instance can be found in the [maliit-buildbot-configuration][5] repository.

For security reasons the build-bot is not directly exposed to the Internet. Instead a script runs every 5 minutes to generate a static HTML website and publish on the public web-server: [Maliit build-bot][1]

This gives us a minimal continuous integration system for Maliit, which for now will hopefully helps us avoid breakage. In the future, the usage of the build-bot might extend to include:

* Automating [the release process][6]
* Testing of merge-requests/patches before merging to master
* Automated integration/system testing, complementing the unit-tests
* Triggering external builders for packaging. OpenSUSE OBS, Maemo 5 Garage, etc.
* Automating certain aspects of bug-lifetime. Resolving when fix is committed, closing on release if pre-verified, etc
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][7]

[0]: http://www.maliit.org/
[1]: http://maliit.jonnor.com/buildbot
[2]: http://blog.jpetersen.org/2011/12/07/maliit-and-qt5/
[3]: http://trac.buildbot.net/
[4]: http://buildbot.net/buildbot/docs/current/full.html
[5]: https://gitorious.org/maliit/maliit-buildbot-configuration
[6]: https://wiki.maliit.org/Development/Making_Releases
[7]: http://www.jonnor.com/wp/?flattrss_redirect&id=518&md5=61c2d50ad1e71f7e3d5128ee1c338cde