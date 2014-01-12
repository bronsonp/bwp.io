---
layout: post
title: "Introducing the Matlab Job Manager"
description: "A MATLAB package for memoisation and remote execution of computational jobs"
tags: [matlab,programming]
---

I am releasing Matlab code for managing and executing computational tasks. I call it the [**Matlab Job Manager**](https://github.com/bronsonp/matlab-job-manager). This is the code that I use to run the tasks for my [scientific simulations](/about/).

Key features:

* [Memoisation](http://en.wikipedia.org/wiki/Memoization) of computed results.
* The memoisation cache is automatically cleared when the associated code is modified.
* Parallel execution using a variety of methods:
    * Matlab's `parfor` construct
    * Clusters running a Portable Batch System scheduler
    * A built-in job server to distribute tasks to workers running remotely.

I'm making this code available online in the hope that others will contribute and make improvements. **If you use this code, please contribute your changes back to me on Github.** The source code is available [here](https://github.com/bronsonp/matlab-job-manager).
