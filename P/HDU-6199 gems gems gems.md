---
title: HDU-6199 gems gems gems
tags: [DP]
categories: [DP]
date: 2017-09-10 23:18:53
---

[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=6199)

<!-- more -->

# HDU-6199 gems gems gems

## Problem Description

>Now there are n gems, each of which has its own value. Alice and Bob play a game with these n gems.
>
They place the gems in a row and decide to take turns to take gems from left to right. 

>Alice goes first and takes 1 or 2 gems from the left. After that, on each turn a player can take k or k+1 gems if the other player takes k gems in the previous turn. The game ends when there are no gems left or the current player can't take k or k+1 gems.
>
>Your task is to determine the difference between the total value of gems Alice took and Bob took. Assume both players play optimally. Alice wants to maximize the difference while Bob wants to minimize it.


## Input

>The first line contains an integer T (1≤T≤10), the number of the test cases. 
>
>For each test case:
>
>the first line contains a numbers n (1≤n≤20000);
the second line contains n numbers: V1,V2…Vn. (−100000≤Vi≤100000)

## Output

>For each test case, print a single number in a line: the difference between the total value of gems Alice took and the total value of gems Bob took.


## Sample Input


>1
>
>3
>
>1 3 2


## Sample Output

>4

# 题解

## 题意

>有一列最多20000个宝石，每个宝石都有各自的权值。每轮都必须从左往右依次拿k或k+1个宝石，其中k是上一轮对方所拿宝石个数。

>Alice先行动，可以拿一或两个宝石。

## 思路

>一开始就想到是个DP，然而到最后也没做出来，WA到是没WA，不过TLE和MLE了不少。

>赛后用别人AC代码跑出来的数据和自己手算的不一样，发现自己题意理解错了：

>本题中difference指 Alice所取的宝石价值之和-Bob所取宝石价值之和。

>（比赛的时候瞎改改还心态崩了）

## 代码

```
#include<bits/stdc++.h>
using namespace std;
const int maxn = 20050;
int n;
int s[maxn], Sum[maxn];
int dp[2][300][300];
const int mod = 255;
int main()
{
	int T;
	scanf("%d", &T);
	while (T--)
	{
		scanf("%d", &n);
		memset(dp, 0, sizeof(dp));
		Sum[0] = 0;
		for (int i = 1; i <= n; i++)
		{
			scanf("%d", &s[i]);
			Sum[i] = Sum[i - 1] + s[i];
		}
		int size = sqrt(n * 2) + 1;
		for (int i = n; i >= 1; i--)
		{
			for (int j = size; j >= 1; j--)
			{
				if (i + j <= n)
				{
					dp[0][i&mod][j] = Sum[(i + j - 1)] - Sum[i - 1] + max(dp[1][(i + j)&mod][j], dp[1][(i + j + 1)&mod][j + 1] + s[i + j]);
					dp[1][i&mod][j] = -Sum[i + j - 1] + Sum[i - 1] + min(dp[0][(i + j)&mod][j], dp[0][(i + j + 1)&mod][j + 1] - s[i + j]);
				}
				else if (i + j == n + 1)
				{
					dp[0][i&mod][j] = Sum[i + j - 1] - Sum[i - 1] + dp[1][(i + j)&mod][j];
					dp[1][i&mod][j] = Sum[i - 1] - Sum[i + j - 1] + dp[0][(i + j)&mod][j];
				}
			}
		}
		printf("%d\n", dp[0][1][1]);
	}


}

```