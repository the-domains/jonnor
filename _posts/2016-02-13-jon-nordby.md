---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - input
  - meego
  - plugins
  - methods
  - maliit
  - keyboard
  - qml
  - framework
  - examples
  - repository
description: 'In Maliit input methods are implemented as plugins. This flexibility is important because it allows the same framework to provide very different text input methods, without us having to implement them all. Different virtual keyboards, hardware keyboard input, handwriting, speech-to-text, input methods for accessibility, et.c. are all possible with the Maliit framework.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:52.465Z'
dateModified: '2016-02-13T18:05:38.916Z'
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

In [Maliit][0] input methods are implemented as plugins. This flexibility is important because it allows the same framework to provide very different text input methods, without us having to implement them all. Different virtual keyboards, hardware keyboard input, handwriting, speech-to-text, input methods for accessibility, et.c. are all possible with the Maliit framework. This makes the input method plugin API the most important extension point.

To make it simple to start developing an input method for Maliit, we have written a set of example plugins that can be used as a skeleton\* for a new input method. There is one "Hello World" example showing the C++ interface, and one showing the [newly added QML interface][1]. The latest documentation for the framework in HTML format is also included, along with a simple test application. How to get started is documented on our wiki page: [Go!][2]

A nice thing is that these examples are in our framework repository: built as part of the standard build, with simple tests run as part of our test-suite. This ensures that the examples stay up-to-date and working, something I find that step-by-step, code-and-talk tutorials in some documentation repository/directory typically do not.

If you want to look at real-life examples of plugins, check out the [Meego Keyboard code][3] (C++), the [Meego Keyboard Quick code][4] (QML), or [foolegg][5] from maemo.org's [cute-input-method code][6] (QML with Pinjyin support!). Also make sure to check out [Michael Hasselmann][7]s talk at the Meego Spring 2011 Conference: [Developing custom input methods for Meego][8].

If you hit any issues, contact us through one of [our communication channels][9].

\* Note that currently the license of the examples is LGPLv2 like the rest of the framework.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][10]

[0]: http://wiki.meego.com/Maliit
[1]: http://taschenorakel.de/michael/2011/05/12/writing-qml-based-input-methods-maliit/
[2]: http://wiki.meego.com/Maliit/Documentation#Plugin_development_Quickstart
[3]: https://meego.gitorious.org/meegotouch/meegotouch-inputmethodkeyboard/trees/master/m-keyboard
[4]: https://meego.gitorious.org/meegotouch/meegotouch-inputmethodkeyboard/trees/master/meego-keyboard-quick
[5]: http://talk.maemo.org/member.php?u=31949
[6]: https://github.com/foolegg/cute-input-method/tree/maliit
[7]: http://taschenorakel.de/michael/
[8]: http://sf2011.meego.com/program/sessions/developing-custom-input-methods-meego
[9]: http://wiki.meego.com/Maliit#Communication_channels
[10]: http://www.jonnor.com/wp/?flattrss_redirect&id=413&md5=6902756be5ab084cbc18b2f2a11bedcb