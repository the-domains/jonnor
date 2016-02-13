---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - gtk
  - maliit
  - implement
  - meego
  - support
  - input
  - mainline
  - repository
  - javis
  - code
description: 'GTK+ application support for Maliit input methods has existed for a long time, but up until now it has lived in separate repositories. This has been inconvenient for users and for developers, and was the major cause for it to not be on the same level as the Qt support.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:52.710Z'
dateModified: '2016-02-13T18:05:38.447Z'
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

GTK+ application support for [Maliit][0] input methods has existed for a long time, but up until now it has lived in separate repositories. This has been inconvenient for users and for developers, and was the major cause for it to not be on the same level as the Qt support. This has changed as the GTK+ support has now been merged into the maliit-framework repository, and along side the Qt support. Maliit 0.80.8, which was [released yesterday][1], contains these changes.

Two implementations existed for Maliit GTK+ support. [One][2] was written by [Javis Pedro][3] as part of a Google Summer of Code project for MeeGo in 2010\. His blog has [several posts][4] on the topic.[The other][5] implementation was maintained by Raymond Liu (Intel). This is the implementation shipped in Meego Netbook, and the one improved by [Claudio Saavedra][6] (Igalia) as part of the GTK+ on MeeGo project. It was also the only one that was updated to work with the DBus connection changes that was done quite some time ago, and supporting both GTK 2 and 3\. For these reasons this was the implementation integrated into mainline Maliit.

Once the code [was integrated][7], improvements soon followed. The application now correctly[reconnects to server][8], and make install will automatically update the GTK+ input module cache [on Ubuntu][9], thanks to [Łukasz Zemczak][10] (Canonical), and [on Fedora][11]. This means GTK+ application support will work out of the box, no twiddling needed.

While this is a huge step in the right direction, the GTK+ support is not as good as for Qt yet. Javis Pedros implementation has features that does not exist in mainline, so code/principles can hopefully be reused from there to implement these. This includes custom toolbars and attribute extensions, and content type hints for text entries. Other features looks hard to implement due to limitations/differences in the input context plugin architecture found in GTK+, and will probably need work in GTK+ itself to solve.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][12]

[0]: http://www.maliit.org/
[1]: http://lists.meego.com/pipermail/meego-inputmethods/2011-November/000251.html
[2]: https://gitorious.org/meego-gtk-im
[3]: http://javispedro.com/
[4]: http://javispedro.com/cgi-bin/mt/mt-search.fcgi?search=meegotouch&IncludeBlogs=1&limit=20
[5]: https://www.gitorious.org/meegotouch-inputmethodbridges
[6]: http://people.gnome.org/~csaavedra/
[7]: https://gitorious.org/maliit/maliit-framework/merge_requests/77
[8]: https://gitorious.org/maliit/maliit-framework/commit/04b7b8ac3160b8a042e63b2ea2c72464ef74a37b
[9]: https://gitorious.org/maliit/maliit-framework/commit/783602d3243d3df47633a8658b27d55175e717aa
[10]: http://sil2100.vexillium.org/
[11]: https://gitorious.org/maliit/maliit-framework/commit/24393bc8e0bd61ccc36629e94084c0066e6c181d
[12]: http://www.jonnor.com/wp/?flattrss_redirect&id=502&md5=0fc2dba944a22dd3bf2e7dd963085acc