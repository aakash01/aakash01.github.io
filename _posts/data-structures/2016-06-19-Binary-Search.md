---
layout: post
title: "Binary Search"
description: "Binary Search"
category: Programming
tags: [Java]
published: true
author: aakash01
---
{% include JB/setup %}

## Binary Search 

>Binary search is a Divide & Conquer searching algorithm performed on a sorted array. <br>
>In Binary Search, after each iteration , the size of the search space is reduced to half resulting in the computational complexity of O(log(n)).

``` java
public static int binarySearch(int[] arr, int l, int r, int q){
   if(l<=r){
      int m = l + (r-l)/2;
      if(arr[m] == q){
         return m;
      } else if(arr[m] > q){
         return binarySearch(arr, l, m-1, q);
      }
      return binarySearch(arr, m+1, r, q);
   }
   return -1;
}
```

**Time Complexity : T(n) = T(n/2) + c  == O(log(n)).**

#### Binary Search using generics. 

``` java
public static <T extends Comparable> int genericBinarySearch(T[] arr, int l , int r, T query){
   if(l<=r){
      int m = l  +(r-l)/2;
      int compareIndex = query.compareTo(arr[m]);
      if(compareIndex == 0){
         return m;
      } else if(compareIndex < 0){
         return genericBinarySearch(arr, l, m-1, query);
      }
      return genericBinarySearch(arr, m+1, r, query);
   }
   return -1;
}
```
``` java
Integer[] arr = new Integer[]{1,2,3,7,9};
System.out.println(genericBinarySearch(arr, 0, 4, 2));

String[] strArr = new String[]{"Agra","Bombay","Delhi","Kolkata","Indore"};
System.out.println(genericBinarySearch(strArr, 0, 4, "Kolkata"));
```


