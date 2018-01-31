---
title: 素数相关算法
date: 2017-07-31 22:00:41
tags: [ACM,数学,素数]
categories: [算法]
---
#### 引言

素数在ACM中出现得十分频繁。我在此简要写一下素数相关算法。

<!--more-->

## 一、朴素算法

>对于判断素数而言，最朴素的算法是根据素数的定义：在[2,n-1]是否存在m使得n%m==0。时间复杂度为O(n)

#### 代码

```cpp
int isPrime(int n) {  
    int i;  
    for (i = 2; i < n; ++i) {  
        if (n % i == 0) return 0;  
    }  
    return 1;  
}
```
>显然对于给定的n，任何大于sqrt(n)的数都不会是n的因子。故只需判断[2,sqrt(n)]中的所有数即可。时间复杂度为O(sqrt(n))

#### 代码

```cpp
int isPrime(long long n) {  
    long long i;  
    for (i = 2; i * i <= n; ++i) {  
        if (n % i == 0) return 0;  
    }  
    return 1;  
}  
```
>对于这一算法，虽然仅仅是将i改为i*i，但在1s时间内可以处理的数可达10^16。

## 二、素数筛选法

>朴素方法可以判断某个数是否为素数，但对于某个区间内有多少个素数或是某个区间内有哪些素数这些问题，最优的朴素算法所需的时间也是O(n*sqrt(n))。而使用埃氏筛选法则可以将时间优化到O(n)。

>思路：默认2为素数，将所有2的倍数置为合数；再将3默认为素数，将所有3的倍数置为合数；遇到4--已被置为合数，跳过······

#### 代码

```cpp
const int maxn = 1e7 + 5;  
int pri[maxn];  
void getPrime(int n) {  
    for (int i = 0; i <= n; ++i) pri[i] = i;  
    pri[1] = 0;  
    for (int i = 2; i <= n; ++i) {  
        if (!pri[i]) continue;  
        pri[++pri[0]] = i;  
        for (int j = 2; i * j <= n && j < n; ++j) {  
            pri[i * j] = 0;  
        }  
    }  
}  
```
>以上代码由于重复计算并不是严格O(n)的。比如对于数30，它被2、3、5都置为合数（显然只需要置为合数一次就可以了）。一下算法可以在此基础上进行优化。

#### 代码

```cpp
const int MAXN = 1e7 + 5;  
void getPrime(){  
    memset(prime, 0, sizeof(prime));  
    for (int i = 2;i <= MAXN;i++) {  
        if (!prime[i])prime[++prime[0]] = i;  
        for (int j = 1;j <= prime[0] && prime[j] <= MAXN / i;j++) {  
            prime[prime[j] * i] = 1;  
            if (i%prime[j] == 0) break;  
        }  
    }  
}  
```

## 三、容斥原理

>使用素数筛选法只能应对10^7左右的运算，对于10^8级别的运算有很大可能会MLE或者TLE。（例AOJ-AHU-557)
>
>此时可以考虑容斥原理。对于给出的n依次减去n/pi再加上n/(pi*pj)······并以此类推便可以得出结果（注意剪枝以防超时）

#### 代码

```cpp
#include <cmath>  
#include <cstdio>  
using namespace std;  
   
const int maxn = 10005;  
int sqrn, n, ans = 0;  
bool vis[maxn];  
int pri[1500] = {0};  
void init(){  
    vis[1] = true;  
    int k = 0;  
    for(int i = 2; i < maxn; i++){  
        if(!vis[i]) pri[k++] = i;  
        for(int j = 0; j < k && pri[j] * i < maxn; j++){  
            vis[pri[j] * i] = true;  
            if(i % pri[j] == 0) break;  
        }  
    }  
}  
void dfs(int num, int res, int index){  
    for(int i = index; pri[i] <= sqrn; i++){  
        if(1LL * res * pri[i] > n){  
            return;  
        }  
        dfs(num + 1, res * pri[i], i+1);  
        if(num % 2 == 1){  
            ans -= n / (res * pri[i]);  
        }else{  
            ans += n / (res * pri[i]);  
        }  
   
        if(num == 1) ans++;  
    }  
}  
int main(){  
    init();  
    while(~scanf("%d",&n) && n){  
        ans = n;  
        sqrn = sqrt((double)n);  
        dfs(1,1,0);  
        printf("%d\n",ans-1);  
    }  
    return 0;  
}  
```
## 四、区间筛法

