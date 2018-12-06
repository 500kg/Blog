---
title: 博弈-SG函数与SG定理
date: 2017-08-05 21:01:18
tags: [博弈]
categories: [博弈]
mathjax: true
---
&emsp;&emsp;简单一点的博弈就是必胜点与必败点（NP），对于复杂一点的就需要用到SG函数了。

<!-- more -->

[博弈知识汇总](http://www.cnblogs.com/kuangbin/archive/2011/08/28/2156426.html)
[博弈中的异或](http://blog.csdn.net/hndu__lz/article/details/61925818)

在介绍SG前我们先来看一下必胜点与必败点吧。

# 一、必胜点与必败点

必胜点和必败点的概念：
> 
>&emsp;&emsp;P点：必败点，换而言之，就是谁处于此位置，则在双方操作正确的情况下必败。      
>&emsp;&emsp;N点：必胜点，处于此情况下，双方操作均正确的情况下必胜。
>必胜点和必败点的性质：
> 
>&emsp;&emsp;1、所有终结点是必败点P。（我们以此为基本前提进行推理，换句话说，我们以此为假设）
>         
>&emsp;&emsp;2、从任何必胜点N操作，至少有一种方式可以进入必败点P。
>         
>&emsp;&emsp;3、无论如何操作必败点P都只能进入必胜点N。

我们以[hdu 1847 Good Luck in CET-4 Everybody!](http://acm.hdu.edu.cn/showproblem.php?pid=1847)为例：

> 当 n = 0 时，显然为必败点，因为此时你已经无法进行操作了
> 
> 当 n = 1 时，因为你一次就可以拿完所有牌，故此时为必胜点
> 
> 当 n = 2 时，也是一次就可以拿完，故此时为必胜点
> 
> 当 n = 3 时，要么就是剩一张要么剩两张，无论怎么取对方都将面对必胜点，故这一点为必败点。

通过打表我们可以找到一定的规律，从而使其迎刃而解。

# 二、SG函数与SG定理

对于一个更加复杂些的题目如[hdu 2147 kiki's game](http://acm.hdu.edu.cn/showproblem.php?pid=2147)我们无法使用P/N解决它。但是有一种新工具，可以使组合问题变得简单————SG函数和SG定理。

SG函数：
>&emsp;&emsp;首先定义mex(minimal excludant)运算，这是施加于一个集合的运算，表示最小的不属于这个集合的非负整数。例如mex{0,1,2,4}=3、mex{2,3,5}=0、mex{}=0。
> 
>&emsp;&emsp;对于任意状态 x ， 定义 SG(x) = mex(S),其中 S 是 x 后继状态的SG函数值的集合。如 x 有三个后继状态分别为 SG(a),SG(b),SG(c)，那么SG(x) = mex{SG(a),SG(b),SG(c)}。 这样 集合S 的终态必然是空集，所以SG函数的终态为 SG(x) = 0,当且仅当 x 为必败点P时。即SG[x] = 0时为败态，非0时为胜态。

取石子问题

有1堆n个的石子，每次只能取{ 1, 3, 4 }个石子，先取完石子者胜利，那么各个数的SG值为多少？

> SG[0]=0;
> 
> x=1 时，可以取走1 - f{1}个石子，剩余{0}个，所以 SG[1] = mex{ SG[0] }= mex{0} = 1;
> 
> x=2 时，可以取走2 - f{1}个石子，剩余{1}个，所以 SG[2] = mex{ SG[1] }= mex{1} = 0;
> 
> x=3 时，可以取走3 - f{1,3}个石子，剩余{2,0}个，所以 SG[3] = mex{SG[2],SG[0]} = mex{0,0} =1;
> 
> x=4 时，可以取走4-  f{1,3,4}个石子，剩余{3,1,0}个，所以 SG[4] = mex{SG[3],SG[1],SG[0]} = mex{1,1,0} = 2;
> 
> x=5 时，可以取走5 - f{1,3,4}个石子，剩余{4,2,1}个，所以SG[5] = mex{SG[4],SG[2],SG[1]} =mex{2,0,1} = 3;

## 代码如下
```cpp
//f[N]:可改变当前状态的方式，N为方式的种类，f[N]要在getSG之前先预处理  
//SG[]:0~n的SG函数值  
//S[]:为x后继状态的集合  
int f[N],SG[MAXN],S[MAXN];  
void  getSG(int n){  
    int i,j;  
    memset(SG,0,sizeof(SG));  
    //因为SG[0]始终等于0，所以i从1开始  
    for(i = 1; i <= n; i++){  
        //每一次都要将上一状态 的 后继集合 重置  
        memset(S,0,sizeof(S));  
        for(j = 0; f[j] <= i && j <= N; j++)  
            S[SG[i-f[j]]] = 1;  //将后继状态的SG函数值进行标记  
        for(j = 0;; j++) if(!S[j]){   //查询当前后继状态SG值中最小的非零值  
            SG[i] = j;  
            break;  
        }  
    }  
}  
```

# 三、感想

对于博弈这类题目，其实最终结果只取决于当前的局面。换言之在给出当前局面时，结局已经被决定了。

# 四、附
这是一些博弈题

[传送门](https://vjudge.net/contest/121217#overview)

POJ 2234 Matches Game

HOJ 4388 Stone Game II

POJ 2975 Nim

HOJ 1367 A Stone Game

POJ 2505 A multiplication game

ZJU 3057 beans game

POJ 1067 取石子游戏

POJ 2484 A Funny Game

POJ 2425 A Chess Game

POJ 2960 S-Nim

POJ 1704 Georgia and Bob

POJ 1740 A New Stone Game

POJ 2068 Nim

POJ 3480 John

POJ 2348 Euclid's Game

HOJ 2645 WNim

POJ 3710 Christmas Game 

POJ 3533 Light Switching Game

