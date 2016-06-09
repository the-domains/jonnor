---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: >-
  http://www.jonnor.com/2011/05/geglfilter-gstreamer-element-for-manipulating-video-using-gegl/
inLanguage: en
keywords:
  - gegl
  - gstreamer
  - gimp
  - element
  - images
  - screenshot
  - framework
  - manipulated
  - video
  - processing
description: >-
  Gegl is an image processing framework used in projects like Gimp and
  DarkTable. It will eventually allow Gimp to allow non-destructive, high
  bit-depth image processing, among other things. And GStreamer is  the
  multimedia framework for GNU/Linux, handling video/audio/other
  playback/recording/manipulation on your favorite
  desktop/server/mobile/embedded system.
datePublished: '2016-06-09T16:16:38.946Z'
dateModified: '2016-06-09T16:16:34.300Z'
author: []
related: []
app_links: []
title: 'geglfilter: GStreamer element for manipulating video using Gegl'
sourcePath: _posts/2016-02-13-jon-nordby.md
authors: []
publisher:
  name: Jonnor
  domain: www.jonnor.com
  url: 'http://www.jonnor.com'
  favicon: null
starred: false
_context: 'http://schema.org'
_type: Article

---
# geglfilter: GStreamer element for manipulating video using Gegl

[Gegl][0] is an image processing framework used in projects like Gimp and DarkTable. It will eventually allow Gimp to allow non-destructive, high bit-depth image processing, among other things. And [GStreamer][1] is _the_ multimedia framework for GNU/Linux, handling video/audio/other playback/recording/manipulation on your favorite desktop/server/mobile/embedded system.

After writing the [C][2][airo overlay GStreamer element][2], I implement a basic GStreamer element which allows you to apply a filter to video in a GStreamer pipeline using Gegl. Using this element, video editing/manipulation applications like [Pitivi][3] could allow users to apply effects provided by Gegl to videos. Gegl is a very powerful image processing framework, and already has [a significant number of image processing operations][4]. More operations is expected, especially from the port the tools, filters and plugins used in Gimp to Gegl.

Here are some screenshots showing the standard GStreamer video test data being manipulated in different ways using Gegl. Note: the size of the images are only different because the output windows had different sizes when I took the screenshot.

[A bug has been filed for inclusion][5] of this element into gst-plugins-good. The patch attached there also contains an example application, showing how to use the element.

In the patches you will find an example.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][6]

[0]: http://www.jonnor.com/2011/05/geglfilter-gstreamer-element-for-manipulating-video-using-gegl/www.gegl.org
[1]: http://gstreamer.freedesktop.org/
[2]: http://www.jonnor.com/2011/03/cairooverlay-generic-cairo-overlay-element-for-gstreamer/
[3]: http://www.pitivi.org/
[4]: http://www.gegl.org/operations.html
[5]: https://bugzilla.gnome.org/show_bug.cgi?id=650750
[6]: http://www.jonnor.com/wp/?flattrss_redirect&id=381&md5=70db982ae462366ffab84c644c3e3a81