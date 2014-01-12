---
layout: post
title: How to write a network server in Matlab
description: "Introducing the Matlab Network Server library for network communication in Matlab made easy"
tags: [matlab,programming]
---

This post introduces the open source software that I have written to implement client-server network communication in Matlab.

I use Matlab for numerical simulations, and I intended to use the network link to distribute computational jobs to worker threads running remotely. The idea was that I could prepare the scripts on my local computer but have the actual computations running remotely on my university's high performance computing centre. This turned out to be harder than it should have been because:

1. Matlab does not include built in functions for serializing objects.
2. Matlab's networking library is part of the Instrument Control Toolbox, which I do not have a licence for. Additionally, this library is designed for sending and receiving raw bytes. It cannot send Matlab objects.

In the end I decided to write my own library.

For serialization, I borrowed the [`hlp_serialize` code from the Mathworks File Exchange](http://www.mathworks.com.au/matlabcentral/fileexchange/34564-fast-serializedeserialize/content/hlp_serialize.m). This library implements its own format, and it is as fast as you could hope for from a pure Matlab implementation.

For network communication, I wrote a MEX wrapper around the [ZeroMQ](http://zeromq.org/) library.

I'm making my source code available online. I call this library the [__Matlab Network Server__](https://github.com/bronsonp/matlab-network-server). The code is available on Github. This library makes it easy to implement a client-server architecture (or request-response architecture) in Matlab. Arbitrary Matlab objects can be passed as messages, including custom classes.

Refer to the [Github project]( https://github.com/bronsonp/matlab-network-server) for a basic usage example to get started.
