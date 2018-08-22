---
title: HDU-2147 kiki's game
date: 2017-08-08 20:48:35
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=2147)

<!-- more -->

# HDU-2147 kiki's game


## Problem Description

>Recently kiki has nothing to do. While she is bored, an idea appears in his mind, she just playes the checkerboard game.The size of the chesserboard is n*m.First of all, a coin is placed in the top right corner(1,m). Each time one people can move the coin into the left, the underneath or the left-underneath blank space.The person who can't make a move will lose the game. kiki plays it with ZZ.The game always starts with kiki. If both play perfectly, who will win the game?


## Input

>Input contains multiple test cases. Each line contains two integer n, m (0<n,m<=2000). The input is terminated when n=0 and m=0.


## Output

>If kiki wins the game printf "Wonderful!", else "What a pity!".

## Sample Input


> 5 3
> 
> 5 4
> 
> 6 6
> 
> 0 0



## Sample Output


> What a pity!

> Wonderful!

> Wonderful!

## 题意


>一个被放置在(n,m)位置的棋子，每次可以向左、下或左下移动一格。问先手输赢情况。


## 思路


>找规律发现n或m为偶必胜其余必败。


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
	int n, m;
	while (scanf("%d%d", &n, &m) == 2)
	{
		if (n == 0 && m == 0)break;
		if ((n % 2) == 0 || (m % 2) == 0)
			puts("Wonderful!");
		else puts("What a pity!");
	}
	return 0;
}

```