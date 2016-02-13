---
author: []
related:
  - score: 0.6592485905000001
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
  - maliit
  - server
  - applications
  - plugin
  - api
  - input
  - dbus
  - application-hosted
  - method
  - configuration
description: 'The standard way of deploying Maliit is to have a single maliit-server instance (per user session), hosting the actual input method (virtual keyboard, handwriting). Applications then communicate with the server (and by extension, the IM) through an IPC. This allows for a single instance of Maliit to serve all applications, which is memory efficient and robust.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:11:58.924Z'
dateModified: '2016-02-13T18:04:50.187Z'
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

The standard way of deploying [Maliit][0] is to have a single maliit-server instance (per user session), hosting the actual input method (virtual keyboard, handwriting). Applications then communicate with the server (and by extension, the IM) through an IPC.

This allows for a single instance of Maliit to serve all applications, which is memory efficient and robust. A crash in a Maliit IM plugin cannot take down the application and risk loss of significant user data. The disadvantage is the increased system complexity (a separate server process needs to be running at all times\*) and requiring compositing of the application and input method windows. The latter can be quite challenging to do in a well-performing way on low-powered mobile/embedded devices. See [Jans blogpost][1] for how we handled that on the Nokia N9\.

\* By default we make use of DBus autostarting, of course.

### Application-hosted Maliit

To make Maliit more suitable for systems where only a single application runs (embedded) or compositing performance is not good enough, we now also allow Maliit to be "application-hosted": the Maliit server and input method plugins lives in the application process, not a separate server process. Enabling this feature has been a long running task of mine: All the code in input-context and server was made transport independent, a direct transport (no IPC) was introduced, and setting up the server for a given configuration (X11, QPA, app-hosted) was simplified. Other motivations for this work include being able to run the server and IM plugin easily for automated end-to-end system or acceptance testing, or just to easily start the server with a given IM plugin loaded for quick manual testing during development (see Michaels [merge request][2]).

An example application exists as part of the Maliit SDK that demonstrates the feature: [maliit-exampleapp-embedded][3]

This works by having a special input-context "MaliitDirect" which instead of connecting to the server over DBus, creates the server and a direct connection. As when running standalone the server will instantiate and manage the necessary input method plug-ins.

Because the IM does not have its own window in this configuration, the application is responsible for retrieving the IM widget from the server, and re-parenting it into the appropriate place in the widget hierarchy. For all other purposes the application uses the same interface as if the IM was hosted remotely, making sure the abstraction is not broken and that one can easily use the application with Maliit deployed in different configuration.

This feature currently works with Qt4 applications, and is in Maliit since the latest release (0.90.0). One issue is that with the current input method API, the plugin assumes a fullscreen window; overlays extending the base area of the IM will be clipped and size needs to be overridden. This is something we [are fixing][4] in the new [improved API][5].

### Compositor-hosted Maliit

Another approach to make rendering perform better is to host the input method in the process responsible for the compositing. This also reduces the number or processes involved in rendering/compositing, and the associated overhead. This could be a X11 compositing window manager (like KWin or mcompositor), but a more realistic use-case is a Wayland compositor (for instance based on [QtCompositor][6]).

The API allows the consumer to inject an class instance for the configuration dependent logic, allowing to integrate the Maliit server with the logic in the rest of the compositor. Applications will use the normal "Maliit" inputcontext and communicate to the server through an IPC like DBus.

After the work with application-hosted Maliit, this feature was completed by making the server and connection libraries available as public API. The API is available in the latest Maliit release (0.90.0), but is considered unstable until Maliit hits the [1.0][7] mark.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][8]

[0]: http://www.maliit.org/
[1]: http://blog.jpetersen.org/2012/01/25/compositing-in-maliit/
[2]: https://gitorious.org/maliit/maliit-framework/merge_requests/163
[3]: https://gitorious.org/maliit/maliit-framework/trees/master/examples/apps/embedded
[4]: https://gitorious.org/maliit/maliit-framework/merge_requests/145
[5]: https://wiki.maliit.org/Ideas/New_Plugin_Interface
[6]: http://devqt.blogspot.com/2011/03/qt-compositor.html
[7]: https://wiki.maliit.org/Roadmap
[8]: http://www.jonnor.com/wp/?flattrss_redirect&id=541&md5=e1d3e93f5cf5f9709a1699f490e75b2f