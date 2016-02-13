---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2009/11/senior-project-screenshot-and-x11ssh-tip/'
inLanguage: en
starred: false
keywords:
  - x11
  - server
  - ssh
  - xauth
  - nolisten
  - tcp
  - xserverrc
  - forwarding
  - config
  - localhost
description: 'So, I have not really written that post describing my senior project yet (well, I have a draft...), but here is a visual teaser at least: To get this nice image I had to do some X11 forwarding over SSH through an intermediate server.'
datePublished: '2016-02-13T20:31:23.865Z'
dateModified: '2016-02-13T20:16:07.707Z'
author: []
related:
  - score: 0.607191205
    description: "Servers.com, a hosting company with a focus on dedicated bare-metal servers that launched in Europe in 2005, today announced the opening of its first U.S. data center location. The new Dallas data center currently only offers dedicated servers, but it will soon also play host to Servers.com's shared cloud hosting servers."
    title: Servers.com Brings Its Bare-Metal Servers To The US
    url: 'http://techcrunch.com/2015/07/28/servers-com-launches-in-us-takes-aim-at-digitalocean-with-focus-on-bare-metal-servers/'
    thumbnail_height: 400
    thumbnail_url: 'https://tctechcrunch2011.files.wordpress.com/2015/07/8681750288_354823d8d3_o.jpg?w=764&h=400&crop=1'
    thumbnail_width: 764
app_links: []
title: Senior project screenshot and X11+SSH tip
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
# Senior project screenshot and X11+SSH tip

So, I have not really written that post describing my senior project yet (well, I have a draft...), but here is a visual teaser at least:
![](http://www.jonnor.com/wp/files/2009-11-08-003736_1280x800_scrot-300x187.png)

To get this nice image I had to do some X11 forwarding over SSH through an intermediate server. And since I'm probably not the only one with such needs and I'm bound to forget how I did it I will post it here.

Basically I used [this excellent reference][0]. But if you need trusted X11 forwarding (like with ssh -Y instead of -X) you need to generate an xauth file as an extra step when you're on the remote server. That can be done with "xauth generate $DISPLAY ." And the "nolisten tcp" config option that you need to disable locally is usually found in /etc/X11/xinit/xserverrc  
Additional heads up: if you try and connect with -X in addition to this manual forwarding you are setting up, you might get strange errors like "X connection to localhost:10.0 broken (explicit kill or server shutdown)." So don't do that.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][1]

[0]: http://factorial.hu/articles/20080302/more-robust-remote-x-tunneling
[1]: http://www.jonnor.com/wp/?flattrss_redirect&id=76&md5=4c0bf076f1bac376e2cf9ccf6dddfc4b