---
layout: post
title: "Online LaTeX equation rendering"
link: /latex-math/
description: "How I made my online LaTeX equation renderer"
---

I have created a webpage that renders LaTeX equations. In an online chat session, one may want to send an equation, but typical instant message software can't render LaTeX. A simple workaround is to provide a link to a webpage where the equation is visible. You can test out this software [here](/latex-math/).

This software is completely client-side. The server does not store the text being rendered, in fact, the server does not even *see* the text being rendered. The excellent [MathJax](http://www.mathjax.org/) library is used to create beautiful typography.

This was inspired by [P. Lutus' Interactive LaTeX editor](http://arachnoid.com/latex/) but there are some things that I wanted to change:

* Rather than embedding the equation in a HTTP `GET` request, I used the URL hash parameter (that is, the text after the `#` in a URL). The problem with HTTP `GET` requests is that they are length-limited, so you can't simply paste in multiple pages of text with embedded equations. The URL hash is not sent to the server and thereby this length limit is avoided.
* To further assist with rendering large blocks of LaTeX, I used a [JavaScript compression library](http://pieroxy.net/blog/pages/lz-string/index.html) to first compress the text before base64 encoding it. This results is shorter URLs than would otherwise be achieved.

The JavaScript code to implement the LaTeX rendering is visible in [this website's GitHub page](https://raw.github.com/bronsonp/bronson.philippa.fm/master/_pages/latex-math.md).
