---
layout: post
title: "MATLAB: accelerating the ode15s solver"
description: "Tips and tricks that helped me dramatically improve the performance of the ode15s solver"
tags: [matlab,programming]
---

* Plot showing the distribution of solution times for a family of problems in ode15s, indicating the sometimes awful performance

Tips:
* JPattern
* Identically setting partitions to zero
* Steady state hints
* Switching solvers
