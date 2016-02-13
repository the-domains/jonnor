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
  - windows
  - plugins
  - input
  - build
  - method
  - development
  - enable
  - todo-list
  - application-hosted
description: 'Enabling third-party developers of input methods is one of the primary goals in the Maliit project. In an attempt to improve this story I spent some time on getting Maliit to work on Windows. Since we use Qt there were few changes needed to the code, but since we use qmake, quite many to the build system.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:13:25.266Z'
dateModified: '2016-02-13T18:05:32.821Z'
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

Enabling third-party developers of input methods is one of the primary goals in the Maliit project. In an attempt to improve this story I spent some time on getting Maliit to work on Windows.

Since we use Qt there were few changes needed to the code, but since we use qmake, quite many to the build system. One of the bigger changes was making glib-dbus and qdbus optional, which is also useful for Maliit on embedded systems.

With the Windows build fixes merge requests [for maliit-framework][0] and [for maliit-plugins][1], one can now [build Maliit on Windows][2] and run the provided example applications. This feature is currently being reviewed and should be in the next Maliit release.
[![](http://www.jonnor.com/wp/files/2012-03-13-155530_2704x1050_scrot_crop-300x225.png)][3]

Thanks to the standalone viewer application for Maliit Keyboard this allows one to develop new features, theming and language layouts for it on Windows.

Sadly loading an input method plugin in the maliit server crashes for an [unknown reason][4]. With my limited Windows software development experience I was not able to solve this within the couple of days I had available. This is necessary for application-hosted Maliit to work and to enable general development of Maliit input method plugins (not just maliit-keyboard). Help would be much appreciated, even just someone checking if it is reproducible on another Windows system.

Also [left on the todo-list][5] due to lack of time is to set up a Windows build slave for [the Maliit buildbot][6], to test that the build continues to work on Windows and to produce executables.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][7]

[0]: https://gitorious.org/maliit/maliit-framework/merge_requests/165
[1]: https://gitorious.org/maliit/maliit-plugins/merge_requests/50
[2]: https://wiki.maliit.org/Documentation/Installing#From_source_code_.28Windows.29
[3]: http://www.jonnor.com/wp/files/2012-03-13-155530_2704x1050_scrot_crop.png
[4]: https://bugs.maliit.org/show_bug.cgi?id=111
[5]: https://bugs.maliit.org/show_bug.cgi?id=112
[6]: http://www.jonnor.com/2011/12/the-maliit-buildbot/
[7]: http://www.jonnor.com/wp/?flattrss_redirect&id=538&md5=d85622fb2dd3b4c95db3480c57b19d0c