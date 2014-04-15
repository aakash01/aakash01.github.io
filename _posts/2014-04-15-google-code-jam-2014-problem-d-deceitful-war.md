---
layout: post
title: "Google Code Jam 2014: Problem D. Deceitful War"
description: ""
category: 
tags: []
---
{% include JB/setup %}

##Problem

	Naomi and Ken sometimes play games together. Before they play, each of them gets N identical-looking blocks of wood with masses between 0.0kg and 1.0kg (exclusive). All of the blocks have different weights. There are lots of games they could play with those blocks, but they usually play something they call War. Here is how War works:

	a. Each player weighs each of his or her own blocks, so each player knows the weights of all of his or her own blocks, but not the weights of the other player's blocks.
	b. They repeat the following process N times:
		1. Naomi chooses one of her own blocks, with mass ChosenNaomi.
		2. Naomi tells Ken the mass of the block she chose.
		3. Ken chooses one of his own blocks, with mass ChosenKen.
		4. They each put their block on one side of a balance scale, and the person whose block is heavier gets one point.
		5. Both blocks are destroyed in a fire.
	Naomi has realized three things about War. First, she has realized that she loses a lot. Second, she has realized that there is a unique strategy that Ken can follow to maximize his points without assuming anything about Naomi's strategy, and that Ken always uses it. Third, she has realized that she hates to lose. Naomi has decided that instead of playing War, she will play a game she calls Deceitful War. The great thing about Deceitful War is that Ken will think they're playing War!

	Here is how Deceitful War works, with differences between Deceitful War and War in bold:

	a. Each player weighs each of his or her own blocks. <b> Naomi also weighs Ken's blocks while he isn't looking, so Naomi knows the weights of all blocks </b> and Ken only knows the weights of his own blocks.
	b. They repeat the following process N times:
		1. Naomi chooses one of her own blocks, with mass ChosenNaomi.
		2. Naomi tells Ken a number, ToldNaomi, between 0.0kg and 1.0kg exclusive. Ken, who thinks they're playing War, thinks the number Naomi just told him is ChosenNaomi.
		3. Ken chooses one of his own blocks, with mass ChosenKen.
		4.They each put their block on one side of a balance scale, and the person whose block is heavier gets one point.
		5.Both blocks are destroyed in a fire.
	Naomi doesn't want Ken to know that she isn't playing War; so when she is choosing which block to play, and what mass to tell Ken, she must make sure that the balance scale won't reveal that ChosenNaomi is not equal to( <>) ToldNaomi. In other words, she must make decisions so that:

		* ChosenNaomi > ChosenKen if, and only if, ToldNaomi > ChosenKen, and
		* ToldNaomi is not equal to the mass of any of Ken's blocks, because he knows that isn't possible.
	It might seem like Naomi won't win any extra points by being deceitful, because Ken might discover that she wasn't playing War; but Naomi knows Ken thinks both players are playing War, and she knows what he knows, and she knows Ken will always follow his unique optimal strategy for War, so she can always predict what he will play.

	You'll be given the masses of the blocks Naomi and Ken started with. Naomi will play Deceitful War optimally to gain the maximum number of points. Ken will play War optimally to gain the maximum number of points assuming that both players are playing War. What will Naomi's score be? What would it have been if she had played War optimally instead?

	Examples

	If each player has a single block left, where Naomi has 0.5kg and Ken has 0.6kg, then Ken is guaranteed to score the point. Naomi can't say her number is >= 0.6kg, or Ken will know she isn't playing War when the balance scale shows his block was heavier.

	If each player has two blocks left, where Naomi has [0.7kg, 0.2kg] and Ken has [0.8kg, 0.3kg], then Naomi could choose her 0.2kg block, and deceive Ken by telling him that she chose a block that was 0.6kg. Ken assumes Naomi is telling the truth (as in how the War game works) and will play his 0.8kg block to score a point. Ken was just deceived, but he will never realize it because the balance scale shows that his 0.8kg block is, like he expected, heavier than the block Naomi played. Now Naomi can play her 0.7kg block, tell Ken it is 0.7kg, and score a point. If Naomi had played War instead of Deceitful War, then Ken would have scored two points and Naomi would have scored zero.

	Input

	The first line of the input gives the number of test cases, T. T test cases follow. Each test case starts with a line containing a single integer N, the number of blocks each player has. Next follows a line containing N space-separated real numbers: the masses of Naomi's blocks, in kg. Finally there will be a line containing N space-separated real numbers: the masses of Ken's blocks, in kg.

	Each of the masses given to Ken and Naomi will be represented as a 0, followed by a decimal point, followed by 1-5 digits. Even though all the numbers in the input have 1-5 digits after the decimal point, Ken and Naomi don't know that; so Naomi can still tell Ken that she played a block with mass 0.5000001kg, and Ken has no reason not to believe her.

	Output

	For each test case, output one line containing "Case #x: y z", where x is the test case number (starting from 1), y is the number of points Naomi will score if she plays Deceitful War optimally, and z is the number of points Naomi will score if she plays War optimally.

	Limits

	1 <= T <= 50.
	All the masses given to Ken and Naomi are distinct, and between 0.0 and 1.0 exclusive.
	Small dataset

	1 <= N <= 10.

	Large dataset

	1 <= N <= 1000.

	Small input : 14 points	
	Large input : 16 points
	
