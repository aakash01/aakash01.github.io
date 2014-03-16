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

-----
####Hint

Simple BruteForce approach would be to, For each day, check how many contiguous days are with less stock price then current price.

{% highlight java linenos %}
int[] calcSpan(int bar[]){
	int[] s = new int[bar.length];
	int span;
	for(int i=0;i<bar.length;i++){
		span=0;
		while(span <= i && bar[i]>=bar[i-span]) {
			span++;
		}
		s[i]=span;
	}
	return s;
}
{% endhighlight %}

`Time Complexity` : `O(n`<sup>`2`</sup>`)`   Space Complexity : `O(1)`

Can we reduce it to O(n) ? 


As we are already keeping tracks of the stock_spans for previous day we don't need to recacluate it again. We will check if the previous stock value is less than the curr value then add the span of the previous stock and repeat this process untill we found a stock with greater value 

So Simple Algo would be .


For a Stock[i], 

	1. check previous stock value, If it is smaller , add the span[i-1] to curr_span and move backwards to j = j-span[j] and repeat the process for stock[j] untill  we found a stock with greater value
	
	2. Else if value of bar[j] > bar[i] stop and update the value.


`Time Complexity` : `O(n)`   Space Complexity : `O(1)`


-----------

####Code(Java)



{% highlight java linenos %}

void calcSpan(int bar[]){
for(int i=0; i<bar.length;i++){
	int j=i-1,span=1;
	while(j>=0 && bar[j]<bar[i]){
		span+=s[j];
		j=j-s[j];
	}
	s[i]=span;
}
}

{% endhighlight %}
