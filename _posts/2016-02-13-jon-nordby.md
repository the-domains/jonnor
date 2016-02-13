---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - pygtk
  - mypaint
  - meego
  - netbook
  - ideapad
  - pixbufs
  - numeric
  - buut
  - numpy
  - obs
description: 'When I got back from the Meego conference, I tried building MyPaint on the Ideapad I got (which runs Meego Netbook 1.1). I was pleasantly surprised to find pygtk in the core repositories. numpy on the other hand was missing but that was easy to build from source.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:56.087Z'
dateModified: '2016-02-13T18:05:13.618Z'
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

When I got back from the Meego conference, I tried building [MyPaint][0] on the Ideapad I got (which runs Meego Netbook 1.1).

I was pleasantly surprised to find pygtk in the core repositories. numpy on the other hand was missing but that was easy to build from source. Buut, it seems that pygtk is built without numeric support, making MyPaint unusable; numeric support is used to get access to the pixels in pygtk pixbufs, which we need for several central things.  
I have of course [filed a bug][1] for this so hopefully it will be resolved soon. If not I will have to provide alternative pygtk packages using the community OBS. In any case, expect it to be working soon.

I also hope to adapt MyPaint's UI to the handset and netbook/tablet form factor, but this is only talk so far.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][2]

[0]: http://www.mypaint.info/
[1]: http://bugs.meego.com/show_bug.cgi?id=10195
[2]: http://www.jonnor.com/wp/?flattrss_redirect&id=325&md5=7ba79cb8c9f62180b864ebf4412d9b5d