---
layout: post
title: "Finding Spans"
description: ""
category: Programming
tags: [Programming, Stacks]
---
{% include JB/setup %}

>	**Finding Spans** : Given an array A the span S[i] of A[i] is the maximum number of consecutive elements A[j] immediately preceding A[i] and such that A[j] <= A[i].



>	#####[The stock span problem](http://en.wikipedia.org/wiki/Stack_(abstract_data_type&#41;#The_Stock_Span_Problem) is a financial problem where we have a series of n daily price quotes for a stock and we need to calculate span of stock's price for all n days. 
>	#####The span Si of the stock's price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its price on the given day.

![Finding_Spans]({{http://aakash01.github.io}}/assets/images/find_spans.png)

For Eg:

If an array of 6 days prices is given as {80, 30, 40, 65, 90, 30}, then the span values for corresponding 6 days are {1, 1, 2, 3, 5, 1}



