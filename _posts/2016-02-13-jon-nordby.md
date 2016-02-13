---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - graphs
  - imgflo
  - runtime
  - flowhub
  - gegl
  - gimp
  - server
  - image
  - processing
  - noflo
description: 'At TheGrid we are in need for a flexible service for doing server-side image processing. So after some discussion at LGM in Leipzig, I started writing one based on GEGL, the image processing library that will power the upcoming GIMP 2.10 release.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:12:00.421Z'
dateModified: '2016-02-13T18:04:36.790Z'
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

At [TheGrid][0] we are in need for a flexible service for doing server-side image processing. So after some discussion at [LGM in Leipzig][1], I started writing one based on [GEGL][2], the image processing library that will power the upcoming GIMP 2.10 release. The library provides a demand-driven graph-based API , with a ton of [operations included][3] and support for GPU processing using OpenCL.

### Runtime

For creating image processing pipelines for the server, [imgflo][4] acts as a runtime for [Flowhub][5], our [open source][6] visual programming IDE. It adds to the existing NoFlo browser, Node.js and [MicroFlo][7] microcontroller runtime targets, all possible thanks to the runtime-agnostic [protocol.][8]
[![](http://www.jonnor.com/wp/files/imgflo-caged-cassowary-light-1024x558.png)][9]

The preview is live and changes whenever changes are made to the graph. This allows to quickly experiment and develop new graphs.

### Server

As a server, imgflo provides a simple HTTP API where you specify the input image as an URL, the graph to process it through and any parameters exposed on that graph.

Processed images are cached, so that subsequent request on the same url just returns the image out of the cache.  
The git repository includes configuration and build setup for Heroku, so deploying an instance is a 5 minute job.

### Next

imgflo 0.1 is now minimally useful as image processing server, but there are many more [enhancements][10] on the todo list. Scalability and integration with NoFlo are two big topics, as as expanding the pool of available operations and graphs. [Porting filters from GIMP][11] to GEGL is a way of helping with the latter.

Additionally it would be interesting to provide a way of using imgflo with GIMP. First of all one could use graphs made with Flowhub via GEGL [meta-operations][12]. A more crazy idea is to [integrate directly][13], using Flowhub as a companion node-based editor.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][14]

[0]: http://thegrid.io/
[1]: http://libregraphicsmeeting.org/2014/
[2]: http://gegl.org/
[3]: http://gegl.org/operations.html
[4]: https://github.com/jonnor/imgflo
[5]: http://flowhub.io/
[6]: https://github.com/noflo/noflo-ui
[7]: http://www.jonnor.com/2013/11/microflo-0-2-0-visual-arduino-programming/
[8]: http://noflojs.org/documentation/protocol/
[9]: http://www.jonnor.com/wp/files/imgflo-caged-cassowary-light.png
[10]: https://github.com/jonnor/imgflo/issues?labels=enhancement
[11]: http://wiki.gimp.org/index.php/Hacking:Porting_filters_to_GEGL
[12]: https://github.com/jonnor/imgflo/issues/9
[13]: https://github.com/jonnor/imgflo/issues/10
[14]: http://www.jonnor.com/wp/?flattrss_redirect&id=690&md5=bc6a6ca7cb163bafb7b8236ce90bc18d