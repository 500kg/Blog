---
title: HDU-4764	Stone
date: 2017-08-07 20:15:47
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=4764)

<!-- more -->

# HDU-4764	Stone



## Problem Description

>Tang and Jiang are good friends. To decide whose treat it is for dinner, they are playing a game. Specifically, Tang and Jiang will alternatively write numbers (integers) on a white board. Tang writes first, then Jiang, then again Tang, etc... Moreover, assuming that the number written in the previous round is X, the next person who plays should write a number Y such that 1 <= Y - X <= k. The person who writes a number no smaller than N first will lose the game. Note that in the first round, Tang can write a number only within range [1, k] (both inclusive). You can assume that Tang and Jiang will always be playing optimally, as they are both very smart students.


## Input

>There are multiple test cases. For each test case, there will be one line of input having two integers N (0 < N <= 10^8) and k (0 < k <= 100). Input terminates when both N and k are zero.


## Output

>For each case, print the winner's name in a single line.


## Sample Input

>1 1
>
>30 3
>
>10 2
>
>0 0


## Sample Output


> Jiang
> 
> Tang
> 
> Jiang


## 题意


>给出n和k，每个人写的数必须必前一个人大[1,k]，第一个人写的数也属于[1,k]，问先手输赢情况


## 思路


>博弈入门题，判断(n-1)%(k+1)是否为0即可


## 代码


```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
	int n, m;
	while (~scanf("%d%d", &n, &m))
	{
		if (n == 0 && m == 0)break;
		if ((n - 1) % (m + 1))
			puts("Tang");
		else
			puts("Jiang");
	}

}
```