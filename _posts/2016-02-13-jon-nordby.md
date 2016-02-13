---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2010/02/mypaint-openraster-et-c-update/'
inLanguage: en
starred: false
keywords:
  - mypaint
  - gimp
  - openraster
  - krita
  - pledgie
  - plug-in
  - document
  - installer
  - 27th
  - hoping
description: I managed to the GIMP OpenRaster plug-in into mainline GIMP. This means that GIMP 2.7.1 and forward will have rudimentary saving and loading support out-of-the-box. Users of GIMP 2.6 or 2.7.0 can download and install the plug-in from here. Luka Čehovin started work on a reference library (libora) for OpenRaster.
datePublished: '2016-02-13T18:30:18.476Z'
dateModified: '2016-02-13T18:29:44.246Z'
author: []
related: []
app_links: []
title: 'Mypaint, OpenRaster, etc. update'
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
### Mypaint, OpenRaster, etc. update

## OpenRaster

I managed to the GIMP OpenRaster plug-in into mainline GIMP. This means that GIMP 2.7.1 and forward will have rudimentary saving and loading support out-of-the-box. Users of GIMP 2.6 or 2.7.0 can download and install the plug-in from [here][0].

[Luka Čehovin][1] started work on a [reference library (libora)][2] for OpenRaster. Hopefully this will, along the way, make it easier to provide OpenRaster support in applications. Perhaps it can also help solve some performance issues we currently have in MyPaint when saving large images.

## MyPaint

In late January we [released MyPaint 0.8.0][3]. The release was delayed a couple of months from the initial planning, and we did not get to integrate as much as we'd like from external git branches, but it was about time to get the changes we do have out in a stable version. It was very nice to have a Windows installer ready from day 1, and that we were able to translate it into 12 languages! This weekend we also [released MyPaint 0.8.1][4], which fixed a nasty memory leak and some minor issues. No Windows installer or DEBs yet tho.

Just recently, MyPaint has also been [successfully built and run on Mac OSX][5], pressure sensitivity and all. Hopefully we can make it solid and easily available to end users with time.

I'm also hoping that we're able to get 0.8.1 into official Ubuntu Lucid repositories. Sadly we missed the deadline for being imported from Debian, and I'm not sure who or how to approach this, but at least we got an issue for it [filed on Launchpad][6]. If we also got into the spring releases of Fedora, OpenSUSE, Mandriva et.c. that would be great, but thats of lesser importance.

More important is documentation, we are currently way behind on end-user documentation. I started a skeleton for a [manual][7], and I suspect that I'll be the one to do finish it also as no-one else has shown an interest in working on it. If I get motivated I might also do some screen-casts showing and explaining some features. Another area of documentation is making sure potential contributors have the information they need to easily be able to contribute, and I'm hoping to make all the relevant information available from the [Development page][8] on our wiki. And I'll probably document up some of the code also, eventually. Lots of things to be done in a software project besides writing code!

As a side note, [Krita][9] 2.2 (due in early May) will include a MyPaint brush-engine, which is very cool. And apparently a commercial OS X application (that I cant remember the name of) already uses the it!

## Going to Libre Graphics Meeting?

I'm looking at going to LGM in Brussels this year, to meet with MyPaint, GIMP, Krita and developers of free and open source graphics software. Sadly its on 27th to 30th of May, which really is a bad time for me; May 27th being the dead-line for my senior project report and on June 2nd is my first exam. But we've planned completion of the report 2 weeks before that and I'm trying to prepare in advance for my exams, so I'm hoping that I can go.

To make this event happen and enable developers to go a money-raising campaign has just been launched on Pledgie: http://pledgie.com/campaigns/8926 Please support this effort if you are able!
[![](http://www.pledgie.com/campaigns/8926.png?skin_name=chrome)][10]
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][11]

[0]: http://registry.gimp.org/node/18435
[1]: http://luka.tnode.com/
[2]: http://create.freedesktop.org/wiki/OpenRaster/Reference_Library
[3]: http://mypaint.intilinux.com/?p=302
[4]: http://mypaint.intilinux.com/?p=362
[5]: http://forum.intilinux.com/mypaint-development-and-suggestions/mac-osx-port/msg5950/#msg5950
[6]: https://bugs.launchpad.net/ubuntu/+source/mypaint/+bug/515016
[7]: http://wiki.mypaint.info/Documentation/Manual
[8]: http://wiki.mypaint.info/Development
[9]: http://krita.org/
[10]: http://www.pledgie.com/campaigns/8926
[11]: http://www.jonnor.com/wp/?flattrss_redirect&id=132&md5=1cfe1250de277bcae43b0f7effb6ea60