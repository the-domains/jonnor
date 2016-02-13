---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2010/11/image-preview-support-for-openraster-in-qt-working/'
inLanguage: en
starred: false
keywords:
  - libora
  - openraster
  - plug-in
  - kde
  - qimage
  - readme
  - gitorious
  - applications
  - document
  - rendering
description: "While learning Qt here at Openismus I've written a basic, working plug-in for Qt that adds support for the OpenRaster file format*."
datePublished: '2016-02-13T20:29:23.439Z'
dateModified: '2016-02-13T19:55:19.236Z'
author: []
related: []
app_links: []
title: Image preview support for OpenRaster in Qt working
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
# Image preview support for OpenRaster in Qt working

While learning Qt here at Openismus I've written a basic, working plug-in for Qt that adds support for the [OpenRaster][0] file format\*. Here is my Qt-based test application demoing this functionality by showing some awesome multi-layered abstract test art made by yours truly using Krita:

The level of features supported is such that you will be able to preview OpenRaster documents created with applications like MyPaint, Drawpile, Nathive and GIMP, with the limitation that it will have a white background for transparent areas. The code can be found in [qopenraster repository][1] on gitorious (no tarballs), and the README file documents how to install as well as things that remain to be done.

The plug-in is basically a thin wrapper around [libora][2], the OpenRaster [reference library][3]. libora takes care of parsing the OpenRaster document, reading out the layer data and rendering it into a single buffer. The rendering ability was added by me as part of this work, in addition to some other minor stuff. The Qt plug-in does RGBA to ARGB conversion and provides the QImageIOPlugin interface expected by Qt.

Doing this has also exposed several limitations and not-so-nice things in libora that should/needs to be improved. I've updated libora's [README][4] file to reflect this.
_\*Assuming the Qt application actually uses QImage in a straight-forward way. The KDE image viewer Gwenview does not seem to use QImage directly, so you will not automatically get support there by installing the plug-in :((. I fear that other KDE applications might be the same, though I was not able to test Digikam. If anyone has a suggestion for a Qt based image viewer that works sanely in this area, don't hesitate to leave a comment._

PS: I have an almost-working gdk-pixbuf module as well, will push that to gitorious soon.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][5]

[0]: http://create.freedesktop.org/wiki/OpenRaster
[1]: http://gitorious.org/openraster/qopenraster
[2]: http://gitorious.org/openraster/libora
[3]: http://create.freedesktop.org/wiki/OpenRaster/Reference_Library
[4]: http://gitorious.org/openraster/libora/blobs/master/README
[5]: http://www.jonnor.com/wp/?flattrss_redirect&id=306&md5=dcb6ecfb85b8906a64b9985ff7eca170