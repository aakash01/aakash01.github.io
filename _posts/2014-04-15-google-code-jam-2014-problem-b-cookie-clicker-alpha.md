---
layout: post
title: "Google Code Jam 2014: Problem B. Cookie Clicker Alpha"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##Problem

	Introduction

	Cookie Clicker is a Javascript game by Orteil, where players click on a picture of a giant cookie. Clicking on the giant cookie gives them cookies. They can spend those cookies to buy buildings. Those buildings help them get even more cookies. Like this problem, the game is very cookie-focused. This problem has a similar idea, but it does not assume you have played Cookie Clicker. Please don't go play it now: it might be a long time before you come back.

	Problem

	In this problem, you start with 0 cookies. You gain cookies at a rate of 2 cookies per second, by clicking on a giant cookie. Any time you have at least C cookies, you can buy a cookie farm. Every time you buy a cookie farm, it costs you C cookies and gives you an extra F cookies per second.

	Once you have X cookies that you haven't spent on farms, you win! Figure out how long it will take you to win if you use the best possible strategy.

	Example

	Suppose C=500.0, F=4.0 and X=2000.0. Here's how the best possible strategy plays out:

	   i. You start with 0 cookies, but producing 2 cookies per second.
	  ii. After 250 seconds, you will have C=500 cookies and can buy a farm that produces F=4 cookies per second.
     iii. After buying the farm, you have 0 cookies, and your total cookie production is 6 cookies per second.
	  iv. The next farm will cost 500 cookies, which you can buy after about 83.3333333 seconds.
	   v. After buying your second farm, you have 0 cookies, and your total cookie production is 10 cookies per second.
	  vi. Another farm will cost 500 cookies, which you can buy after 50 seconds.
	 vii. After buying your third farm, you have 0 cookies, and your total cookie production is 14 cookies per second.
	viii. Another farm would cost 500 cookies, but it actually makes sense not to buy it: instead you can just wait until you have X=2000 cookies, which takes about 	 142.8571429 seconds.
	Total time: 250 + 83.3333333 + 50 + 142.8571429 = 526.1904762 seconds.
	Notice that you get cookies continuously: so 0.1 seconds after the game starts you'll have 0.2 cookies, and t seconds after the game starts you'll have 2t cookies.

	Input

	The first line of the input gives the number of test cases, T. T lines follow. Each line contains three space-separated real-valued numbers: C, F and X, whose meanings are described earlier in the problem statement.

	C, F and X will each consist of at least 1 digit followed by 1 decimal point followed by from 1 to 5 digits. There will be no leading zeroes.

	Output

	For each test case, output one line containing "Case #x: y", where x is the test case number (starting from 1) and y is the minimum number of seconds it takes before you can have X delicious cookies.

	We recommend outputting y to 7 decimal places, but it is not required. y will be considered correct if it is close enough to the correct number: within an absolute or relative error of 10-6. See the FAQ for an explanation of what that means, and what formats of real numbers we accept.

	Limits

	1 <= T <= 100.

	Small dataset

	1 <= C <= 500.
	1 <= F <= 4.
	1 <= X <= 2000.

	Large dataset

	1 <= C <= 10000.
	1 <= F <= 100.
	1 <= X <= 100000.

	Small input : 8 points	
	Large input : 11 points

   <span class="label label-warning">[Small Input File](https://gist.github.com/aakash01/10678230#file-b-small-attempt0)  </span>   <span class="label label-warning">   [Large Input File](https://gist.github.com/aakash01/10678230#file-b-large) </span>


<pre>
Sample
<table class="table">
<tr>
<td>Input</td>
<td>Output</td>
</tr>
 <tr>
 <td>
4
30.0 1.0 2.0
30.0 2.0 100.0
30.50000 3.14159 1999.19990
500.0 4.0 2000.0

</td>
<td>
Case #1: 1.0000000
Case #2: 39.1666667
Case #3: 63.9680013
Case #4: 526.1904762

</td>
</tr>
</table>
</pre>

##Hint 

This Question is pretty straightforward. 

At each step we will calculate two rates, 
1. Spend 500 Cookies and increase the rate and calcluate the time based on new rate , say T1
2. Calculate the time based on current rate without spending any cookies , Say T2
3. We will repeat step 1 & 2 untill T1 < T2

For Eg. 
<br />C=500.0, F=4.0 and X=2000.0
<br/> T1 = 500/2 (time to generate 500 cookies) + 2000/6 (rate increases by 4 ) =  583.33
<br/> T2 = 2000/2 = 1000 
<br/> as T1 is less than T2 we will repeat again,
<br/> T1 = 500/2 + 500/6 + 2000/10 = 533.33
<br/> T2 = 583.33 , Repeat again
<br/> T1 = 500/2 + 500/6 + 500/10 + 2000/14 = 142.87
<br/> T2 = 533.33



##Code (C++)


{% highlight cpp linenos %}
#include<iostream>
#include<cstdio>
#include<cstring>
#include<ctime>
#include<cmath>
#include <iomanip>

#define re
using namespace std;


int t;
double c, f, x;

double solve(double rate)
{

    double time = 0;
    while (true)
    {
        double r1 = x / rate;
        double r2 = c / rate + x / (rate + f);
        if (r1 > r2)
        {

            time += c / rate;
            rate = rate + f;
        }
        else
            return time + r1;

    }

    double r1 = x / rate;
    double r2 = c / rate + x / (rate + f);
    if (r1 > r2)
        return c / rate + solve(rate + f);
    else
        return r1;

}


int main(int argc, char const *argv[])
{
#ifdef re
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    freopen("log.txt", "w", stderr);
#endif

    cin >> t;
    for (int i = 1; i <= t; i++)
    {
        cin >> c >> f >> x;
        cout << "Case #" << i << ": " << std::setprecision(7) << fixed << solve(2) << endl;
    }

    /*#ifdef re
    printf("\n  Time Taken  %.31f sec\n",(double)clock()/(CLOCKS_PER_SEC));

    #endif*/
    return 0;
}
{% endhighlight %}
