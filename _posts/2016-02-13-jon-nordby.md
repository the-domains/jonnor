---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - qml
  - application
  - imago
  - desktop
  - property
  - images
  - qdeclarativeview
  - qobject
  - drop-down
  - folder
description: "In learning Qt, I of course needed to get some experience with the newest and shiniest bits of Qt: Qt Quick. One of the things I've done with that is to make a simple application, an image viewer called Imago. The code can be found at Gitorious."
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:52.979Z'
dateModified: '2016-02-13T18:05:37.128Z'
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

In learning Qt, I of course needed to get some experience with the newest and shiniest bits of Qt: Qt Quick.

One of the things I've done with that is to make a simple application, an image viewer called Imago. The code can be found [at Gitorious][0]. It is a bit different from typical Qt Quick applications as it is not a mobile application but rather targets the desktop. Thus I'm using standard desktop UI concepts like drop-down menues, and ordinary file-chosers.

The lists can be "flicked" through using the pointer, or using the scroll wheel. Moving between the views that show multiple images and the single-image view has a small animation.

### Implementation

In a Qt Quick application two languages and runtimes are involved; C++ and the declarative language that forms the basis of Qt Quick, QML. Qt supports bi-directional communication between the two using a number of metods.  
In my case I chose to make a QObject class that maintains all of the central state in the application. This includes things like what folder is currenty open, the images in that folder, which image is currently focused/selected. All these attributes are implemented as QObject properties, and are notifyiable (meaning they have an attached signal that you guarantee to emit each time the value changes). Exporting this object to QML then allows these properties to be used in property bindings, or for one to connect to the notification signals.  
So in Imago QML is basically used as a "stupid" UI layer for the image view. Other things, like window title and drop-down menues are handed by the C++ side, but by using the signals and properties of the same object.

Writing a desktop application means that one cannot assume a fixed window size like people tend to do for mobile device applications. With setting the resize property of the QDeclarativeView (the widget that displays the QML stuff) to QDeclarativeView::SizeRootObjectToView and using anchor layouts throughout this is possible, but it took me a good while to get working properly. Mostly because the concepts are new, and most (all?) the examples in the documentation seem to neglect this aspect.

The grid and traditional view are actually implemented in different QML files (though the delegate for the images in the list is shared). I did this to test how having several UIs would be like, and for a simple application like this it works out just fine.

### Where to now?

Imago right now is very simple, and could benefit from some added features and some designer love. I also just found a bug in the traditional view that needs to be fixed. I have documented these things in the [README][1] file in case someone is interested. As I have moved my focus over to other projects, I probably wont be taking this application much further, at least not at this time.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][2]

[0]: http://gitorious.org/openismus-playground/imago
[1]: http://gitorious.org/openismus-playground/imago/blobs/master/README.txt
[2]: http://www.jonnor.com/wp/?flattrss_redirect&id=324&md5=39b93d0ff7dc7c79e1e1dccec65db2e9