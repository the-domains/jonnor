---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - msgflo
  - participants
  - noflo
  - node
  - dynos
  - inport
  - msg
  - messages
  - process
  - graph
description: 'At The Grid we do a lot of CPU intensive work on the backend as part of producing web pages. This includes content extraction, normalization, image analytics, webpage auto-layout using constraint solvers, webpage optimization ( GSS to CSS compilation) and image processing.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:12:02.267Z'
dateModified: '2016-02-13T18:04:26.657Z'
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

At [The Grid][0] we do a lot of CPU intensive work on the backend as part of producing web pages. This includes content extraction, normalization, image analytics, webpage auto-layout using constraint solvers, webpage optimization ( [GSS][1] to CSS compilation) and [image processing][2].

The system runs on Heroku, and spreads over some 10 different dyno roles, communicating between each other using AMQP message queues. Some of the dyno separation also deals with external APIs, allowing us to handle service failures and API rate limiting in a robust manner.

Majority of the workers are implemented using [NoFlo][3], a flow-based-programming for Node.js (and browser), using [Flowhub][4] as our IDE. This gives us a strictly encapsulated, visual, introspectable view of the worker; making for a testable and easy-to-understand architecture.

However NoFlo is only concerned about an individual worker process: it does not comprehend that it is a part of a bigger system.

### Enter MsgFlo

[MsgFlo][5] is a new FBP runtime designed for distributed systems. Each node represents a separate process, and the connections (edges) between nodes are message queues in a broker process.  
To make this distinction clearer, we've adopted the term _participant_ for a node which participates in a MsgFlo network.  
Because MsgFlo implements the same [FBP runtime protocol][6] and [JSON graph format][7] as NoFlo, imgflo, [MicroFlo][8] - we can use the same tools, including the [.FBP DSL][9] and Flowhub IDE.

The graph above represents how different _roles_ are wired together. There may be 1-N participants in the same role, for instance 10 dynos of the same dyno type on Heroku.  
There can also be multiple participants in a single process. This can be useful to make different independent facets show up as independent nodes in a graph, even if they happen to be executing in the same process. One could use the same mechanism to implement a shared-nothing message-passing multithreading model, with the limitation that every message will pass through a broker.

Connections have pub-sub semantics, so generally each of the individual dynos will receive messages sent on the connection.  
The special component _msgflo/RoundRobin_ specifies that messages should be delivered in a round-robin fashion: new message goes only to the next process in that role with available capacity. The RoundRobin component also supports dead-lettering, so failed jobs can be routed to another queue. For instance to be re-processed at a later point automatically, or manually after developers have located and fixed the issue. This way one never loose pending work.  
On AMQP roundrobin delivery and deadlettering can be fulfilled by the broker (e.g. RabbitMQ), so there is no dedicated process for that node.

### Messaging systems

People use different messaging systems. We've tried to make sure that MsgFlo architecture and tools can be used with many different. The format and delivery of [discovery messages is specified][10], and the tools have a transport abstraction layer. Currently there is production-level support for AMQP 0-9-1 (tested with RabbitMQ). Basic support exists for [MQTT][11], a simple protocol popular in distributed "Internet-of-Things" type systems. Support for more transports can be added by [implementing two classes][12].

### Polyglot participation

MsgFlo itself only handles the discovery of participants and setup of the connections between them, as well as providing debug capabilities like Flowhub endpoint support. Having participants in a particular language requires implementing . We do provide a set of libraries that makes this easy for popular languages:

Using [noflo-runtime-msgflo][13] makes it super simple to use NoFlo as MsgFlo participants. The exported ports of the NoFlo graph or component (for instance 'in', 'out', and 'error') will be automatically made available as queues in MsgFlo, and one can connect this into a bigger system.

    noflo-runtime-msgflo --name compute_foo --graph project/MyGraph

