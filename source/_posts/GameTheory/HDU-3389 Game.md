---
title: HDU-3389 Game
date: 2017-08-07 20:23:23
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=3389)

<!-- more -->

# HDU-3389 Game


## Problem Description
>Bob and Alice are playing a new game. There are n boxes which have been numbered from 1 to n. Each box is either empty or contains several cards. Bob and Alice move the cards in turn. In each turn the corresponding player should choose a non-empty box A and choose another box B that B<A && (A+B)%2=1 && (A+B)%3=0. Then, take an arbitrary number (but not zero) of cards from box A to box B. The last one who can do a legal move wins. Alice is the first player. Please predict who will win the game.

## Input

>The first line contains an integer T (T<=100) indicating the number of test cases. The first line of each test case contains an integer n (1<=n<=10000). The second line has n integers which will not be bigger than 100. The i-th integer indicates the number of cards in the i-th box.

## Output

>For each test case, print the case number and the winner's name in a single line. Follow the format of the sample output.

## Sample Input


> 2

> 2

> 1 2

> 7

> 1 3 3 2 2 1 2

## Sample Output


> Case 1: Alice
> 
> Case 2: Bob
## 题意

>有n个盒子，编号为1~n，每个盒子有ai个卡片。每轮挑一个盒子A和B，要求B<A && (A+B)%2=1 && (A+B)%3=0 ;将A中任意卡牌放入B中。无法行动的将输掉比赛。

## 思路（抄kuangbin的）

>1. 分成一个二分图
如果可以从A拿卡片到B，连一条从A到B的边。把所有box编号x满足（(x%
3==0&&x%2==1) || x%3==1)这个条件的放左边，其他放右边，不难发现
a) 只有从左边到右边的边或从右到左的边。
b) 所有不能拿卡片出去的box都在左边。
2. 证明左边的box并不影响结果。假设当前从右边的局势来看属于输家的人为了
摆脱这种局面，从左边的某盒子A拿了n张卡片到B，因为B肯定有出去的边，对手
会从B再取走那n张卡片到左边，局面没有变化
3. 于是这就相当于所有右边的box在nim游戏。

## 代码

```cpp

#include<bits/stdc++.h>
using namespace std;

int main()
{
	int kase = 0;
	int T;
	cin >> T;
	while (T--)
	{
		int n; cin >> n;
		int ans = 0;
		for (int i = 1; i <= n; i++)
		{
			int a;
			cin >> a;
			if ((i % 2 == 0 && i % 3 == 0) || i % 3 == 2)
				ans ^= a;
		}
		if (ans)printf("Case %d: Alice\n", ++kase);
		else printf("Case %d: Bob\n", ++kase);
	}
}

```