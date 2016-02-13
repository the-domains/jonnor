---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - mypaint
  - tile
  - brush
  - dab
  - speedups
  - backend
  - gegl
  - multi-threading
  - drawing
  - performance
description: 'A first set of performance improvements for the brush engine has just landed in MyPaint master. The goals for this work for me were, in priority: a) Making sure that moving to a GEGL backend in MyPaint does not reduce performance, b) Improve performance when integrating the MyPaint brush engine in other applications, and lastly c) Improving the performance in MyPaint itself.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:58.922Z'
dateModified: '2016-02-13T18:04:52.218Z'
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

A first set of performance improvements for the brush engine has just landed in MyPaint master. The goals for this work for me were, in priority: a) Making sure that moving to [a GEGL backend in MyPaint][0] does not reduce performance, b) Improve performance when integrating the MyPaint brush engine in other applications, and lastly c) Improving the performance in MyPaint itself.
_TL;DR: \* Users of the soon-to-be-released MyPaint 1.1 should experience about 15% faster drawing of strokes for medium to big brushes. \* _Switching to the GEGL based backed for MyPaint 1.2 is now both feasible and highly desirable from a performance perspective.__

### Optimizations

The optimizations are implemented through three complimentary strategies:

All dab drawing operations that happen as a result of a motion update event are queued up. When the brush engine has calculated where all dabs should go, tiles are fetched, all dabs drawn and the tiles updated. This in contrast to before where each dab drawing operation would fetch and update tiles.

The tiles to be processed are divided evenly between processing threads (one per core). Each tile is processed completely independent of other tiles, so there is no locking or synchronization in the drawing code. The tile backing store must naturally be thread-safe and may ensure this using locks.

Within each tile we attempt to make use of auto-vectorization to create the brush dab mask and do the composition of the dab onto the tile. Currently this is only implemented for a part of the mask calculation.

### Results

Details of the results and how they can be reproduced is found in the [original email thread][1].

Starting with the lowest priority goal, but the most relevant to users; performance impact on MyPaint right now.

In terms of raw speed of drawing brushes to onto the underlying surface, speedups range from 20% to 50% for larger brushes (16 px+). This sets an upper boundary for the speedup perceived by the user.

Looking at the UI-enabled benchmarks of MyPaint, which is doing everything a normal application instance does, including layer compositing and rendering to screen, around 15% speedup was observed. As the UI benchmark only tests a single brush at size=8.0px, it is possible that larger brushes will a higher speedup.
_Users of the soon-to-be-released MyPaint 1.1 should experience about 15% faster drawing of strokes for medium to big brushes._

Note that the backend in use does not make use of the multi-threading introduced by (2) due to the tile store not being thread-safe and that it already had a cache to mitigate the problem fixed by (1).  
Note

So in terms of raw surface rendering speed, the GEGL based backend is now significantly faster than the Python-based one. With 1 and 2 threads it is respectively up to 25% and 100% faster for big brush sizes. With 6 threads, it can be up to 4 times faster.

_Switching to the GEGL based backed for MyPaint 1.2 is now both feasible and highly desirable from a performance perspective_.

Note that to see UI performance increases approaching the raw surface drawing performance increase we may also need to do the layer compositing multi-threaded.

I'm trying to convince the Krita guys to update to the new version and to provide some feedback on the impact. Other consumers of the MyPaint brush engine do not tend to communicate much with us (some are proprietary).  
I have strong hopes that (1) should increase their performance radically as their tile get/set cost is significantly higher than in the MyPaint case: They need to convert between the internal Krita and the MyPaint brush engine working colorspace each time. They may also be able to enable multi-threading and see speedups similar to the GEGL-based backend as a result.

### Future Work

This is only lays the groundwork of better optimized MyPaint brush engine, many areas have room for improvement. For one only a small subset of the heavy code is vectorized. There may be inner loops that can be tweaked. It may be that, with a different tile access pattern compared to before, a different tile size would be more ideal. Perhaps doing the expensive calculation of the brush dab could be avoided some times by caching them... Thinking bigger, one could move all the drawing (and rendering) to the GPU.

More details on these ideas can be found [here][2]. If you are interested in working on any of it, get in touch and start hacking!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][3]

[0]: http://www.jonnor.com/2012/05/mypaint-and-goats-at-lgm2012/
[1]: https://mail.gna.org/public/mypaint-discuss/2012-11/msg00003.html
[2]: http://gitorious.org/mypaint/mypaint/blobs/HEAD/brushlib/PERFORMANCE
[3]: http://www.jonnor.com/wp/?flattrss_redirect&id=625&md5=4c48876747aa6ba46ea6ebb563a2da1f