---
title: HDU-1564	Play a game
date: 2017-08-08 20:48:35
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=1564)

<!-- more -->

# HDU-1564	Play a game


## Problem Description

>New Year is Coming! 
>
ailyanlu is very happy today! and he is playing a chessboard game with 8600. 


> The size of the chessboard is n*n. A stone is placed in a corner square. They play alternatively with 8600 having the first move. Each time, player is allowed to move the stone to an unvisited neighbor square horizontally or vertically. The one who can't make a move will lose the game. If both play perfectly, who will win the game?


## Input

>The input is a sequence of positive integers each in a separate line. 
>
>The integers are between 1 and 10000, inclusive,(means 1 <= n <= 10000) indicating the size of the chessboard. The end of the input is indicated by a zero.


## Output

>Output the winner ("8600" or "ailyanlu") for each input line except the last zero. 
>
No other characters should be inserted in the output.

## Sample Input


> 2
> 0
> 


## Sample Output


> 8600

## 题意


>给你一个n*n的棋盘，棋子放在左上角，每轮它可以向上下左右移动，移动过得点不能再移动。问先手输赢状态。


## 思路


>找规律发现和奇偶有关（我猜测和n*n的奇偶有关，而n\*n的奇偶性和n的奇偶性一样）


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
	int n;
	while (scanf("%d", &n) == 1)
	{
		if (n == 0)return 0;
		if (n % 2)puts("ailyanlu");
		else puts("8600");
	}
}
```