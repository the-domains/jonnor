---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2010/09/massifg-0-2/'
inLanguage: en
starred: false
keywords:
  - massif
  - graph
  - api
  - massifg
  - goffice
  - visualizing
  - usability
  - heap
  - detailed
  - view
description: MassifG is an application for visualizing the output of valgrinds massif tool. See the first release announcement for more info.
datePublished: '2016-02-13T20:30:07.957Z'
dateModified: '2016-02-13T20:10:48.906Z'
author: []
related: []
app_links: []
title: MassifG 0.2
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
# MassifG 0.2

MassifG is an application for visualizing the output of [valgrinds][0] massif tool. See the [first release announcement][1] for more info. Here is the high level list of changes since version 0.1:

* Graphing component ported to use GOffice - graphs are much nicer now
* A detailed view has been implemented
* Parses the heap trees found in massif snapshots
* Menu entry for directly exporting graph to a PNG file
* gtk-doc based API documentation

Of course there were also many minor changes, fixes and improvements. Here is how it looks now (simple and detailed view, respectively):
[![](http://www.jonnor.com/wp/files/massifg-0.2-simple-300x248.png)][2]
[![](http://www.jonnor.com/wp/files/massifg-0.2-detailed-300x247.png)][3]

The tarball can be found [here][4]. Packages for Arch are [i][5][n A][5][UR][5]. I'm also hoping to make packages for Ubuntu and Fedora in the next couple of days.

### Roadmap

I will probably move my focus over to C++ and other tasks now, so MassifG progress will be slower, but here is what I'd like to see going forward.

* Show name of the function when hovering over the graph.  
Minor thing, but it will increase usability a lot as it can be very hard to see which legend entry the data corresponds to in the detailed view. Requires[support in GOffice][6]
* Add axis labels and title with information from the massif file.
* Improve usability on small screen/window size.
* The detailed view currently needs a lot of space, and does not work nicely when this is not available. Need to ask the GOffice people for some hints and tips here.
* Make an API and UI for running massif.  
This so that users don't have to invoke massif manually, and then open the file in MassifG to visualize the results. Would additionally be nice if the graph was updated interactively while massif runs, but that is secondary.
* Make a UI widget for visualizing the heap tree.  
Possibly a GtkTreeView. I'm open for suggestions here.
* Expose a public library with the relevant parts of the API.  
This way, others applications can use it - if anyone is interested I'd love to have some feedback on the API. I am of course open to changing it if necessary. Support for GObject introspection would be nice too.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][7]

If anyone would like to work on any of this, give me a hint so we don't duplicate effort. Let me know if you have any other good ideas too.

[0]: http://valgrind.org/
[1]: http://www.jonnor.com/2010/08/introducing-massifg-0-1/
[2]: http://www.jonnor.com/wp/files/massifg-0.2-simple.png
[3]: http://www.jonnor.com/wp/files/massifg-0.2-detailed.png
[4]: http://www.jonnor.com/files/massifg-0.2.tar.gz
[5]: http://aur.archlinux.org/packages.php?O=0&K=massifg&do_Search=Go
[6]: https://bugzilla.gnome.org/show_bug.cgi?id=627277
[7]: http://www.jonnor.com/wp/?flattrss_redirect&id=241&md5=2e6103bbf424fc51ae08cd3adca37033