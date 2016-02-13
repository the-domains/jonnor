---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2014/12/sndflo-0-1-visual-supercollider-sound-programming/'
inLanguage: en
starred: false
keywords:
  - supercollider
  - runtime
  - sndflo
  - audio
  - fbp
  - graph
  - websocket
  - flowhub
  - json
  - osc
description: 'SuperCollider is an open source project for real-time audio synthesis and algorithmic composition. It is split into two parts; an interpreter (sclang) implementing the SuperCollider language and the audio synthesis server (scsynth). The server has an directed acyclic graph of nodes which it executes to produce the audio output ( paper| book on internals).'
datePublished: '2016-02-13T20:35:54.186Z'
dateModified: '2016-02-13T20:20:19.173Z'
author: []
related: []
app_links: []
title: 'sndflo 0.1: Visual sound programming in SuperCollider'
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
# sndflo 0.1: Visual sound programming in SuperCollider

[SuperCollider][0] is an open source project for real-time audio synthesis and algorithmic composition.  
It is split into two parts; an interpreter (sclang) implementing the SuperCollider _language _and the _audio synthesis server_ (scsynth).  
The server has an directed acyclic graph of nodes which it executes to produce the audio output ( [paper][1]| [book][2] on internals). It is essentially a dataflow runtime, specialized for the problem domain of real-time audio processing. The client controls the server through OSC messages which manipulates this graph. Typically the client is some SuperCollider code in the sclang interpreter, but one can also use [Clojure,][3][Python][4] or [other clients][5]. It is in many ways quite similar to the [Flowhub][6] visual IDE (a FBP protocol client) and runtimes like [NoFlo][7], [imgflo][8] and [MicroFlo][9].  
So we decided to make SuperCollider a runtime too: [sndflo][10].

We used SuperCollider for [Piksels & Lines Orchestra][11], a audio performance system which hooked into graphics applications like GIMP, Inkscape, MyPaint, Scribus - and sonified the users actions in the application. A lot of time was spent wrestling with SuperCollider, due to the number of new concepts and myriad of ways to do things, and  
lack of (well documented) best practices.  
There is also a tendency to favor very short, expressive constructs (often opaque). An extreme example, here is an album of SuperCollider pieces composed with[][12] (+ [an analysis][13] of some of them).

On the contrary sndflo is very focused and opinionated. It exposes Synths as components, which are be wired together using Busses (edges in the graph), allowing to build audio effect pipelines. There are several [known issues and limitations][14], but it has now reached a minimally useful state. Creating Synths components (the individual effects) as a visual graph of UGen (primitives like Sin,Cos,Min,Max,LowPass) components is also within scope and planned for next release.

The sndflo runtime is itself written [in SuperCollider][15], as an extension. This is to make it easier for those familiar with SuperCollider to understand the code, and to facilitate integration with existing SuperCollider code and tools. For instance setting up a audio pipeline visually using Flowhub+sndflo, then using the Event/Pattern/Stream system in SuperCollider to create an algorithmic composition that drives this pipeline.  
Because a web browser cannot talk OSC (UDP/TCP) and SuperCollider does not talk WebSocket a [node.js wrapper ][16]converts messages on the [FBP protocol][17] between JSON over WebSocket to JSON over OSC.

sndflo also implements the remote runtime part of the FBP protocol, which allows seamless interconnection between runtimes. One can _export ports in one runtime_, and then use it as _a component in another runtime_, communicating over one of the supported transports (typically JSON over WebSocket).
YouTube demo video

<iframe src="http://www.youtube.com/embed/5Rx_WBJD2Mw" frameborder="0" width="420" height="315" style=""></iframe>

In above example sndflo runs on a Raspberry Pi, and is then used as a component in a NoFlo browser runtime to providing a web interface, both programmed with Flowhub. We could in the same way wire up another FBP runtime, for instance use MicroFlo on Arduino to integrate some physical sensors into the system.  
Pretty handy for embedded systems, interactive art installations, internet-of-things or other heterogenous systems.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][18]

[0]: http://supercollider.sourceforge.net/
[1]: http://tim.klingt.org/publications/lac2010_supernova.pdf
[2]: http://supercolliderbook.net/rossbencinach26.pdf
[3]: http://overtone.github.io/
[4]: https://pypi.python.org/pypi/SC/0.2
[5]: http://supercollider.sourceforge.net/wiki/index.php/Systems_interfacing_with_SC
[6]: http://flowhub.io/
[7]: http://noflojs.org/
[8]: http://imgflo.org/
[9]: http://microflo.org/
[10]: http://github.com/jonnor/sndflo
[11]: http://github.com/piksels-and-lines-orchestra
[12]: http://supercollider.sourceforge.net/sc140/
[13]: https://ccrma.stanford.edu/wiki/SuperCollider_Tweets
[14]: http://github.com/jonnor/sndflo/issues
[15]: https://github.com/jonnor/sndflo/tree/master/classes
[16]: https://github.com/jonnor/sndflo/blob/master/sndflo.coffee
[17]: http://noflojs.org/documentation/protocol
[18]: http://www.jonnor.com/wp/?flattrss_redirect&id=786&md5=c55240972332c18b06c6d7162ed0155b