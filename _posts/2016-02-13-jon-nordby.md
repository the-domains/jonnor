---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2011/03/cairooverlay-generic-cairo-overlay-element-for-gstreamer/'
inLanguage: en
starred: false
keywords:
  - gstreamer
  - drawing
  - gst-plugins-good
  - cairo
  - signal
  - stream
  - caps-updated
  - video
  - bugreports
  - vala
description: 'I wrote the initial version of this in late January, and after some interations it was merged yesterday to gst-plugins-good, and will be in gst-plugins-good 0.10.33. This solves the feature request I filed in 2009, one of my oldest bugreports in bugs.gnome.org!'
datePublished: '2016-02-17T20:44:03.260Z'
dateModified: '2016-02-17T20:43:54.398Z'
author: []
related: []
app_links: []
title: 'cairooverlay: Generic Cairo overlay element for GStreamer'
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
# cairooverlay: Generic Cairo overlay element for GStreamer

I wrote the initial version of this in late January, and after some interations it was [merged yesterday][0] to gst-plugins-good, and will be in gst-plugins-good 0.10.33\. This solves the [feature request][1] I filed in 2009, one of my oldest bugreports in bugs.gnome.org!

### What does it do?

cairooverlay allows you to draw arbitrary things on top of a video stream in GStreamer using Cairo. Previously you had to create a custom GStreamer element for that (in C/Vala), but now you can just hook up to some signals, using any programming language with GStreamer/Cairo bindings.

To draw an overlay using this element, you use the "caps-updated" signal to get information about the video stream (like width and height) and the "draw" signal to do the actual drawing. In addition to the Cairo context, the draw signal passes you the timestamp and duration of the buffer, so you can also do animations.

For more info see the included [example application][2] or the [documentation][3] (should be updated soon). Here is the obligatory screenshot showing the example application drawing a heart onto a test videostream:
[![](http://www.jonnor.com/wp/files/2011-03-03-192343_1280x800_scrot_cropped-300x295.png)][4]

The heart is actually animated, so I guess I should have had a video. But you'll just have to trust me that it is very cute, or grab the code yourself!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][5]

[0]: http://cgit.freedesktop.org/gstreamer/gst-plugins-good/commit/?id=32dff9df75942c51b3ecbd7ffa394ef755881d50
[1]: https://bugzilla.gnome.org/show_bug.cgi?id=595520
[2]: http://cgit.freedesktop.org/gstreamer/gst-plugins-good/tree/tests/examples/cairo/cairo_overlay.c
[3]: http://gstreamer.freedesktop.org/data/doc/gstreamer/head/gst-plugins-good-plugins/html/
[4]: http://www.jonnor.com/wp/files/2011-03-03-192343_1280x800_scrot_cropped.png
[5]: http://www.jonnor.com/wp/?flattrss_redirect&id=371&md5=0a98aab4c045419184024eab3c5d18c3