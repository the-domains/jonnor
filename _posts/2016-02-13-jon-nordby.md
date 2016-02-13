---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - imgflo
  - image
  - layout
  - grid
  - passthrough
  - graph
  - https
  - amp
  - filters
  - content
description: 'When I announced the first release of the imgflo project in April, it was perhaps difficult to see what exactly it was useful for and why we are developing it. This has changed now as 3 weeks ago we launched The Grid, our AI-based web publishing platform.'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:12:00.233Z'
dateModified: '2016-02-13T18:04:33.976Z'
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

When I announced the [first release][0] of the imgflo project in April, it was perhaps difficult to see what exactly it was useful for and why we are developing it. This has changed now as 3 weeks ago we launched [The Grid][1], our [AI-based web publishing][2] platform. We are on a bold mission to have "websites build themselves"; because until posting to personal websites becomes easier and more rewarding than posting to social media, content on the web will continue to pile up in closed silos.
[![](http://www.jonnor.com/wp/files/thegrid-5k-join-300x90.png)][3]

To help solve this problem we built several open source technologies:

[NoFlo][4]: for creating highly testable, component-based, distributed software.  
[Flowhub][5]: for visually and interactively building programs and extensions.  
[GSS][6]: for building constraint-based, responsive layouts  
And of course [imgflo][7]: for on-demand server-side image processing.

In total over 100k lines of code, and around 5000 commits over the last 12 months. Some of the stack is expained in more detail in a recent [interview with Libre Graphics World][8].

### imgflo on The Grid

[thegrid.io][1] launch site is of course built with The Grid. In the particular layout filter used, the look & feel is driven largely by the content. Colors for text captions are extracted from tweets and social media posts, and the featured images are largely unfiltered. Other Grid layout filters may style all provided content, including images, towards a uniform look specified by a color scheme. Or a layout filter may mix-and-match content- versus style-driven design.

The background texture on this section was created with imgflo, by passing the featured image through a blur graph:

[https://imgflo.herokuapp.com/graph/vahj1ThiexotieMo/1ff47cef6f354fe0fbdefb...Fimages%2Fgrid-chrome.jpg&width=1300&height=768&std-dev-x=25&std-dev-y=25][9]
[![](http://www.jonnor.com/wp/files/thegridio-imgflo-bg-texture-300x153.png)][10]

It is important to note that no-one chose this exact image to be used in the particular layout section (and thus have the given image filter applied), which is why processing happens on-demand. The layout section with image inside a computer screen is _available_ for content which has images of type "screenshot". This property may be automatically detected by our image analytics pipeline, or manually annotated by user. The system allows describing many other such _constraints,_ which are all taken into account when it works to create the appropriate layout _for given content_.

Even without considering styling, imgflo has a couple of important roles on a Grid site. Important is the ability create multiple scaled down versions to optimize download size. For this we also created a helper library called [RIG][11], which is used to generate a set of CSS media-queries with imgflo request urls.

     > rig = require 'rig-up' > css = rig content, serverconfig, 'passthrough', parameters, ...  # passthrough is name of the graph to process through   @media (max-width: 503px) { .media, .background { background-image: url('https://imgflo.herokuapp.com/graph/apikey/6bb56129dc707894baa88d10a02a12b9/passthrough?input=https%3A%2F%2Fa.com%2Fb.png&width=400&height=225'); } } @media (min-width: 504px) and (max-width: 1007px) { .media, .background { background-image: url('https://imgflo.herokuapp.com/graph/apikey/d099f7222293d335a6192d742f523bfa/passthrough?input=https%3A%2F%2Fa.com%2Fb.png&width=800&height=450'); } } 

Processing images through imgflo also means that they are cached. So if the original image becomes unavailable, the website still has versions it can use. This can happen for instance on Twitter when people change their profile picture.  
Note that while we optimize images when presented on site, we don't touch the original image (non-destructive). This means image uploaded to The Grid has the full data & metadata preserved, unlike on some other social/web services. However, we are currently not [preserving metadata in processed images][12].

### imgflo 0.2

imgflo is now split into three repositories, the [GEGL-based Flowhub runtime][13], the [HTTP API server][14] and the [native dependencies][13]. The runtime itself is plain C with glib, and could be used in non-web applications for desktop, mobile or embedded.

A major feature is that processing requests can now be authenticated, so that non-legitimate users cannot disrupt legitimate ones by overloading the server. We also use Amazon S3 for caching processed images, offloading a large portion of the work. Servicing 10k++ visits a day with a 2-dyno Heroko app has been no problem with this setup.

In imgflo-server we've also added support for using different processors than imgflo (which uses GEGL), in particular NoFlo with [noflo-canvas][15]. One can now build and deploy image processing pipelines using JavaScript, including all the libraries that work with the <canvas\> element.

Full details about the changes can be found in the changelogs: [server][16], [runtime][17].

### Scale

Flowhub provides imgflo a node-based visual & interactive IDE for developing new image filters for The Grid. It is similar to etablished tools like FilterForge, the Blender compositor, vvvv and nuke - which many designers and visual artists are familiar with. However there are still many snags in the workflow for non-technical people. Smoothing out these is major part of the next imgflo milestone.  
After that the focus will be on horizontal scalability, to handle the load as The Grid enters beta and opens to founding members in spring.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][18]

[0]: http://www.jonnor.com/2014/04/imgflo-0-1-an-image-processing-server-and-flowhub-runtime/
[1]: http://thegrid.io/
[2]: http://techcrunch.com/2014/10/08/the-grid-uses-artificial-intelligence-to-design-your-websites-for-you
[3]: http://www.jonnor.com/wp/files/thegrid-5k-join.png
[4]: http://noflojs.org/
[5]: http://flowhub.io/
[6]: http://gridstylesheets.org/
[7]: http://imgflo.org/
[8]: http://libregraphicsworld.org/blog/entry/artificial-intelligence-designs-websites-uses-open-technology-stack
[9]: https://imgflo.herokuapp.com/graph/vahj1ThiexotieMo/1ff47cef6f354fe0fbdefbf5e12dba2c/gaussianblur?input=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fcdn.thegrid.io%2Fassets%2Fimages%2Fgrid-chrome.jpg&width=1300&height=768&std-dev-x=25&std-dev-y=25
[10]: http://www.jonnor.com/wp/files/thegridio-imgflo-bg-texture.png
[11]: https://www.npmjs.org/package/rig-up
[12]: https://github.com/jonnor/imgflo/issues/68
[13]: http://github.com/jonnor/imgflo
[14]: http://github.com/jonnor/imgflo-server
[15]: https://github.com/noflo/noflo-canvas
[16]: https://github.com/jonnor/imgflo-server/blob/master/CHANGES.md
[17]: https://github.com/jonnor/imgflo/blob/master/CHANGES.md
[18]: http://www.jonnor.com/wp/?flattrss_redirect&id=767&md5=4488157d98e85c1958b9fabdd087e07a