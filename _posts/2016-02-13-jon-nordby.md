---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2011/01/want-to-integrate-with-the-meego-netbook-ux-panel/'
inLanguage: en
starred: false
keywords:
  - meego
  - api
  - bugreport
  - dbus
  - gtk
  - mutter-meego
  - libmeego-panel
  - netbook
  - readme
  - gitorious
description: 'It is not well communicated, but you can apparently write your own "tabs"/"panes" for the panel/toolbar found in the Meego Netbook UX. Hopefully this blogpost helps a tiny bit*. As stated by the libmeego-panel/docs/README in the source tree of mutter-meego there are convenience APIs for GTK+ and Clutter based implementations.'
datePublished: '2016-02-13T20:29:15.428Z'
dateModified: '2016-02-13T19:56:05.679Z'
author: []
related: []
app_links: []
title: Meego Netbook UX
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
# Meego Netbook UX

It is not well communicated, but you can apparently write your own "tabs"/"panes" for the panel/toolbar found in the Meego Netbook UX. Hopefully this blogpost helps a tiny bit\*.

As stated by the [libmeego-panel/docs/README][0] in the [source tree of mutter-meego][1] there are convenience APIs for GTK+ and Clutter based implementations. But it seems you can also just use the DBUS API, in case you prefer Qt or something else. I found this out by searching though meego.gitorious.org after someone asked on \#meego

\*Since this should be documented in the platform API, I've of course filed a [bugreport][2].
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][3]

[0]: http://meego.gitorious.org/meego-netbook-ux/mutter-meego/blobs/master/libmeego-panel/docs/README
[1]: http://meego.gitorious.org/meego-netbook-ux/mutter-meego
[2]: http://bugs.meego.com/show_bug.cgi?id=12748
[3]: http://www.jonnor.com/wp/?flattrss_redirect&id=368&md5=28173de74aaacdd352c6f0953aaebac1