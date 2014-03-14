---
layout: post
title: "Single Number"
description: ""
category: programming
tags: [Programming, leetcode]
---
{% include JB/setup %}

> Given an array of integers, every element appears twice except for one. Find that single one.

Ex:
 arr = `1,2,3,4,2,3,1`
 output : `4`


 __Hint__

 A simple brute force algorithm is 
 <div class="panel panel-default">
  <div class="panel-body">
    For each integer i in arr check if it is present. If present continue otherwise return it.
  </div>
</div>


As we can see,  we will iterate through entire array `XORing` each number with one another, all duplicate number will be 0 and we will get the only single number

#### Code (Java)
{% highlight cpp linenos %}
public class Solution {
    public int singleNumber(int[] A) {
        int j= 0;
        for(int i=0;i<A.length;i++){
            j ^= A[i];
        }
       return j;
    }
}
{% endhighlight %}