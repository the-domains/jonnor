---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - arduino
  - fbp
  - microflo
  - microcontroller
  - thermometer
  - switch
  - fridge
  - invertboolean
  - hysteresis
  - using
description: "Lately I've been playing with microcontrollers again; Atmel AVRs with and without Arduino boards. I've make a couple of tiny projects myself, helped an artist friend do interactive works and helped to integrated a microcontroller it in an embedded product at work."
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:59.465Z'
dateModified: '2016-02-13T18:04:43.967Z'
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

Lately I've been playing with microcontrollers again; Atmel AVRs with and without [Arduino][0] boards. I've make a couple of tiny projects myself, helped an artist friend do interactive works and helped to integrated a microcontroller it in an embedded product at work. With Arduino, one does not have to worry about interrupts, registers and custom hardware programmers to get things done using a microcontroller. This has opened the door for many more people that pre-Arduino. But the Arduino language is just a collection of C++ classes and functions, users are still left with telling the microcontroller how to do things; "first do this, then this, then this...".

I think always having to work on such a a low level limits what people make with Arduino, both in who's able to use it and what current users are able to achive. So, I created a new experimental project: [MicroFlo][1]. It has a couple of [goals][2], the two first being the most important:

> People should not need to understand text-based, C style programming to be able to program microcontrollers. But those that do know it should be able to use that knowledge, and be able to mix-and-match it with higher-level paradims within a single program.

> It should be possible to verify correctness of a microcontroller program in an automated way, and ideally in a hardware-independent manner.

Inspired by [NoFlo][3], and designed for integration with it, MicroFlo implements [Flow-based programming][4] (FBP). In FBP, a program is constructed by connecting a set of independent components. Each component has in-ports and out-ports, and can only communicate with eachother through these. The connections can be defined using programatically, using a declarative text language, or using a visual editor. 2D/3D artists will recognise this the concept from node compositors like in [Blender][5], sound artists from applications like [Reaktor][6].

### Current status: A fridge

I have an old used fridge, by the looks of it made in the GDR some time before I was born. Not long after I got it, the thermostat broke and the cooler would not turn off. Instead of throwing it away and getting a new one, which would be the cool and practical\* thing to do, I decided to fix it. Using an Arduino and MicroFlo.  
\* especially considering that it is several months since it broke...

A fridge is a simple system, something that should be simple for hobbyists to create. So it was a decent first usecase to test the framework on. Principially, such a system looks something like this:
[![](http://www.jonnor.com/wp/files/fridge-principle-1024x591.jpg)][7]

The thermostat decides whether to turn the cooler on or off, and the cooler switch realizes this decision. There are many alternative methods of implemening each of these two components. I used a DS1820 digital thermometer IC to read temperature, and a hacked NEXA remote controlled relay for the switch.  
All the logic, including temperature threshold is done in software on an Arduino Uno.
[![](http://www.jonnor.com/wp/files/fridge-hardware-190x300.jpg)][8]

The code below for the cooler switch would have been simpler (a oneliner, left as excersise for the reader) if I instead had used a active high relay directly on the mains (illegal if not a certified electrician). Or alternatively reverse-engineered the 433Mhz protocol used.

MicroFlo code for the fridge, in the [.FBP][9] domain specific language ( [examples/fridge.fbp][10])  
`# Thermostat  
timer(Timer) OUT -> TRIGGER thermometer(ReadDallasTemperature)  
thermometer() OUT -> IN hysteresis(HysteresisLatch)`

\# On/Off switch  
hysteresis() OUT -\> IN switch(BreakBeforeMake)  
switch() OUT1 -\> IN ia(InvertBoolean) OUT -\> IN turnOn(DigitalWrite)  
switch() OUT2 -\> IN ic(InvertBoolean) OUT -\> IN turnOff(DigitalWrite)  
\# Feedback cycle to switch required for syncronizing break-before-make logic  
turnOn() OUT -\> IN ib(InvertBoolean) OUT -\> MONITOR1 switch()  
turnOff() OUT -\> IN id(InvertBoolean) OUT -\> MONITOR2 switch()

\# Config  
'5000' -\> INTERVAL timer() \# milliseconds  
'2' -\> LOWTHRESHOLD hysteresis() \# Celcius  
'5' -\> HIGHTHRESHOLD hysteresis() \# Celcius  
'\["0x28", "0xAF", "0x1C", "0xB2", "0x04", "0x00", "0x00", "0x33"\]' -\> ADDRESS thermometer()  
board(ArduinoUno) PIN9 -\> PIN thermometer()  
board() PIN12 -\> PIN turnOff()  
board() PIN11 -\> PIN turnOn()

Is the above solution nicer than using the Arduino IDE and writing in C++? At the moment maybe not significantly so. But it does prove that this kind of high-level dynamic programming model is feasible to implement also on devices with 2kB RAM and 32kB program memory. And it is a starting point for more interesting exploration.

### Next steps

I will continue to experiment with using MicroFlo for new projects, to develop more components and test/validate the architecture and programming model. I also need to read through all of the [canonical book on FBP][11] by [J. Paul Morrison][12].

Some bigger things that I want to add include:

* Ability to introspect the graph running on the device, in particular the packets moving between components.
* Automated testing (of the framework, individual components and application graphs) using JavaScript [BDD][13] test frameworks like Mocha or Vows.
* Ability to change graphs at runtime, and then persist it to EEPROM so it will be loaded on next reset.

And eventually: Allowing to manipulate and monitor running graphs visually, using the NoFlo development environment. See [bug \#1][14].

Curious still? Check out [the code][1], and ask on the [FBP mailing list][15] if you have any questions!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][16]

[0]: http://arduino.cc/
[1]: https://github.com/jonnor/microflo
[2]: https://github.com/jonnor/microflo#goals
[3]: http://noflojs.org/
[4]: http://en.wikipedia.org/wiki/Flow-based_programming
[5]: https://www.youtube.com/results?search_query=blender+node+compositor
[6]: https://www.youtube.com/results?q=reaktor+programming
[7]: http://www.jonnor.com/wp/files/fridge-principle.jpg
[8]: http://www.jonnor.com/wp/files/fridge-hardware.jpg
[9]: http://noflojs.org/documentation/fbp/
[10]: https://github.com/jonnor/microflo/blob/master/examples/fridge.fbp
[11]: http://www.lulu.com/spotlight/paul_morrison
[12]: http://www.jpaulmorrison.com/
[13]: http://en.wikipedia.org/wiki/Behavior-driven_development
[14]: https://github.com/jonnor/microflo/issues/1
[15]: https://groups.google.com/forum/#!topic/flow-based-programming
[16]: http://www.jonnor.com/wp/?flattrss_redirect&id=643&md5=00e35387e2a644a38ec8584fdcf32c83