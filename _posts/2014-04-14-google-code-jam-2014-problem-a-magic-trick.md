---
layout: post
title: "Google Code Jam 2014: Problem A. Magic Trick"
description: ""
category: 
tags: []
---
{% include JB/setup %}


#Problem

	Recently you went to a magic show. You were very impressed by one of the tricks, so you decided to try to figure out the secret behind it!

	The magician starts by arranging 16 cards in a square grid: 4 rows of cards, with 4 cards in each row. Each card has a different number from 1 to 16 written on the side that is showing. Next, the magician asks a volunteer to choose a card, and to tell him which row that card is in.

	Finally, the magician arranges the 16 cards in a square grid again, possibly in a different order. Once again, he asks the volunteer which row her card is in. With only the answers to these two questions, the magician then correctly determines which card the volunteer chose. Amazing, right?

	You decide to write a program to help you understand the magician's technique. The program will be given the two arrangements of the cards, and the volunteer's answers to the two questions: the row number of the selected card in the first arrangement, and the row number of the selected card in the second arrangement. The rows are numbered 1 to 4 from top to bottom.

	Your program should determine which card the volunteer chose; or if there is more than one card the volunteer might have chosen (the magician did a bad job); or if there's no card consistent with the volunteer's answers (the volunteer cheated).

	Input

	The first line of the input gives the number of test cases, T. T test cases follow. Each test case starts with a line containing an integer: the answer to the first question. The next 4 lines represent the first arrangement of the cards: each contains 4 integers, separated by a single space. The next line contains the answer to the second question, and the following four lines contain the second arrangement in the same format.

	Output

	For each test case, output one line containing "Case #x: y", where x is the test case number (starting from 1).

	If there is a single card the volunteer could have chosen, y should be the number on the card. If there are multiple cards the volunteer could have chosen, y should be "Bad magician!", without the quotes. If there are no cards consistent with the volunteer's answers, y should be "Volunteer cheated!", without the quotes. The text needs to be exactly right, so consider copying/pasting it from here.

	Limits

	1 <= T <= 100.
	1 <= both answers <= 4.
	Each number from 1 to 16 will appear exactly once in each arrangement.

	Small input : 6 points
   [Small Input File](https://gist.github.com/aakash01/10649363)

<pre>
Sample
<table class="table">
<tr>
<td>Input</td>
<td>Output</td>
</tr>
 <tr>
 <td>
3
2
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
3
1 2 5 4
3 11 6 15
9 10 7 12
13 14 8 16
2
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
2
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
2
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
3
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16

</td>
<td>
Case #1: 7
Case #2: Bad magician!
Case #3: Volunteer cheated!
</td>
</tr>
</table>
</pre>


##Hint

This problem was simplest problem in GCJ 2014 qualification round. 

Simple Algorithm
1. Maintain two array A and B of size 4 each
2. Array A will contain the numbers present in selected row of Grid 1.
3. Array B will contain the numbers present in selected row of Grid 2.
4. Traverse both array and find the common numbers between them
	1. If both arrays are distinct , return `Volunteer cheated!`.
	2. If multiple found , return `Bad magician!`
	3. Else return the common number. 


Solution i submitted in gcj: 

#### Code (Java)

 
{% highlight cpp linenos %}
#include<iostream>
#include<cstdio>
#include<cstring>
#include<ctime>
#include<cmath>

#define re
using namespace std;


int t;
int a1, b1;
int a[4];
int b[4];

void solve(int case_no)
{

    bool isFound = false;
    bool isMultiple = false;
    int card_no = -1;



    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 4; j++)
        {
            if (a[i] == b[j])
            {
                if (card_no != -1)
                {
                    isMultiple = true;
                }
                isFound = true;
                card_no = a[i];
            }
        }

    cout << "Case #" << case_no << ": ";

    if (isMultiple)
        cout << "Bad magician!";
    else if (!isFound)
        cout << "Volunteer cheated!";
    else
        cout << card_no;
    cout << endl;

}


int main(int argc, char const *argv[])
{
#ifdef re
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    freopen("log.txt", "w", stderr);
#endif

    cin >> t;
    int temp;
    for (int j = 1; j <= t; j++)
    {
        cin >> a1;

        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (i == a1 - 1)
                    cin >> a[j];
                else
                    cin >> temp;
            }
        }
        cin >> b1;
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (i == b1 - 1)
                    cin >> b[j];
                else
                    cin >> temp;
            }
        }
        solve(j);
    }

    /*#ifdef re
    printf("\n  Time Taken  %.31f sec\n",(double)clock()/(CLOCKS_PER_SEC));

    #endif*/
    return 0;
}

{% endhighlight %}
