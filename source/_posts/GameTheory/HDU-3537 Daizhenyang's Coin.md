---
title: HDU-3537 Daizhenyang's Coin
date: 2017-08-07 20:15:47
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=3537)


<!-- more -->

# HDU-3537 Daizhenyang's Coin



## Problem Description

>We know that Daizhenyang is chasing a girlfriend. As we all know, whenever you chase a beautiful girl, there'll always be an opponent, or a rival. In order to take one step ahead in this chasing process, Daizhenyang decided to prove to the girl that he's better and more intelligent than any other chaser. So he arranged a simple game: Coin Flip Game. He invited the girl to be the judge. 
>
In this game, n coins are set in a row, where n is smaller than 10^8. They took turns to flip coins, to flip one coin from head-up to tail-up or the other way around. Each turn, one can choose 1, 2 or 3 coins to flip, but the rightmost selected must be head-up before flipping operation. If one cannot make such a flip, he lost. 
> 
> As we all know, Daizhenyang is a very smart guy (He's famous for his 26 problems and Graph Theory Unified Theory-Network Flow does it all ). So he will always choose the optimal strategy to win the game. And it's a very very bad news for all the competitors. 
> 
> But the girl did not want to see that happen so easily, because she's not sure about her feelings towards him. So she wants to make Daizhenyang lose this game. She knows Daizhenyang will be the first to play the game. Your task is to help her determine whether her arrangement is a losable situation for Daizhenyang. 
> 
> For simplicity, you are only told the position of head-up coins. And due to the girl's complicated emotions, the same coin may be described twice or more times. The other coins are tail-up, of course. 
> 
> Coins are numbered from left to right, beginning with 0. 

## Input

>Multiple test cases, for each test case, the first line contains only one integer n (0<=n<=100), representing the number of head-up coins. The second line has n integers a1, a2 … an (0<=ak<10^8) indicating the An-th coin is head up. 


## Output

>Output a line for each test case, if it's a losable situation for Daizhenyang can, print "Yes", otherwise output "No" instead. 


## Sample Input

> 0
> 
> 1
> 
> 0
> 
> 4
> 
> 0 1 2 3


## Sample Output

> Yes
> 
> No
> 
> Yes


## 题意

>有很多个硬币在桌上排列成一行，有n个数是正面朝上的，给出它们的坐标ai，问先手必胜还是必败。



## 思路

>各个位置的SG值异或就行了。SG(x)为除了位置x所有硬币向下的情况sg值。通过打表可发现sg(x)=2x(x的二进制表示中有奇数个1);sg(x)=2x+1(x的二进制表示中有偶数个1)。


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

int SG(int x)
{
	int tmp = x;
	int cnt = 0;
	while (tmp)
	{
		if (tmp & 1)cnt++;
		tmp >>= 1;
	}
	if (cnt & 1)return 2 * x;
	else return 2 * x + 1;
}

int a[110];

int main()
{
	int n;
	while (scanf("%d", &n) == 1)
	{
		for (int i = 0; i < n; i++)
			scanf("%d", &a[i]);
		sort(a, a + n);
		n = unique(a, a + n) - a;
		int sum = 0;
		for (int i = 0; i < n; i++)
			sum ^= SG(a[i]);
		if (sum)printf("No\n");
		else printf("Yes\n");
	}
	return 0;
}

```