---
layout: post
title: "Computing Variance is Harder Than You Think"
description: "A simple example of why numerical stability is important, even
when doing the seemingly simple task of computing the variance of a dataset"
category: 
tags: []
---
{% include JB/setup %}

The first pass of understanding a new dataset usually includes having a look
at the descriptive statistics--ie mean, variance, min/max, and 
quantiles. These are all simple statistics that most anyone ever introduced to
statistics will know how to compute. While working on adding descriptive
statistics functionality to pRDDS in [SparklingPandas](LINK) I came across an
example of how a simple numerical
computation of computing the variance over large data sets demand subtle (and
important!) optimizations in their implemenations.

Computations over large amounts of data, often require careful attention to two
things--performance and numerical stability. In the case of computing the
vairance for a random variable, X, 

Numerical Accuracy 
===================
Numerical inaccuracies can come about in a number of ways. More often than not,
the devil is in the floating point arithmetic. In the case of computing the
variance, we know that Var(X) = E[X]^2 - E[X^2]. If E[X]^2 is close to E[X^2],
then this subtraction of these terms using floating point arithmetic will
likely lose significant digits in the computations. You won't see an explicit
error or exception, just an incorrect answer. This means that we can not
compute E[X] and E[X^2] seperately and combine them after making a pass over
all the data and be confident that we have the correct variance.


An alternative strategy would be to compute the mean of X in a first pass, and
then compute E[(\mu - x)^2]. The downside to this approach is that it would
take two passes over the data. It would be significantly faster if we could
compute the variance in a stable way, with a single pass over our data. This is
a good goal to strive for in fast computations on large data sets, and quickly
leads to a line of thinking recurrent in scalable algorithms. You can think of
restricting algorithms to a single pass over the data as often equivalent to
streamign algorithms. Both amount to asking yourself "What would I do if I
could only see each piece of data once?"

The standard method for computing the variance of a random variable in a
streaming setting was proposed by [Person](link).  We update 3 variables each
time we incorporate a new observation of X in to our variance calculation.

mu =
delta =
M2 =

This method avoids the numerical instability of the first method described, but
we are forced to iterate over our collection of observations one at a time. If
we are actually working in a streaming setting, this is fine. In the case I was
trying to solve, and the one I believe to be more common, we a


Performance
==========



