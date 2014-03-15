---
layout: post
title: "Coin Tosses"
description: "Coin Tosses"
category: programming
tags: [Programming, probability, codesprint]
author: aakash01
---
{% include JB/setup %}




>####You have an unbiased coin which you want to keep tossing until you get N consecutive heads.You've tossed the coin M times and surprisingly, all tosses resulted in heads. <br/>What is the expected number of additional tosses needed until you get N consecutive heads?
><br/><br/>Input:
>#####The first line contains the number of cases T. Each of the next T lines contains two numbers N and M.
><br/><br/>Output:
>#####Output T lines containing the answer for the corresponding test case. Print the answer rounded to exactly 2 decimal places.
	Sample Input:4
	2 0
	2 1
	3 3
	3 2
	Sample Output:6.00
	4.00
	0.00
	8.00
*Sample Explanation:*

If N = `2` and M = `0`, you need to keep tossing the coin until you get 2 consecutive heads. It is not hard to show that on average, 6 coin tosses are needed.

If N = `2` and M = `1`, you need 2 consecutive heads and have already have 1. You need to toss once more no matter what. In that first toss, if you get heads, you are done. Otherwise, you need to start over, as the consecutive counter resets, and you need to keep tossing the coin until you get N=2 consecutive heads. <br/>
The expected Number of coin tosses is thus `1 + (0.5 * 0 + 0.5 * 6) = 4.0`

If N = `3` and M = `3`, you already have got 3 heads, so you do not need any more tosses.

	Constraints:1 <= T <= 100
	1 <= N <= 1000
	0 <= M <= N

-------------------

### Hint

This problem is a Mathematical Expectation problem

Mathematically, for a discrete variable X with probability function P(X), the expected value E[X] is given by &Sigma; x<sub>i</sub>P(x<sub>i</sub>) the summation runs over all the distinct values x<sub>i</sub> that the variable can take.

For Eg.

**Find number of coin flips for getting a single head.**

Let Expected number of coin flips for getting a head is `x`

	a. If the first flip is the head, then we are done. The probability of this event is 1/2 and the number of coin flips for this event is 1. 

	b. If the first flip is the tails, then we have to start over.The probability of this event is 1/2 and the expected number of coins flips now onwards is x. But we have already wasted one flip, so the total number of flips is x+1.
 
 this gives ,

 x = (1/2)(1) + (1/2) (1+x)

Solving, we get x = 2. 

Similarly for n consecutive heads ,

1. if 1st , 2nd , 3rd or nth flip gives tail then we have to start all over again.
2. else we are done

Combining 1 & 2 gives x = `(1/2)(x+1) + (1/4)(x+2) + ... + (1/(2^k))(x+k) + .. + (1/(2`<sup>`N`</sup>`))(x+N)  + (1/(2`<sup>`N`</sup>`))(N)`

we get,

x = `2`<sup>`N+1`</sup>`-2` .



*We can also understand it this way* ,

let `En` be the probability for n consecutive heads  means

In order to obtain n consecutive heads, we must first obtain n-1 consecutive heads, followed by:

* with probability &#189;, a further head; or

* with probability &#189;, a tail, after which we must obtain n consecutive heads.

It follows that En = &#189;`(En-1 + 1) + `&#189;`(En-1 + 1 + En)`, from which En = `2En-1 + 2`. which also give En = `2N+1-2`  .


Now as per given problem we already have M number of heads therefore let rest number of coin flips required be x.

let k =N-M be the consecutive heads required.

so,

1. if 1st , 2nd , 3rd or kth flip gives tail then we have to start all over again ie. to find n consecutive heads.
2. else we are done

which gives

y =  `(1/2)(x+1) + (1/4)(x+2) + ... + (1/(2`<sup>`k`</sup>`))(x+k)  + (1/(2`<sup>`N-k`</sup>`))(k)`

and x = `2N+1-2`.

solving this gives , 

y = `2N+1 - 2M+1`



#### Code (Java)

 
{% highlight cpp linenos %}
import java.math.BigInteger;
import java.util.Scanner;
public class Solution {
    public static void main(String[] args) {
        Scanner a = new Scanner(System.in);
        int t= a.nextInt();
        while(t--!=0){
            int n=a.nextInt();
            int m = a.nextInt();
            BigInteger b = BigInteger.valueOf(2).pow(n+1);
            BigInteger c= BigInteger.valueOf(2).pow(m+1);
            System.out.println(b.subtract(c)+".00");
    }}
}
{% endhighlight %}