---
author: []
related:
  - score: 0.5581319332
    description: "Servers.com, a hosting company with a focus on dedicated bare-metal servers that launched in Europe in 2005, today announced the opening of its first U.S. data center location. The new Dallas data center currently only offers dedicated servers, but it will soon also play host to Servers.com's shared cloud hosting servers."
    title: Servers.com Brings Its Bare-Metal Servers To The US
    url: 'http://techcrunch.com/2015/07/28/servers-com-launches-in-us-takes-aim-at-digitalocean-with-focus-on-bare-metal-servers/'
    thumbnail_height: 400
    thumbnail_url: 'https://tctechcrunch2011.files.wordpress.com/2015/07/8681750288_354823d8d3_o.jpg?w=764&h=400&crop=1'
    thumbnail_width: 764
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - glom
  - server
  - database
  - postgresql
  - dead-simple
  - glom-postgresql-setup
  - application
  - set
  - user
  - privilege
description: 'Glom is an application that lets you design database systems, including user interface. It can be run as an ordinary application, and will set up and run a the database server for you automatically. But if you want to set up a shared instance, where several users connect with Glom to the same database, you typically want your database server on a dedicated server.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:52.560Z'
dateModified: '2016-02-13T18:05:38.709Z'
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

[Glom][0] is an application that lets you design database systems, including user interface. It can be run as an ordinary application, and will set up and run a the database server for you automatically. But if you want to set up a shared instance, where several users connect with Glom to the same database, you typically want your database server on a dedicated server. And this can be a bit tricky to set up. So, [glom-postgresql-setup][1] was born; A dead-simple utility application to set up a PostgreSQL server for use with Glom. Like Glom, it is written in C++ using Gtkmm.

glom-postgresql-setup lets you to create a database user, and set up the PostgreSQL configuration to accept connections from external IPs. The UI is just a dialog with two fields and two buttons, dead-simple indeed. For now the application requires to be launched with superuser privileges, but before we encourage use of this tool we will of course implement proper privilege escalation using PolicyKit.  
It would also be nice to be able to install and start the PostgreSQL server as well, but currently that is not so easy to do in a cross-distro way. Hopefully packagekit and systemd will help solve that, eventually.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][2]

[0]: http://www.glom.org/wiki/index.php?title=Glom
[1]: http://gitorious.org/openismus-playground/glom-postgresql-setup
[2]: http://www.jonnor.com/wp/?flattrss_redirect&id=315&md5=6cac9348c8363dcac602c92a76e3ac2a