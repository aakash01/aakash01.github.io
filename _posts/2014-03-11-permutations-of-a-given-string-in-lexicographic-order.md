---
layout: post
title: "permutations of a given string in lexicographic order"
description: "permutations of a given string in sorted lexicographic order"
category: Programming
tags: [Programming, Strings]
---
{% include JB/setup %}

> __Print all permutations of a string in sorted (lexographic) order__

If the Input String is `ABC`, the output should be `ABC`, `ACB`, `BAC`, `BCA`, `CAB`, `CBA`.

####Code (C++)
------------------
{% highlight cpp linenos %}
#include<iostream>
using namespace std;

void change(char *a,int i,int j){
	int temp = a[j];
	while(j>i){
		a[j] = a[j-1];
		j--;
	}
	a[j] = temp;
}

void revert(char *a,int i,int j){
	int temp = a[i];
	while(i<j){
		a[i] = a[i+1];
		i++;
	}
	a[i] = temp;
}

void permute(char *a,int i, int n){
	if(i==n)
	cout<<a<<endl;
	else{
		for(int j=i;j<=n;j++){
		change(a,i,j);
		permute(a,i+1,n);
		revert(a,i,j);
		}
	}
}

int main(){
	char a[] = "ABCD";
	permute(a,0,3);
}
{% endhighlight %}