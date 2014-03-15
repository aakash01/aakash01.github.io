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


 Hint


 A simple brute force algorithm is 
 
    For each integer i in arr check if it is present. If present continue otherwise return it.

The Complexity of above algorithm will be O(n<sup>2</sup>). Can we reduce it to O(n)?

One method would be to use a hash table `hashtable[n]` and check in hashTable if the number is already occured in array. But is this method efficient? Probably not for large n. So how can we implement it without using extra memory?

The catch here is to use `XOR` bitwise operator.
`XOR` have some special properties : 
* A `XOR` A = 0
* A `XOR` 0 = A

As we can see,  we will iterate through entire array `XORing` each number with one another, all duplicate number will be 0 and we will get the only single number

#### Code (Java)

 
{% highlight cpp linenos %}
public class Solution {
    public int singleNumber(int[] A) {
        int j=0;
        for(int i=0;i<A.length;i++){
            j ^= A[i];
        }
       return j;
    }
}
{% endhighlight %}