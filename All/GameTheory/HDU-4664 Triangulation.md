---
title: HDU-4664	Triangulation
date: 2017-08-07 20:15:47
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=4664)

<!-- more -->

# HDU-4664 Triangulation



## Problem Description

>There are n points in a plane, and they form a convex set. 


> No, you are wrong. This is not a computational geometry problem. 


> Carol and Dave are playing a game with this points. (Why not Alice and Bob? Well, perhaps they are bored. ) Starting from no edges, the two players play in turn by drawing one edge in each move. Carol plays first. An edge means a line segment connecting two different points. The edges they draw cannot have common points. 


> To make this problem a bit easier for some of you, they are simutaneously playing on N planes. In each turn, the player select a plane and makes move in it. If a player cannot move in any of the planes, s/he loses. 
> 
Given N and all n's, determine which player will win. 


## Input

>First line, number of test cases, T. 
Following are 2*T lines. For every two lines, the first line is N; the second line contains N numbers, n 1, ..., n N. 

>Sum of all N <= 10^6. 
1<=n i<=10^9.

## Output

>T lines. If Carol wins the corresponding game, print 'Carol' (without quotes;) otherwise, print 'Dave' (without quotes.)


## Sample Input

>2
>
>1
>
>2

>2
>
>2 2


## Sample Output


> Carol
> 
> Dave


## 题意

>在N个棋盘上，每个棋盘上有ni个点。在棋盘上每个点进行连线，点不能重复选取。不能移动的输掉游戏。


## 思路

>这是一个SG题。对于一个有n个点的棋盘，每次划分都会使得它分为i个点和n-i-2个点的棋盘。故sg(x)=mex{sg[i]^sg[n-i-2]|0<=i<=n-2}

>答案即为这N个棋盘sg值异或所得答案是否为0。

>由于数据量很大，考虑找规律，发现在100以上（保险起见200以上）以34为周期。故选择在200以内打表，200以上靠规律。使用记忆化搜索大大加快运算速度。


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;
int vis[2000], sg[2000];
int mex(int x)
{
	if (sg[x] != -1)return sg[x];
	if (x == 0 || x == 1)return sg[x] = 0;
	if (x == 2 || x == 3)return  sg[x] = 1;

	memset(vis, 0, sizeof(vis));
	for (int i = 0; i < x - 1; i++)
		vis[mex(i) ^ mex(x - i - 2)] = true;
	for (int i = 0;; i++)
		if (!vis[i])
			return sg[x] = i;
}
int f(int x)
{
	if (x < 300)return mex(x);
	else
	{
		x %= 34;
		x += 34 * 4;
		return mex(x);
	}
}
int main()
{
	int T;
	cin >> T;
	memset(sg, -1, sizeof(sg));
	while (T--)
	{
		int n; cin >> n;
		int ans = 0, x;
		while (n--)
		{
			scanf("%d", &x);
			ans ^= f(x);
		}
		if (ans)puts("Carol");
		else puts("Dave");
	}
}
```