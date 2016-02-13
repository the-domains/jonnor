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
  - piksel
  - applications
  - libre
  - graphics
  - lgru
  - vector
  - workshop
  - interoperability
description: 'Last week I was so lucky as to attend the 3rd Libre Graphics Research Unit ( LGRU) meeting in beautiful Bergen, Norway. The meeting was titled Piksels and Lines and had "a particular focus on improvements, interoperability between and fringe use of F/LOSS graphic bitmap and vector software, as well as generative software used in performative contexts."'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:13:25.273Z'
dateModified: '2016-02-13T18:05:30.077Z'
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

Last week I was so lucky as to attend the 3rd Libre Graphics Research Unit ( [LGRU][0]) meeting in [beautiful Bergen][1], Norway.

The meeting was titled [_Piksels and Lines_][2] and had "a particular focus on improvements, interoperability between and fringe use of F/LOSS graphic bitmap and vector software, as well as generative software used in performative contexts."

The meeting was structured into three different areas: Seminar, Workshop and Performance.

### Seminar

The attendants that were invited for the meeting each did a presentation of their choosing. They were recorded and are available in the [online archive][3] of the seminar. The video quality leaves something to be desired, but the audio is generally good.

The presentations I found particularly interesting were:

I gave a presentation titled _MyPaint and cross-application workflows_. It was an introduction to MyPaint as a creative tool, how it combines raster and vector (piksels and lines) concepts, and my perspective on interoperability between libre graphics applications.
[![](http://www.jonnor.com/wp/files/2012-06-11-142050_1280x1600_scrot_crop.png)][4]

### Workshop
[![](http://www.jonnor.com/wp/files/P1050978_medium-300x225.jpg)][5]

I had hoped to hack some code for one of my existing ideas during the workshops. That did not happen. Instead I ended up hacking specifications. Maybe that is just as good. Hacking one can always do later, hashing out and documenting ideas has to be done while it is fresh.

First the results of some discussions with Øyvind Kolås, the [GEGL][6] maintainer:

**A journal for GEGL**: transaction log over changes made to a GEGL graph. [Specification][7]. [Discussion][8]. This feature would allow for applications based on GEGL to:

* Implement non-linear histories (undo/redo), and a timeline of the changes
* Store the history in a document like OpenRaster
* Share the history between different applications
* Let multiple applications to work on the same document at the same time

**A strategy for improved file format support in GEGL**, and using this to improve file support and interoperability in libre graphics applications. [Proposed plan][9].

Executing this plan would move a lot of the existing file format support from GIMP (PSD, XCF, OpenRaster) down into GEGL so that it can be reused across applications. And would then let GEGL provide image support plugins for GdkPixbuf and QImage - so that at the very least - previews will work _everywhere_.

Chatting with Egil Möller, creator of Sketchspace, also resulted in:

**A web based system supporting a continuous work-flow from free-hand**  
**sketch to finished product**. [Concept and mockups][10]

"Imagine starting from a freehand drawing or imported raster image and _gradually_ refining this into a technical document with illustrations, UML-diagrams or even running code or a 3d model."

Refining here means that the user guides the tool to transform freehand sketch into vector paths, then into vector shapes, then into something domain-specific and formal like UML - by adding additional data like annotations, strengthening of lines to "disambiguating" the transformation.

Needless to say, this is more a visionary thing. Realizing this would involve finding good solutions to a fair amount of computer vision problems.

**Making GEGL available for use in web-based applications**. [Proposal][11].

More on the concrete side: allow GEGL to be used in interactive or batch-oriented web applications, or in native applications based on web technologies (Javascript, HTML5 user interfaces).

Some of the discussions also resulted in me writing down the [strategy for GEGL integration in MyPaint][12] and the related ideas/plans for how to [improve the performance][13] of the MyPaint brush engine.

Now we just need to implement all the stuff... Contributions welcomed!

### Performance

Since [Piksel][14], with a long history in generative performance arts, was the hosting organization it was not surprising a project in that area materialized.

A workshop session hosted by media artist [Brendan Howell][15] called _Demonstrating the Unexpected _came up with the idea of the _Piksels & Lines Orchestra (PLO)_: think of the collaborative use of our traditional libre graphics software as an orchestra. The applications, from MyPaint to Scribus, are instruments; the people using them players; a performance the use of these instruments. Can we create an experience for an audience based on this framework? How would it sound? How would it look?

Having plenty of code-crafting people available, the next afternoon it was decided to spend a couple of hours realizing a prototype. The [LGRU blog has the details][16]. We recorded video of our initial performances with this prototype as well, but that has sadly not made it online yet...

### Thanks!

Thanks a lot to Piksel and LGRU for sponsoring my attendance, and the EU Culture Programme and Bergen municipality for funding activities that support libre graphics and free culture!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][17]

[0]: http://lgru.net/
[1]: http://www.flickr.com/search/?q=bergen&f=hp
[2]: http://www.piksel.no/pulse/lgru
[3]: http://piksel.no/dmmdb/index.php?channel=PikselLines
[4]: http://piksel.no/dmmdb//contents/piksellines420120706-102121-b-dl.ogg
[5]: http://www.jonnor.com/wp/files/P1050978_medium.jpeg
[6]: http://gegl.org/
[7]: http://git.gnome.org/browse/gegl/tree/docs/journal.txt
[8]: https://mail.gnome.org/archives/gegl-developer-list/2012-June/msg00004.html
[9]: https://mail.gnome.org/archives/gegl-developer-list/2012-June/msg00003.html
[10]: http://beta.primarypad.com/p/sketchspaced
[11]: https://mail.gnome.org/archives/gegl-developer-list/2012-June/msg00010.html
[12]: https://gitorious.org/mypaint/mypaint/blobs/HEAD/README.gegl#line45
[13]: https://gitorious.org/mypaint/mypaint/blobs/HEAD/brushlib/PERFORMANCE
[14]: http://www.jonnor.com/2012/06/piksels-and-lines-libre-graphics-research-unit-seminar-in-bergen/www.piksel.no
[15]: http://www.wintermute.org/brendan/
[16]: http://blogs.lgru.net/ft/theme/piksels-and-lines/turning-tools-into-instruments
[17]: http://www.jonnor.com/wp/?flattrss_redirect&id=565&md5=cc7cd2464e8fda6acaf0406d61b740d0