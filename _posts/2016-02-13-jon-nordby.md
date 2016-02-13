---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - cuda
  - threads
  - hlt
  - nvidia
  - gpus
  - code
  - parallelism
  - cpus
  - kernel
  - used
description: "I've attended a small workshop/seminar in Bergen (at IFT) about nVidia CUDA and its use in the ALICE project at CERN. The goal for me and the other students from Vestfold University College was to get a concrete task for our senior project and to get up to speed on some of the things we need to get started."
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:13:25.642Z'
dateModified: '2016-02-13T18:05:23.045Z'
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

I've attended a small workshop/seminar in Bergen (at [IFT][0]) about nVidia CUDA and its use in the ALICE project at CERN. The goal for me and the other students from Vestfold University College was to get a concrete task for our [senior project][1] and to get up to speed on some of the things we need to get started.

The three days were heavily packed with information, so this will just be a tiny tiny summary. I will probably write up some posts explaining some parts in more detail later. If I can get a hold of the presentations given I will link them here.

### Talks/topics

#### Day 1:

##### Why parallelize and why GPGPU?

Computing units does not scale simply by frequency anymore so we need to parallelize to increase performance. GPUs are commodity hardware designed for massive parallelism driven forward by a huge consumer market in 3D graphics =\> provides high performance, low cost, is flexible and easy to use compared to DSP, FPGA, custom vector CPUs etc.

##### The Nvidia CUDA platform

Describes the underlying hardware platform and a concept for accessing this from a high level language (C with some C++ and custom extensions). Current generation has approx 200 stream processors and is designed to have several thousand threads running at the same time. There are cards especially for GP-computing (Tesla-series), but for a lot of computations the high end GeForce cards are good enough. Practically all newer GPUs from nVidia is CUDA capable, all the way from the Ion found in netbooks/net-tops.

##### CUDA programming model

Functions called kernels are executed on the device. All threads will run this same code, differentiation on which threads do what is done by using their IDs in statements. Threads are grouped into blocks, blocks are grouped into grids. The number of threads/blocks is specified on kernel invocation and used for scaling to different devices. Memory is divided into several parts, each of which needs be handled manually. Device <=\> host transfers is also done manually.

#### Day 2:

##### The TPC and HLT in ALICE.

Incredibly high data rates, not feasible or wanted to store all raw data =\> some processing/analysis needs to be done in real-time ("online"). This can be done now using a large cluster of machines (the HLT). Using GPUs will allow this cluster to consist of a smaller number of nodes =\> cheaper and will free resources for other things like offline analysis.

##### Optimizing CUDA code.

Calculations are fast, (global) memory is slow =\> Focus on reducing and optimizing memory access. Designed for massive parallelism =\> make sure your problem sizes are big enough and that you're split the problem in a good way.

#### Day 3:

##### OpenCL

Basically the CUDA model + vendor/platform independence - C++ features, otherwise only minor differences =\> Should be easy to port to and understand when you know CUDA. Implementations on the way, also for CPUs (x86 with SSE and Cell) and DSPs (Texas Instruments). Likely to be a good candidate for scientific computing in the future.

##### CUDA-ified tracking code

We had a look at how CUDA has been implemented to do a task within the AliRoot framework used in the HLT allready. Some concept mismatches leads to having to wrap code in somewhat ugly ways. Further uglified/complicated by the fact that the same code should be able to run on either the CPU or GPU.

##### Our task: Vertex finding

More about this in a later post!

### Other

I brought a camera along, but as I'm not used to having one with me I completely forgot to take pictures. We did get to see Bergen a little bit, tho we spent most of our time on the CUDA/CERN stuff.  
And there was rain. Every day, all day pretty much. Not sure how I'd cope with that if I lived there.
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][2]

[0]: http://www.uib.no/ift/
[1]: http://www.jonnor.com/2009/09/senior-project-confirmed/
[2]: http://www.jonnor.com/wp/?flattrss_redirect&id=36&md5=39c681a54a8251d31a798a6120510076