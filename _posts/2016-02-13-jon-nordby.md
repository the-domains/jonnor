---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - gegl
  - gtk
  - graph
  - display
  - application
  - gegl-qt
  - gegl-gtk
  - library
  - operation
  - using
description: "So, in the last couple of months I've been working a bit on GEGL. Some of the work has already been covered by LWN, so I guess it is time that I blog about it... GEGL is a generic image processing library which is used by applications like GIMP, (and in the future maybe MyPaint and DarkTable)."
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:57.318Z'
dateModified: '2016-02-13T18:05:00.687Z'
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

So, in the last couple of months I've been working a bit on [GEGL][0]. Some of the work has already been [covered by LWN][1], so I guess it is time that I blog about it...

GEGL is a generic image processing library which is used by applications like [GIMP][2], (and in the future maybe [MyPaint][3] and [DarkTable][4]). It provides applications with a graph based image processing backend that can do non-destructive processing of high-bitdepth images, among other things.

One of the problems that I think has been limiting adaptation of GEGL has been the entry barrier to starting to use it in a graphical application. While GEGL provides the image processing backend, it did not provide good and easy ways of displaying the output on screen. Now it does!

### GTK+, Clutter and Qt integration libraries

Some code for integrating GEGL in GTK+ based applications has existed in the GEGL tree for a long time, but it was not well maintained and there was no public API. After brushing up the code to use Cairo for rendering and to support both GTK+ 2 and 3, it was split out to a separate library and repository: [gegl-gtk][5]. This library now provides a GtkWidget for displaying the output of a node in the GEGL graph, with basic support for scaling and translations. Any change in the GEGL graph will be reflected in the view widget. This makes it trivial for applications using a GTK+ based user interface to get started using GEGL, see for instance the provided examples [in C][6] or [in Python][7].

The same functionality is provided for Clutter based user interfaces by [gegl-clutter][8] in form of a ClutterActor. This code was previously available as [clutter-gegl][9], but has now been renamed and moved to be a part of the GEGL project, and is maintained by [Øyvind Kolsås][10]. [Example code][11] in C.

Last but not least, [gegl-qt][12] was created to serve the needs of applications using Qt based user interfaces. The different widget systems (QWidget-, QGraphicsWidget- and QML-based) are all supported. In addition to the features currently available in the GTK+ and Clutter versions, the Qt view widgets also support auto-scaling and auto-centering. Python bindings via PySide is planned, but blocking on a [PySide issue][13] at the moment.

A pretty boring screenshot showing two QWidget based examples (code: [1][14], [2][15]) for transformations:
[![](http://www.jonnor.com/wp/files/2011-08-21-192538_1280x800_scrot_cropped-300x198.png)][16]

Artwork: " [Wanted][17]", speedpainting by [David Revoy][18]

The first stable release of gegl-qt and gegl-gtk will hopefully be available soon. The list of tasks can be found [in the README][19][files][20].

### Display operations

In GEGL, image processing is described as a graph of operations. "gegl:display" and "gegl:gtk-display" operations existed in the gegl tree, and by attaching one of these to a node in the graph one could display the output of the graph at the given node in a window . Such display operations are useful for applications that just want to show the output of a graph without having to use a GUI library directly.

The problem was that both of these operations were optional, so applications could not rely on this functionality to be present. This is solved by letting the "gegl:display" operation be a meta-operation, which uses other operations as a handler to actually display the output. Such display handler operations are now provided by gegl (optional, using SDL), gegl-gtk (using GTK+) and gegl-qt (using Qt). In addition a fallback operation that will export a PNG file and launch an external application to display it will be provided in GEGL.

More to GEGL stuff to come soon, hopefully.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][21]

[0]: http://www.gegl.org/
[1]: http://lwn.net/Articles/451417/
[2]: http://www.gimp.org/
[3]: http://www.mypaint.org/
[4]: http://darktable.sourceforge.net/
[5]: http://git.gnome.org/browse/gegl-gtk
[6]: http://git.gnome.org/browse/gegl-gtk/tree/examples/gegl-gtk-basic.c
[7]: http://git.gnome.org/browse/gegl-gtk/tree/examples/gegl-gtk-python.py
[8]: http://git.gnome.org/browse/gegl-clutter
[9]: http://git.clutter-project.org/cgit.cgi?url=clutter-gegl
[10]: http://pippin.gimp.org/
[11]: http://git.gnome.org/browse/gegl-clutter/tree/examples/parsexml.c
[12]: http://git.gnome.org/browse/gegl-qt/
[13]: http://lists.pyside.org/pipermail/pyside/2011-August/002785.html
[14]: http://git.gnome.org/browse/gegl-qt/tree/examples/qwidget-transformations
[15]: http://git.gnome.org/browse/gegl-qt/tree/examples/qwidget-autotransform
[16]: http://www.jonnor.com/wp/files/2011-08-21-192538_1280x800_scrot_cropped.png
[17]: http://mypaint.deviantart.com/#/d3urag0
[18]: http://www.davidrevoy.com/
[19]: http://git.gnome.org/browse/gegl-qt/tree/README.txt#n62
[20]: http://git.gnome.org/browse/gegl-gtk/tree/README
[21]: http://www.jonnor.com/wp/?flattrss_redirect&id=442&md5=14ca04429b25a21a9512d0566aceb144