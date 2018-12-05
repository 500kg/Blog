---
title: HDU-5510 Bazinga
tags: [KMP]
categories: [字符串]
date: 2017-09-13 22:42:48
---

[传送门](http://acm.hdu.edu.cn/showproblem.php?pid=5510)

<!-- more -->

# HDU-5510 Bazinga

## Problem Description

>Ladies and gentlemen, please sit up straight. 
Don't tilt your head. I'm serious. 


>For nn given strings S1,S2,⋯,Sn labelled from 1 to n, you should find the largest i (1≤i≤n) such that there exists an integer j (1≤j<i) and Sj is not a substring of SiSi. 

>A substring of a string SiSi is another string that occurs in Si. For example, "ruiz" is a substring of "ruizhang", and "rzhang" is not a substring of "ruizhang".

## Input

>The first line contains an integer t (1≤t≤50)which is the number of test cases. 

>For each test case, the first line is the positive integer n (1≤n≤500) and in the following nn lines list are the strings S1,S2,⋯,Sn. 

>All strings are given in lower-case letters and strings are no longer than 2000 letters.

## Output

>For each test case, output the largest label you get. If it does not exist, output −1.

## Sample Input

>4
>
>5

>ab
>
>abc
>
>zabc
>
>abcd
>
>zabcd
>
>4
>
>you
>
>lovinyou
>
>aboutlovinyou
>
>allaboutlovinyou
>
>5
>
>de
>
>def
>
>abcd
>
>abcde
>
>abcdef
>
>3
>
>a
>
>ba
>
>ccc

## Sample Output

>Case #1: 4
>
>Case #2: -1
>
>Case #3: 4
>
>Case #4: 3

# 题解

## 题意

>给你n个字符串，编号从1开始有小到大编号。求最大的字符串编号i,满足存在1<=j<i，字符串j不是i的子串。

## 思路

>思考：
>
>假如字符串Sx是字符串Sy的子串，那么对于任何字符串St:若Sx是St的子串，Sy却不一定是St的子串；而如果Sy是St的子串，Sx一定是St的子串。

>有了如上结论后我们可以得出结论：如果字符串Sx是字符串Sy的子串，那么在接下来的字符串匹配中，我们不需要匹配Sx而只需要观察Sy的匹配结果即可。

>通过如上思路的优化，我们使用KMP可以AC这道题。但对于一系列各不为子串的字符串，我们将会TLE。（数据不够强）

>为避免如上错误，我们在失配之后直接Break。

>（代码是WF写的，优化二是SF提出来的，这篇博客是我强行写的）

## 代码
```
/*
教练我要打ACM!
*/
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef long double ld;

const int inf = 0x3f3f3f3f;
const int maxn = 3000 + 20;

int fail[maxn];
void get_fail(const string& t) {
  fail[0] = -1;
  int n = t.size();
  int j = 0;
  int k = -1;
  while (j < n) {
    if (k == -1 || t[j] == t[k]) {
      fail[++j] = ++k;
    } else {
      k = fail[k];
    }
  }
}
int KMP(const string& s, const string& t) {
  get_fail(t);
  int sn = s.size();
  int tn = t.size();
  int i = 0;
  int j = 0;
  while (i < sn && j < tn) {
    if (j == -1 || s[i] == t[j]) {
      ++i; ++j;
    } else {
      j = fail[j];
    }
  }
  if (j == tn) return i - tn + 1;
  else return -1;
}
bool vis[maxn];
int main() {
  // freopen("/home/wfgu/solve/data.in", "r", stdin);
  ios::sync_with_stdio(false);
  cin.tie(0);

  int T;
  cin >> T;
  vector<string> belly;
  for (int cas = 1; cas <= T; ++cas) {
    belly.clear();
    int n;
    cin >> n;
    string str;
    for (int i = 0; i < n; ++i) {
      cin >> str;
      belly.push_back(str);
    }
    memset(vis, 0, sizeof(vis));
    int ret = -1;
    for (int i = 0; i < n; ++i) {
      for (int j = 0; j < i; ++j) {
        if (vis[j]) continue;
        if (KMP(belly[i], belly[j]) == -1) {
          ret = i + 1;
          break;
        } else {
          vis[j] = true;
        }
      }
    }
    cout << "Case #" << cas << ": " << ret << endl;
  }
  return 0;
}
```