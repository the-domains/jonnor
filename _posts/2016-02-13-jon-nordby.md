---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2011/12/gitorious-merge-request-monitor/'
inLanguage: en
starred: false
keywords:
  - mrqbot-7aceb
  - maliit
  - maliit-framework
  - gitorious
  - maliit-plugins
  - merged
  - qml
  - irc
  - mrqbot-affa1
  - desertconsulting
description: 'In Maliit, all changes have to be reviewed by two people in order to be merged to mainline. This helps us catch issues early and keep code quality high. Since the code is hosted on Gitorious, we use their merge requests feature for that purpose.'
datePublished: '2016-02-13T20:30:03.602Z'
dateModified: '2016-02-13T20:03:08.334Z'
author: []
related: []
app_links: []
title: Gitorious Merge Request Monitor
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
# Gitorious Merge Request Monitor

In [Maliit][0], all changes have to be reviewed by two people in order to be merged to mainline. This helps us catch issues early and keep code quality high. Since the code is [hosted on Gitorious][1], we use their merge requests feature for that purpose. Up until now we have periodically checked the website for changes (potentially going through each and every one of the repositories), and manually mentioned updates in the IRC channel. This is both tedious and inefficient, so I wrote a simple tool to help the issue: [Gitorious Merge Request Monitor][2]

It provides an IRC Bot which gives status updates on merge requests in an IRC channel:

One can also query the current status from it:

Status changes are retrieved by periodically checking the Gitorious project activity feed (Atom)\*, and the status itself is scraped from the website. There is no other API right now, unfortunately. Implemented in Python with Twisted, feedparser and BeautifulSoup doing all of the heavy lifting.

Get it from PyPi, using easy\_install or pip:  
`pip install gitorious-mrq-monitor  
gitorious-mrq-monitor --help # For usage information`

For now this solves the immediate need for the development work-flow we have in the Maliit project. Several ideas for extending the tool are mentioned in the [TODO][3]. Contributions welcomed!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][4]

[0]: http://www.maliit.org/
[1]: https://gitorious.org/maliit
[2]: https://github.com/jonnor/gitorious-mrq-monitor
[3]: https://github.com/jonnor/gitorious-mrq-monitor/blob/master/README
[4]: http://www.jonnor.com/wp/?flattrss_redirect&id=520&md5=f88fdda952e1f7eee352d3b58c6bea87