>区间筛是针对一类诸如查询区间[a,b]中素数个数(0<a<b<10^12,b-a<10^6)对于这一问题，朴素的埃氏筛和上面提到的容斥原理都无法解决，因此我们需要区间筛

#### 代码

```cpp

代码还不会撒~

```

## 五、Meissel-Lehmer算法

>黑科技，可以再3.82ms内判断出10^10内的素数个数。

#### 代码

```cpp
#include    <stdio.h>  
#include    <string.h>  
#include    <stdlib.h>  
#include    <time.h>  
#include    <math.h>  
   
__int64 *primarr, *v;  
__int64 q = 1, p = 1;  
   
//π(n)  
__int64 pi(__int64 n, __int64 primarr[], __int64 len)  
{  
    __int64 i = 0, mark = 0;  
    for (i = len - 1; i > 0; i--) {  
        if (primarr[i] < n) {  
            mark = 1;  
            break;  
        }  
    }  
    if (mark)  
        return i + 1;  
    return 0;  
}  
   
//Φ(x,a)  
__int64 phi(__int64 x, __int64 a, __int64 m)  
{  
    if (a == m)  
        return (x / q) * p + v[x % q];  
    if (x < primarr[a - 1])  
        return 1;  
    return phi(x, a - 1, m) - phi(x / primarr[a - 1], a - 1, m);  
}  
   
__int64 prime(__int64 n)  
{  
    char *mark;  
    __int64 mark_len;  
    __int64 count = 0;  
    __int64 i, j, m = 7;  
    __int64 sum = 0, s = 0;  
    __int64 len, len2, len3;  
   
    mark_len = (n < 10000) ? 10002 : ((__int64)exp(2.0 / 3 * log(n)) + 1);  
   
    //筛选n^(2/3)或n内的素数  
    mark = (char *)malloc(sizeof(char) * mark_len);  
    memset(mark, 0, sizeof(char) * mark_len);  
    for (i = 2; i < (__int64)sqrt(mark_len); i++) {  
        if (mark[i])  
            continue;  
        for (j = i + i; j < mark_len; j += i)  
            mark[j] = 1;  
    }  
    mark[0] = mark[1] = 1;  
   
    //统计素数数目  
    for (i = 0; i < mark_len; i++)  
        if (!mark[i])  
            count++;  
   
    //保存素数  
    primarr = (__int64 *)malloc(sizeof(__int64) * count);  
    j = 0;  
    for (i = 0; i < mark_len; i++)  
        if (!mark[i])  
            primarr[j++] = i;  
   
    if (n < 10000)  
        return pi(n, primarr, count);  
   
    //n^(1/3)内的素数数目  
    len = pi((__int64)exp(1.0 / 3 * log(n)), primarr, count);  
    //n^(1/2)内的素数数目  
    len2 = pi((__int64)sqrt(n), primarr, count);  
    //n^（2/3)内的素数数目  
    len3 = pi(mark_len - 1, primarr, count);  
   
    //乘积个数  
    j = mark_len - 2;  
    for (i = (__int64)exp(1.0 / 3 * log(n)); i <= (__int64)sqrt(n); i++) {  
        if (!mark[i]) {  
            while (i * j > n) {  
                if (!mark[j])  
                    s++;  
                j--;  
            }  
            sum += s;  
        }  
    }  
    free(mark);  
    sum = (len2 - len) * len3 - sum;  
    sum += (len * (len - 1) - len2 * (len2 - 1)) / 2;  
   
    //欧拉函数  
    if (m > len)  
        m = len;  
    for (i = 0; i < m; i++) {  
        q *= primarr[i];  
        p *= primarr[i] - 1;  
    }  
    v = (__int64 *)malloc(sizeof(__int64) * q);  
    for (i = 0; i < q; i++)  
        v[i] = i;  
    for (i = 0; i < m; i++)  
        for (j = q - 1; j >= 0; j--)  
            v[j] -= v[j / primarr[i]];  
   
    sum = phi(n, len, m) - sum + len - 1;  
    free(primarr);  
    free(v);  
    return sum;  
}  
   
int main()  
{  
    __int64 n;  
    __int64 count;  
    int h;  
    clock_t start, end;  
    while(scanf("%I64d", &n)!=EOF)  
    {  
  
        p=1;  
        q=1;  
        start = clock();  
        count = prime(n);  
        end = clock() - start;  
        printf("%I64d(%d亿)内的素数个数为%I64d\n",n,n/100000000,count);  
        printf("用时%lf毫秒\n",(double)end/1000);  
    }  
    return 0;  
}  
```