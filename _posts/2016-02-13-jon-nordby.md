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
  - mypaint
  - gimp
  - geglbuffer
  - lgm
  - babl
  - pippin
  - hacks
  - goat
  - implementation
description: 'Already covered in the news from LGM was the release of GIMP 2.8, and that GIMP 2.10 will be fully GEGLified. The goat-invasion branch which has most of that work, the result of 3 weeks of pippin and mitch on a couch hacking together, has already landed in master.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:57.083Z'
dateModified: '2016-02-13T18:04:58.162Z'
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

Already covered in the news from LGM was the release of GIMP 2.8, and that [GIMP 2.10 will be fully GEGLified][0]. The goat-invasion branch which has most of that work, the result of 3 weeks of [pippin][1] and [mitch][2] on a couch hacking together, has already landed in master. This means that GIMP now has support for high bit-depth workflows for most operations. Finally.

### Putting the goat in MyPaint

During LGM I started working on using GEGL in MyPaint. I have already mentioned this idea [several][3][times][4], so it was time to stop talking and get hacking.

As a first step in making use of GEGL I wanted to replace the current surface implementation with one based on [GeglBuffer][5]. Since GeglBuffer already provides tiling, and can store any buffer data supported by Babl this turned out to be easy. Øyvind (pippin) added the semi-quirky pixel format we currently use\* in MyPaint to Babl, and I was able to get a rough working GEGL based Surface implementation the first evening.

\* RGBA premultiplied alpha, in 16 bit unsigned integers with 2^15 being the maximum value.

The next couple of days went to moving to the [GeglBufferIterator][6] API instead of gegl\_buffer\_{get,set} to have zero-copy access to improve performance, and improving GEGL and GEGL-GTK so that some of the hacks in the initial implementation could be removed.

Most of the work is in the [gegl branch][7] of MyPaint. A simple test application, mypaint-gegl.py, is included, and you can read [README.gegl][8] for how to try it out. Warning: only intended for curious developers at this stage.

A lots of work remains to be done for MyPaint to be able to fully use GEGL. The progress is tracked in two bugs, one for [MyPaint work][9] and one for [GEGL issues][10]. Because one cannot combine PyGObject with PyGTK, it will likely not be possible to fully integrate GEGL in MyPaint before [porting to PyGI and GTK+ 3][11].

Oh, in case the goat references are lost on you - check the [GEGL page on wikipedia][12].
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][13]

[0]: http://gimpfoo.de/2012/04/17/goat-invasion-in-gimp/
[1]: http://pippin.gimp.org/
[2]: http://gimpfoo.de/
[3]: http://river-valley.tv/mypaint-%E2%80%93-the-past-the-present-and-the-future/
[4]: http://libregraphicsworld.org/blog/entry/mypaint-1.0-there-can-never-be-too-much-awesomeness
[5]: http://www.gegl.org/api.html#GeglBuffer
[6]: http://gegl.org/api.html#GeglBufferIterator
[7]: https://gitorious.org/mypaint/mypaint/commits/gegl
[8]: https://gitorious.org/mypaint/mypaint/blobs/gegl/README.gegl
[9]: https://gna.org/bugs/index.php?19732
[10]: https://bugzilla.gnome.org/show_bug.cgi?id=675962
[11]: https://gna.org/bugs/?19230
[12]: http://en.wikipedia.org/wiki/GEGL
[13]: http://www.jonnor.com/wp/?flattrss_redirect&id=552&md5=763d4b0c65891b56d04551d30b2cd506