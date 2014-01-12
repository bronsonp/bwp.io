---
layout: page
permalink: /software/
title: Software that I've written
---

## Matlab Network Server

* Easy client-server communication in Matlab
* Can send arbitrary Matlab objects over the network
* [Code available on Github.](https://github.com/bronsonp/matlab-network-server)

## Matlab Job Manager

* Framework for running computational tasks written in Matlab
* Memoises results so that previously computed tasks are returned immediately without redoing the calculation. Example use: when making plots, the plot script can be run repeatedly without needed to wait for the computations each time.
* Automates the parallel and/or distributed execution using `parfor` loops, the `qsub` job submission utility in the PBS job scheduler, or the built-in Job Server that distributes tasks to remote workers over a network connection.
* [Code available on Github.](https://github.com/bronsonp/matlab-job-manager)

## Online LaTeX equation sharing

* Easy way to share equations with someone during an online chat.
* Completely client-side (JavaScript) implementation.
* The LaTeX equation is [compressed](http://pieroxy.net/blog/pages/lz-string/index.html), then encoded in `base64`, and then stored in the URL. The server does not store the equations.
* Uses MathJax rendering for beautiful typography.
* [Hosted online on this website.](/latex-math/)
