---
layout: publication
title: "Analytic solution of the fractional advection-diffusion equation for the time-of-flight experiment in a finite geometry"
doi: "10.1103/PhysRevE.84.041138"
authors:
  - <strong>B. W. Philippa</strong>
  - R. D. White
  - R. E. Robson
preprint: "http://arxiv.org/abs/1108.5831"
local_pdf: "/publications/pdf/2011 - Philippa, White, Robson.pdf"
journal: "Physical Review E"
use_mathjax: true
---

## Non-technical summary

The main novelty of this paper is in the mathematical technique. The
technique has to do with things called *infinite series*. Many
interesting problems can only be solved in terms of an infinite
series. An infinite series is something like:

$$f = g_0 + g_1 + g_2 + g_3 + ...$$

The \\(...\\) there continues forever. This equation says that you
need to add up an *infinite* number of terms in order to calculate the
solution exactly.

Of course, it is not physically possible to add up an infinite number
of things. In practice, what you do is add up 10 terms, or 100 terms,
or 1000 terms, depending upon how accurate you need your solution to
be. Sometimes you get lucky, and 10 terms is good enough for all
practical purposes. Other times, you need thousands or even tens of
thousands of terms. It all depends upon the nature of the problem that
you were solving.

An infinite series that requires an huge number of terms is said to
"converge slowly". Conversely, a series where only a few terms are
needed is one that "converges quickly". Slowly converging series are
annoying, in that they slow down your calculations, and can be tricky
to work with.

It turns out that there's a clever piece of mathematics called the
[*Poisson summation theorem*](http://en.wikipedia.org/wiki/Poisson_summation_formula)
that can convert a slowly converging series into a quickly converging
series. The end result is a completely different series that
(hopefully) converges much more quickly.

My colleague Rob Robson
[showed in 1985](http://dx.doi.org/10.1103/PhysRevA.31.3492) that the
Poisson summation theorem is particularly effective for solutions of
the advection-diffusion equation. This equation describes a wide range
of physical system: charges in a semiconductor, heat in a metal bar,
pollutants in groundwater, and many others.

A relative of the advection-diffusion equation is called the
*fractional* advection-diffusion equation. The fractional modifier
means that the equation describes different physical systems. In this
case, it's charges in a *disordered* semiconductor.

The solution of the fractional advection-diffusion equation is an
infinite series. It's a slowly converging series, and it is difficult
to work with. It's so difficult that it is genuinely challenging to
write a computer program that can evaluate the terms to sufficient
precision to get the series to add up correctly.

This paper shows how the Poisson summation theorem converts this
infinite series into something much nicer. We show that the Poisson
summation theorem and another mathematical trick called the Laplace
transform can together convert this infinite series into a single,
closed-form expression. That means that the end result isn't a series
at all! There's just one term.

This mathematical technique is useful to people using these types of
equations. It provides an alternative representation that is likely to
be easier to work with in many cases.
