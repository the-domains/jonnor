---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - microflo
  - microcontroller
  - flowhub
  - arduino
  - runtime
  - testing
  - noflo
  - node
  - embedded
  - device
description: ''
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:59.947Z'
dateModified: '2016-02-13T18:04:38.469Z'
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

Its been nearly 6 months since the [previous release][0] of MicroFlo, which was the first that allowed you to visually program your Arduino using NoFlo UI. While we are still just getting started, lots of things have changed since then.

### Flowhub

[Flowhub][1] is the name of the officially supported, packaged and hosted version of the open source NoFlo UI. This is the IDE used for programming with MicroFlo, and a lot of work has been put into it the last couple of months. [_Today we released the beta version_][2].
[![](http://www.jonnor.com/wp/files/flowhub-beta-is-here-tight.png)][3]

You can test it out for browser, node.js and microcontrollers [now][4].

Other runtimes are in development, and you can add your own by implementing the [FBP runtime protocol][5]. For instance there are runtimes for [desktop development][6] for GNOME, [image processing][7] using GEGL, [audio synthesis][8] using SuperCollider and [for Python][9].

### Heterogenous FBP

Often microcontrollers act as sensors and actuators in a larger system, where embedded computers, mobile devices and servers are used to provide the data storage and processing as well as user interfaces and connectivity with other systems.

With MicroFlo 0.3 one can visually create a microcontroller program, and then export ports on this program to make the entire microcontroller available as a component in NoFlo on node.js. This allows to seamlessly create programs which combine microcontrollers and embedded computers.  
We made use of this functionality when we [created an interactive table][10] that shows the status of the Ingress virtual reality game.

### Platform support

MicroFlo has worked on AVR-based Arduinos from day 1, but it was always the goal to not be specific to Arduino. Therefore I'm happy to say that there are now basic platform implementations for:

* AVR-based Arduino and derivatives
* Atmel AVR8 (without using Arduino)
* mbed LPC1768 (ARM Cortex M3)
* Texas Instruments Tiva-C (ARM Cortex M4)
* Embedded Linux (RPi, BeagleBone Black)

Basic bring-up up of new platform can be done in a couple of days, and components which do not use platform-dependent libraries can be used immediately. The goal is to be portable enough that you can pick up whatever capable device you find in your parts-bin, prototype your initial code there - then move the program over to a more ideal device if/when appropriate.  
If you have particular platforms you'd like to see supported, [leave a note][11].

### Simulation & Automated testing

Automated testing in the embedded world using C/C++ is very painful compared to that of recent web technologies. CoffeScript (or JavaScript) in combination with a modern BDD framework like Mocha makes for simple and beautiful tests.

> MicroFlo enables automated BDD testing of microcontroller programs from JavaScript! [https://t.co/VnTSLORSGl][12][pic.twitter.com/noOEf5BxAe][13]
> 
> - Jon Nordby (@jononor) [January 26, 2014][14]

These tests are ran in a simulator which implements the MicroFlo I/O backend (C++) in JavaScript using a Node.js addon. Unfortunately there are not many good open source instruction-level simulators for the platforms MicroFlo support, so the platform backends can only be tested once we support [on-device testing][15].

Automated testing is a critical piece to making sure that MicroFlo is not only a fun and rewarding way to create microcontroller programs, but also an excellent way to make industrial quality devices.

### Easier to get started

MicroFlo now ships a Chrome app, used to let Flowhub communicate with the MicroFlo runtime running on device over serial/USB/Bluetooth. This means it is no longer neccesary to run node.js in a terminal, removing a usability issue in getting started.

In the future, this functionality will be baked into the Flowhub Chrome app itself. With time component code editing, building the firmware and flashing the device will also be available there, making Flowhub a true integrated development environment for MicroFlo.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][16]

[0]: http://www.jonnor.com/2013/11/microflo-0-2-0-visual-arduino-programming/
[1]: http://flowhub.io/
[2]: http://bergie.iki.fi/blog/flowhub-beta/
[3]: http://www.jonnor.com/wp/files/flowhub-beta-is-here-tight.png
[4]: http://flowhub.io/documentation/
[5]: http://noflojs.org/documentation/protocol/
[6]: https://github.com/noflo/noflo-gnome
[7]: http://www.jonnor.com/2014/04/imgflo-0-1-an-image-processing-server-and-flowhub-runtime/
[8]: https://github.com/jonnor/sndflo
[9]: https://github.com/jonnor/protoflo
[10]: http://bergie.iki.fi/blog/ingress-table/
[11]: https://github.com/jonnor/microflo/issues/24
[12]: https://t.co/VnTSLORSGl
[13]: http://t.co/noOEf5BxAe
[14]: https://twitter.com/jononor/statuses/427498832012648448
[15]: https://github.com/jonnor/microflo/issues/13
[16]: http://www.jonnor.com/wp/?flattrss_redirect&id=700&md5=1c579ec2bfcdea3392366545f1bd8949