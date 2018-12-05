---
title: HDU-1525 Euclid's Game
date: 2017-08-08 21:12:50
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=1525)

<!-- more -->

# HDU-1525 Euclid's Game


## Problem Description

> Two players, Stan and Ollie, play, starting with two natural numbers. Stan, the first player, subtracts any positive multiple of the lesser of the two numbers from the greater of the two numbers, provided that the resulting number must be nonnegative. Then Ollie, the second player, does the same with the two resulting numbers, then Stan, etc., alternately, until one player is able to subtract a multiple of the lesser number from the greater to reach 0, and thereby wins. For example, the players may start with (25,7): 
> 
> 25 7
> 
> 11 7
> 
> 4 7
> 
> 4 3
> 
> 1 3
> 
> 1 0 
> 
> an Stan wins. 
> 

> The size of the chessboard is n*n. A stone is placed in a corner square. They play alternatively with 8600 having the first move. Each time, player is allowed to move the stone to an unvisited neighbor square horizontally or vertically. The one who can't make a move will lose the game. If both play perfectly, who will win the game?


## Input

>The input consists of a number of lines. Each line contains two positive integers giving the starting two numbers of the game. Stan always starts.


## Output

>For each line of input, output one line saying either Stan wins or Ollie wins assuming that both of them play perfectly. The last line of input contains two zeroes and should not be processed. 

## Sample Input


> 34 12
> 
> 15 24
> 
> 0 0


## Sample Output

> Stan wins
> 
> Ollie wins

## 题意


>给你两个数a,b。每轮可以用大的数减去小的正整数倍（不能减到小于0），减到0的胜利。


## 思路


>对两个数a,b。若a==b先手必胜；对剩下的情况不妨设a>b，若a>2*b||a%b==0则必胜，后者是显然的，而前者可以将它改为(a,b)或(a,b-a)，这两者中必有一种是必败态。若b<a<2\*b则递推计算。


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
	int n, m;
	while (scanf("%d%d", &n, &m) == 2)
	{
		if (n == 0 & m == 0)break;
		if (m > n)swap(m, n);
		int sta = 0;
		while (m)
		{
			if (n%m == 0 || n > 2 * m)break;
			n = n - m;
			swap(n, m);
			sta ^= 1;

		}
		if (!sta) puts("Stan wins");
		else puts("Ollie wins");
	}
}
```