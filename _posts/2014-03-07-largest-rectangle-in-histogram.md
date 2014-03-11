---
layout: post
title: Largest Rectangle in Histogram
description: ""
category: null
tags: []
published: true
---

{% include JB/setup %}
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![histogram]({{http://aakash01.github.io}}/assets/images/histogram.png)

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![histogram_area]({{http://aakash01.github.io}}/assets/images/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = `10` unit.

For example,
Given height = `[2,1,5,6,2,3]`,
return `10`.

{% highlight java linenos %}
public class Solution {
    public int largestRectangleArea(int[] height) {
        int count = 0;
        int max_area = 0;
        Stack<Integer> stack = new Stack<Integer>();
        for(int i=0;i<height.length;i++){
            count = 0;
            while(!stack.isEmpty() && stack.peek() > height[i]){
                int k = stack.pop();
                count++;
                max_area = Math.max(max_area,count*k);
            }
            
            
        for(int j=0;j<=count;j++)
        stack.push(height[i]);
        }
        count = 0;
        while(!stack.isEmpty()){
            int k = stack.pop();
                count++;
                max_area = Math.max(max_area,count*k);
        }
        
        return max_area;
    }
}
{% endhighlight %}

