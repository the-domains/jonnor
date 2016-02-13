---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - openraster
  - gtk
  - libora
  - qml
  - application
  - especially
  - interfaces
  - project
  - useful
  - development
description: "I've actually been back close to a week now, but never mind that... In the per-conference day with training sessions I attended the Qt Essentials track, which was more or less as expected. Glad I read a full Qt book beforehand, it would have been challenging to keep up with the shear amount of information without it."
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:14:45.791Z'
dateModified: '2016-02-13T18:05:36.890Z'
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

I've actually been back close to a week now, but never mind that...

In the per-conference day with training sessions I attended the Qt Essentials track, which was more or less as expected. Glad I read a full Qt book beforehand, it would have been challenging to keep up with the shear amount of information without it.  
The keynotes I attended on the second day were not particularly exciting: no major announcements nor insights were given. The technical talks on the other hand were filled with goodies. The talks by Jens Bache-Wiig and Roberto Raggi on [Qt Quick][0] were especially good.\*

The talks definitely made me want to try Qt Quick for doing user interfaces for small-form factor devices, especially because it allows for very rapid prototyping and iterations when developing. The current lack of widgets and traditional layouts probably limits its usefulness for typical desktop application with more complex user interfaces though. There is nothing that helps you achieve a native look and feel either, but the [Qt Components][1] project is aiming to bridge those gaps.  
I also suspect that the declarative and dynamic nature of QML poses several new challenges for developers, especially for those that are mostly used to traditional Qt programming with C++. I'm especially concerned that there was no way to visualize or do static checking on the property-bindings that are so central in QML. Very curious as to how that plays out in practice.

\*I'm told the talks will be online after the Qt Developer Days event in San Fransisco is over.

### Qt projects you said?

Going forward I'll be doing some projects with Qt, in the same way I [have done][2] with GTK. My first project has already started: implementing viewer-class OpenRaster support for Qt. This means that applications using Qt and QImage will soon be able to display fully-rendered OpenRaster images!  
Development of the Qt integration happens in the [repository on gitorious][3], and the libora modifications currently lives in [my personal clone][4]. It will be pushed to mainline as soon as I have more-or-less settled on the API, and done a basic implementation. Using libora for all the OpenRaster specific stuff is being a bit more painful than expected, but it is the right thing to do as it means that other consumers benefits as well. Like a potential GdkPixbuf plugin or applications not using Qt or GTK. I'll write more once it reaches a useful state.

After that is done I will probably do something with more UI, like a proper application. Hopefully I will get to toss Qt Quick into the mix as well. I've got an idea that I think would be a nice fit, so we'll see.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][5]

[0]: http://doc.qt.nokia.com/4.7/qtquick.html
[1]: http://qt.gitorious.org/qt-components
[2]: http://www.jonnor.com/tag/massifg/
[3]: http://gitorious.org/openraster/qt-viewer-support
[4]: http://gitorious.org/~jonnor/openraster/jonnors-libora
[5]: http://www.jonnor.com/wp/?flattrss_redirect&id=298&md5=861daec9a362120d9b8c63a3010dafd7