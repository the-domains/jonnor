---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - graph
  - massifg
  - massif
  - output
  - implement
  - parsing
  - gtk
  - goffice
  - pango
  - applications
description: 'MassifG is an application for visualizing the output of valgrinds massif tool. I am writing it as part of my trainee program here at Openismus. MassifG is free software, available under GPLv3. You will find the git repository at gitorious, and the tarball release for 0.1 here.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:53.719Z'
dateModified: '2016-02-13T18:05:34.227Z'
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

MassifG is an application for visualizing the output of [valgrinds][0] massif tool. I am writing it as part of my [trainee program][1] here at [Openismus][2]. MassifG is free software, available under GPLv3\. You will find the git repository [at gitorious][3], and the tarball release for 0.1 [here][4]. Packages for Arch are available [in AUR.][5]

Used together with massif MassifG gives you a nice, simple graph of allocated heap memory over time which you can use to help evaluate if your program is leaking memory or not:

## Current status

With release 0.1 MassifG can:
[![](http://www.jonnor.com/wp/files/massifg-0.1-300x158.png)][6]

* Parse and display a simple graph from massif output.
* Open files selected on the command line or from the UI.
* Print out the graph to a printer or file. This code was contributed by [Murray Cumming][7] - thanks!

I was hoping that I could make version 0.1 the "minimally useful" release, but I have to admit that it is not quite there yet. Instead I nickname release 0.1 "getting it out there". The main issue is that there is massif output that breaks the graph, see under tests/ for an example.

## Implementation

MassifG is written in C, and uses GTK+ for its graphical user interface. Once the ability to export the graph is implemented, it should be easy to allow the application to build and run without GTK, if anyone wants to do that.

The parser is a simple state-machine. It might have been wiser to use bison+flex, and I'll reevaluate that when I need to implement parsing of the detailed output.

The graph functionality is implemented using Cairo and Pango. While Cairo and Pango are excellent technologies with nice APIs, they are quite low-level and that means having to care about all the details. As that brings no benefit to this application I might rewrite the graphing functionality to use the goffice library instead. Sadly there seems to be little high-level or introductionary documentation to goffice APIs, so I might have to fix that along the way.

## Roadmap

In the short term I will:

* Implement parsing and graphing of the detailed massif output
* Fix the graphing bug(s)
* Add the ability to export/save a graph as PNG,PDF et.c. without having to go by the printing dialog

In the longer term I'm considering:

* Adding the ability to run massif on a program directly from MassifG
* An interactive mode which updates the graph while the program to be analyzed is still running
* Making a custom widget which other applications can embed

In the meantime, please do give the current version some testing, and report bugs and other issues.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][8]

[0]: http://valgrind.org/
[1]: http://www.murrayc.com/blog/permalink/2010/03/09/what-our-trainees-learn/
[2]: http://www.openismus.com/
[3]: http://gitorious.org/massifg/massifg
[4]: http://www.jonnor.com/files/massifg-0.1.tar.gz
[5]: http://aur.archlinux.org/packages.php?O=0&K=massifg&do_Search=Go
[6]: http://www.jonnor.com/wp/files/massifg-0.1.png
[7]: http://murrayc.com/
[8]: http://www.jonnor.com/wp/?flattrss_redirect&id=206&md5=d22f50b5d237f1e10bd799efeea7ac7c