<span class="label label-warning">[Small Input File](https://gist.github.com/aakash01/10701095#file-gcj14-d-small-attempt0)  </span>   <span class="label label-warning">   [Large Input File](https://gist.github.com/aakash01/10701095#file-gcj14-d-large) </span>


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
1
0.5
0.6
2
0.7 0.2
0.8 0.3
3
0.5 0.1 0.9
0.6 0.4 0.3
9
0.186 0.389 0.907 0.832 0.959 0.557 0.300 0.992 0.899
0.916 0.728 0.271 0.520 0.700 0.521 0.215 0.341 0.458


</td>
<td>
Case #1: 0 0
Case #2: 1 0
Case #3: 2 1
Case #4: 8 4
</td>
</tr>
</table>
</pre>

##Hint


####Optimal Strategy to play 'War'
1. At each step Naomi will tell the lightest block she have .
2. Ken will find a block just heavier than the ChosenNaomi
3. We will repeat this step untill we are not able to find a suitable block for ken . The Remaining blocks indicate that the weights of Naomi-Blocks > weights of Ken-blocks


####Optimal Strategy to play 'Deceitful War'

For Deceitful War we have to 2 cases 

1. Naomi have lightest block 
	<br/> In this case we are sure that Naomi is going to loose so at least we should take out the heaviest block of ken. For this we will call a number just lower than ken's heaviest block. Ken will play heaviest and Naomi will play lightest 
2. Naomi doesn't have lightest block 
	<br/> Naomi doesn't have lightest block means ken is having block which is lighter than Naomi block , so when we Naomi will play that block we have to make sure that Ken will play lighter block . So Naomi will call a weight which is larger than all of ken's weights , As Ken is plying optimally he will play the lightest block and Naomi will play the block heavier than Ken's block

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


int t, n;
double *naomi, *ken, *temp_ken;

void swap(double *a, int i , int j)
{
    double temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}

void qsort(double *a, int left, int right)
{
    int i, last;

    if (left >= right)
        return;
    swap(a, left, (left + right) / 2);
    last = left;
    for (i = left + 1; i <= right; i++)
        if (a[i] < a[left])
            swap(a, ++last, i);
    swap(a, left, last);

    qsort(a, left, last - 1);
    qsort(a, last + 1, right);
}

void solve(int case_no)
{

    qsort(naomi, 0, n - 1);
    qsort(ken, 0, n - 1);

    qsort(temp_ken, 0, n - 1);


    int naomi_decietful_win = 0;
    int naomi_fair_win = n;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if ( ken[j] != -1)
            {
                if (naomi[i] > ken[j])
                {
                    naomi_decietful_win++;
                    ken[j] = -1;
                }
                else if (naomi[i] < ken[j])
                {
                    for (int k = n - 1; k >= 0; k--)
                    {
                        if (ken[k] != -1)
                        {
                            ken[k] = -1;
                            break;
                        }
                    }
                }
                break;
            }
        }

    }

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (temp_ken[j] != -1)
            {
                if (temp_ken[j] > naomi[i])
                {
                    temp_ken[j] = -1;
                    naomi_fair_win--;
                    break;
                }
            }

        }

    }
    cout << "Case #" << case_no << ": " << naomi_decietful_win << " " << naomi_fair_win << endl;


}


int main(int argc, char const *argv[])
{
#ifdef re
    freopen("input.txt", "r", stdin);
    freopen("output_max.txt", "w", stdout);
    freopen("log.txt", "w", stderr);
#endif

    cin >> t;
    for (int j = 1; j <= t; j++)
    {
        cin >> n;
        naomi = new double[n];
        ken = new double[n];
        temp_ken = new double[n];
        for (int i = 0; i < n; i++)
        {
            cin >> naomi[i];
        }
        for (int i = 0; i < n; i++)
        {
            cin >> ken[i];
            temp_ken[i] = ken[i];
        }

        solve(j);
    }

    /*#ifdef re
    printf("\n  Time Taken  %.31f sec\n",(double)clock()/(CLOCKS_PER_SEC));

    #endif*/
    return 0;
}

{% endhighlight %}