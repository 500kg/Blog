---
title: HDU-6198 number number number
tags: [斐波那契数列]
categories: [数论]
date: 2017-09-10 23:07:56
---

[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=6198)

<!-- more -->

# HDU-6198 number number number

## Problem Description

> We define a sequence F:

>⋅ F0=0,F1=1;
>
>⋅ Fn=Fn−1+Fn−2 (n≥2).

>Give you an integer k, if a positive number n can be expressed by n=Fa1+Fa2+...+Fak where 0≤a1≤a2≤⋯≤ak, this positive number is mjf−good. Otherwise, this positive number is mjf−bad.
>
>Now, give you an integer k, you task is to find the minimal positive mjf−bad number.
>
>The answer may be too large. Please print the answer modulo 998244353.

## Input

>There are about 500 test cases, end up with EOF.
Each test case includes an integer k which is described above. (1≤k≤1000000000)

## Output

>For each case, output the minimal mjf−bad number mod 998244353.

## Sample Input

>1

## Sample Output

>4

# 题解

## 题意

说是给你一个K，问最小的不能用K个斐波那契数之和表示的数是什么。

## 思路

>拉神推了个公式：ans(k)=f(2)+f(4)+···+f(2k+2)

>大意是能用k+1个斐波那契数之和表示而不能用k个斐波那契数表示的数就是上面的那个式子。

>可以用归纳法证明其正确性。

>然后加个f(1)再减个1可以把这个公式改成ans(k)=f(2k+3)-1

>如此便可以运用矩阵快速幂在log(k)的时间中求出答案了。

## 代码

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int mod = 998244353;
typedef vector<ll> vec;
typedef vector<vec> mat;
mat mul(mat &a, mat &b)
{
	mat c(a.size(), vec(b[0].size()));
	for (int i = 0; i<2; i++)
	{
		for (int j = 0; j<2; j++)
		{
			for (int k = 0; k<2; k++)
			{
				c[i][j] += a[i][k] * b[k][j];
				c[i][j] %= mod;
			}
		}
	}
	return c;
}
mat pow(mat a, ll n)
{
	mat res(a.size(), vec(a.size()));
	for (int i = 0; i<a.size(); i++)
		res[i][i] = 1;//单位矩阵；  
	while (n)
	{
		if (n & 1) res = mul(res, a);
		a = mul(a, a);
		n /= 2;
	}
	return res;
}
ll solve(ll n)
{
	mat a(2, vec(2));
	a[0][0] = 1;
	a[0][1] = 1;
	a[1][0] = 1;
	a[1][1] = 0;
	a = pow(a, n);
	return a[0][1];//也可以是a[1][0];  
}
int main()
{
	ll n;
	while (cin >> n)
	{
		cout << solve(2 * n + 3) - 1 << endl;
	}
	return 0;
}
```