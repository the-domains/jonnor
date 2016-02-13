---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2015/01/imgflo-0-3/'
inLanguage: en
starred: false
keywords:
  - imgflo
  - gegl
  - flowhub
  - runtimes
  - gimp
  - operations
  - load
  - image
  - workflow
  - vilson
description: 'Time for a new release of imgflo, the image processing server and dataflow runtime based on GEGL. This iteration has been mostly focused on ironing out various workflow issues, including documentation. Primarily so that the creatives in our team can be productive in developing new image filters/processing.'
datePublished: '2016-02-13T20:36:00.586Z'
dateModified: '2016-02-13T19:44:28.538Z'
author: []
related: []
app_links: []
title: 'imgflo 0.3: GEGL metaoperations++'
sourcePath: _posts/2016-02-13-jon-nordby.md
published: true
authors: []
publisher:
  name: Jonnor
  domain: www.jonnor.com
  url: 'http://www.jonnor.com'
  favicon: null
_context: 'http://schema.org'
_type: Article

---
# imgflo 0.3: GEGL metaoperations++

Time for a new release of [imgflo][0], the image processing [server][1] and dataflow [runtime][2] based on GEGL. This iteration has been mostly focused on ironing out various workflow issues, including documentation. Primarily so that the creatives in our team can be productive in developing new image filters/processing. Eventually this will also be an extension point for third parties on [our platform][3].

By porting the png and jpeg loading operations in GEGL to [GIO][4], we've added support for loading images into imgflo over HTTP or dataURLs. The latter enables opening local file through a file selector in Flowhub. Eventually we'd like to also support [picking from web services][5].

Another big feature is allowing to live-code new GEGL operations (in C) and load them. This works by sending the code over to the runtime, which then compiles it into a new .so file and loads it. Newly instatiated operations then uses that revision of code. We currently do not change the active operation of currently running instances, though [we could][6].  
Operations are never unloaded, due both to a glib limitation and the general trickyness of guaranteeing this to be safe for native code. This is not a big deal as this is a development-only feature, and the memory growth is slow.

imgflo now supports showing the data going through edges, which is very useful to understand how a particular graph works.

Using Heroku one can [get started][7] without installing anything locally. Eventually we might have installers for common OS'es as well.

[Vilson Viera][8] added a set of new image filters to the server, inspired by Instagram. Vilson is also working on our image analytics pipeline, the other piece required for intelligent automatic- and semi-automatic image processing.
[![](http://www.jonnor.com/wp/files/imgflo-instagram-filters-258x300.jpg)][9]

GEGL has for a long time supported meta-operations: operations which are built as a sub-graph of other operations. However, they had to be built programatically using the C API which limited tooling support and the platform-specific nature made them hard to distribute.  
Now GEGL can load such operations from the [JSON format][10] also used by imgflo (and [several][11][other][12][runtimes][13]). This lets one use operations built with Flowhub+imgflo in GIMP:
[![](http://www.jonnor.com/wp/files/imgflo-gimp-anim-640.gif)][14]

This makes Flowhub+imgflo a useful tool also outside the web-based processing workflow it is primarily built for. Feature is available in GEGL and GIMP master as of [last week][15], and will be released in GIMP 2.10 / GEGL 0.3\.

Next iteration will be primarily about scaling out. Both allowing multiple "apps" (including individual access to graphs and usage monitoring/quotas) served from a single service, and scaling performance horizontally. The latter will be critical when the ~20k+ users who have [signed up][16] start coming onboard.  
If you have an interest in using our hosted imgflo service outside of The Grid, get in contact.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][17]

[0]: http://imgflo.org/
[1]: http://github.com/jonnor/imgflo-server
[2]: http://github.com/jonnor/imgflo
[3]: https://thegrid.io/
[4]: https://developer.gnome.org/gio/stable/
[5]: https://github.com/jonnor/imgflo/issues/28
[6]: https://github.com/jonnor/imgflo/issues/82
[7]: http://docs.flowhub.io/getting-started-imgflo/
[8]: http://automata.cc/
[9]: http://www.jonnor.com/wp/files/imgflo-instagram-filters.jpg
[10]: http://noflojs.org/documentation/json/
[11]: http://noflojs.org/
[12]: https://github.com/jonnor/javafbp-runtime
[13]: http://microflo.org/
[14]: http://www.jonnor.com/wp/files/imgflo-gimp-anim-640.gif
[15]: https://git.gnome.org/browse/gegl/commit/?id=564f45bad76eb0f888e628ea70345912dd68cbbb
[16]: http://thegrid.io/
[17]: http://www.jonnor.com/wp/?flattrss_redirect&id=798&md5=9145cdc5f635e57c69ccbd8f2096ed61