If you have some plain Node.js you can use [msgflo-nodejs][14], like this real-life [example from imgflo-server][15].

    msgflo = require 'msgflo' ProcessImageParticipant = (client, role) -> definition = component: 'imgflo-server/ProcessImage' icon: 'file-image-o' label: 'Executes image processing jobs' inports: [ id: 'job' type: 'object' ] outports: [ id: 'jobresult' type: 'object' ] func = (inport, job, send) -> throw new Error 'Unsupported port: ' + inport if inport != 'job' # XXX: use an error queue? @executor.doJob job, (result) -> send 'jobresult', null, result return new msgflo.participant.Participant client, definition, func, role 

In addition to node.js and NoFlo, there is basic participant support provided for Python and for C++ (with AMQP). It took about about half a day and 2-300 lines of code, so adding support for more languages should be pretty simple. There are even [tests][16] you [can reuse][17].

[Example][18] in Python using [msgflo-python][19]:

    import msgflo class Repeat(msgflo.Participant): def __init__(self, role): d = { 'component': 'PythonRepeat', 'label': 'Repeat input data without change', } msgflo.Participant.__init__(self, d, role) def process(self, inport, msg): self.send('out', msg.data) self.ack(msg) 

[Example][20] becomes a bit more verbose in C++11, using [msgflo-cpp][21].

     class Repeat : public msgflo::Participant { struct Def : public msgflo::Definition { Def(void) : msgflo::Definition() { component = "C++Repeat"; label = "Repeats input on outport unchanged"; outports = { { "out", "any", "" } }; } }; public: Repeat(std::string role) : msgflo::Participant(role, Def()) { } private: virtual void process(std::string port, msgflo::Message msg) { std::cout << "Repeat.process()" << std::endl; msgflo::Message out; out.json = msg.json; send("out", out); ack(msg); } }; 

### Next

Since MsgFlo 0.3, we are using MsgFlo in production for _all_ workers across The Grid backends. After migrating we've also moved more things into dedicated participants, because we now have the tooling that makes managing that complexity easy. Our short term focus now is more tools around MsgFlo, like deadline-based autoscaling and integration of data-driven testing using [fbp-spec][22]. Features planned for MsgFlo itself includes live [introspection of messages][23] in Flowhub.

Looking further ahead, we would like to make more use of the polyglot capabilities, for instance by move some of our image analytics out from NoFlo/node.js participants (with C/C++ libs) to pure C++ 11 participants.  
I also hope to do some fun projects with MQTT and MicroFlo - and validate MsgFlo for Embedded/Internet-of-Things-type.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][24]

[0]: http://thegrid.io/
[1]: http://gridstylesheets.org/
[2]: http://imgflo.org/
[3]: http://noflojs.org/
[4]: https://flowhub.io/
[5]: https://github.com/the-grid/msgflo
[6]: http://noflojs.org/documentation/protocol/
[7]: http://noflojs.org/documentation/json
[8]: http://microflo.org/
[9]: http://noflojs.org/documentation/fbp/
[10]: https://github.com/msgflo/msgflo#communications
[11]: http://en.wikipedia.org/wiki/MQTT
[12]: https://github.com/msgflo/msgflo-nodejs/blob/master/src/direct.coffee
[13]: https://github.com/noflo/noflo-runtime-msgflo
[14]: https://github.com/jonnor/imgflo-server
[15]: https://github.com/jonnor/imgflo-server/blob/master/src/worker.coffee
[16]: https://github.com/msgflo/msgflo/blob/master/spec/heterogenous.coffee
[17]: https://github.com/msgflo/msgflo-cpp/blob/master/spec/participant.coffee
[18]: https://github.com/msgflo/msgflo-python/blob/master/examples/repeat.py
[19]: https://github.com/msgflo/msgflo-python
[20]: https://github.com/msgflo/msgflo-cpp/blob/master/examples/repeat.cpp
[21]: https://github.com/the-grid/msgflo-cpp
[22]: https://github.com/flowbased/fbp-spec
[23]: https://github.com/msgflo/msgflo/issues/3
[24]: http://www.jonnor.com/wp/?flattrss_redirect&id=815&md5=a0c98e44d07e5a56286937e5ad4c76be