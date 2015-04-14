---
layout: post
title: "How do I test if a data is Normal?"
description: ""
category: 
tags: []
---
{% include JB/setup %}

The other day, a colleague asked me how to tell if a data set followed a normal
distribution. In order to answer this question well, we need to first answer
"What is a distribution?" We usually identify distributions in terms of functions
defined on the domain of a random variable (the domain being the possible values
it can take) where these functions allow us to compute probabilities of the
corresponding random variable taking on a specific value or range of values.

In probability and statistics, often the first definition you see is in terms
of a probability density function (PDF) where it is seemingly the most intuitive
representation. That is, until you realize that you are spending an inordinate
amount of time talking about how to properly interpret what the value of a PDF
at a point *is*. The long and the short of it is that nothing about PDFs really
make much sense unless they are inside of an integral. This is just another facet
of integration making functions nicer objects to work with. We can define the CDF
of a distribution in terms of its pdf $mu(y)dy$ as $cdf(x) = \int_{-\infinity}
^{x}\mu(y)dy$ 

Because we are prone to integrating away our problems, statisticians have built
statistical tests about distributions around CDFs instead of PDFs. There are two
ways that I go about deciding if a data set follows a particular distribution-
A parametric method called the Kolmogorov-Smirnoff type test and the non parametric
method of analyzing a Q-Q plot.

Kolmogorov-Smirnoff Test
========================

Q-Q Plot
========

