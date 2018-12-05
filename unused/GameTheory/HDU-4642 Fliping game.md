---
title: HDU-4642	Fliping game
date: 2017-08-07 20:31:25
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=4642)

<!-- more -->

# HDU-4642 Fliping game



## Problem Description

>Alice and Bob are playing a kind of special game on an N*M board (N rows, M columns). At the beginning, there are N*M coins in this board with one in each grid and every coin may be upward or downward freely. Then they take turns to choose a rectangle (x1, y1)-(n, m) (1 ≤ x1≤n, 1≤y1≤m) and flips all the coins (upward to downward, downward to upward) in it (i.e. flip all positions (x, y) where x1≤x≤n, y1≤y≤m)). The only restriction is that the top-left corner (i.e. (x1, y1)) must be changing from upward to downward. The game ends when all coins are downward, and the one who cannot play in his (her) turns loses the game. Here's the problem: Who will win the game if both use the best strategy? You can assume that Alice always goes first.

## Input

>The first line of the date is an integer T, which is the number of the text cases.
Then T cases follow, each case starts with two integers N and M indicate the size of the board. Then goes N line, each line with M integers shows the state of each coin, 1<=N,M<=100. 0 means that this coin is downward in the initial, 1 means that this coin is upward in the initial.

## Output

>For each case, output the winner’s name, either Alice or Bob.
>
## Sample Input

> 2
> 

> 2 2

> 1 1

> 1 1

> 3 3

> 0 0 0

> 0 0 0

> 0 0 0


## Sample Output


> Alice
> 
> Bob


## 题意

>给你一张二维图表示硬币哪面朝上，每次翻只能翻(x,y)-(n,m)且x,y递增。问先手输赢情况。

## 思路


>找规律发现答案仅和右下角那个数有关--为一Alice必胜，否则Bob胜。


## 代码

```cpp

#include<bits/stdc++.h>
using namespace std;

int main()
{
	int T;
	cin >> T;
	while (T--)
	{
		int n, m, a;
		cin >> n >> m;
		for (int i = 0; i < n; i++)
			for (int j = 0; j < m; j++)
				scanf("%d", &a);
		if (a)puts("Alice");
		else puts("Bob");
	}
}
