---
title: HDU-1850 Being a Good Boy in Spring Festival
date: 2017-08-08 21:12:52
tags: [博弈]
categories: [博弈]
---
[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=1850)

<!-- more -->

# HDU-1850 Being a Good Boy in Spring Festival


## Problem Description

> 一年在外 父母时刻牵挂 
> 
> 春节回家 你能做几天好孩子吗 
> 
> 寒假里尝试做做下面的事情吧 
> 
> 陪妈妈逛一次菜场 
> 
> 悄悄给爸爸买个小礼物 
> 
> 主动地 强烈地 要求洗一次碗 
> 
> 某一天早起 给爸妈用心地做回早餐 
> 
> 如果愿意 你还可以和爸妈说 
> 
> 咱们玩个小游戏吧 ACM课上学的呢～ 
> 
> 下面是一个二人小游戏：桌子上有M堆扑克牌；每堆牌的数量分别为Ni(i=1…M)；两人轮流进行；每走一步可以任意选择一堆并取走其中的任意张牌；桌子上的扑克全部取光，则游戏结束；最后一次取牌的人为胜者。 
> 现在我们不想研究到底先手为胜还是为负，我只想问大家： 
> 
> ——“先手的人如果想赢，第一步有几种选择呢？” 

## Input

>输入数据包含多个测试用例，每个测试用例占2行，首先一行包含一个整数M(1<M<=100)，表示扑克牌的堆数，紧接着一行包含M个整数Ni(1<=Ni<=1000000，i=1…M)，分别表示M堆扑克的数量。M为0则表示输入数据的结束。


## Output

>如果先手的人能赢，请输出他第一步可行的方案数，否则请输出0，每个实例的输出占一行。 

## Sample Input

> 3
> 
> 5 7 9
> 
> 0

## Sample Output

> 1


## 题意


>中文题面啊~~


## 思路


>NIM博弈，需要考虑的是必胜态有几种转移至必败态的选择。

>对a1^a2^a3····^an=k(k!=0)

>若ai-k^ai>0则可以通过减少ai至某一值使得总的异或为0（即必败态）


## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;
int a[1000006];
int main()
{
	int n;
	while (scanf("%d", &n) == 1 && n)
	{
		int sum = 0;
		for (int i = 0; i < n; i++)
		{
			scanf("%d", a + i);
			sum ^= a[i];
		}
		if (sum == 0)
		{
			puts("0");
			continue;
		}
		int cnt = 0;
		for (int i = 0; i < n; i++)
			if (a[i] >( sum^a[i]))
				cnt++;
		cout << cnt << endl;
	}
}
```