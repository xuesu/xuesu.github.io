# Problem 
Company G has a main campus with N offices (numbered from 0 to N - 1) and M bidirectional roads (numbered from 0 to M - 1). The ith road connects a pair of offices (Ui, Vi), and it takes Ci minutes to travel on it (in either direction).

A path between two offices X and Y is a series of one or more roads that starts at X and ends at Y. The time taken to travel a path is the sum of the times needed to travel each of the roads that make up the path. (It's guaranteed that there is at least one path connecting any two offices.)

Company G specializes in efficient transport solutions, but the CEO has just realized that, embarrassingly enough, its own road network may be suboptimal! She wants to know which roads in the campus are inefficient. A road is inefficient if and only if it is not included in any shortest paths between any offices.

Given the graph of offices and roads, can you help the CEO find all of the inefficient roads? 
# 题意
求不存在于任何一条最短路上的路
# 思路
先求任意两点间最短路，然后对比每条路看Ci是Ui到Vi的最短长度即可
# ==错误原因==
==重边==会导致DP数组被覆盖
# Code 
```c++
#include <cstdio>
#include <map>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <string>
#include <vector>
#include <iostream>
#include <assert.h>
#include <sstream>
#include <cctype>
#include <queue>
#include <stack>
#include <map>
using namespace std;
typedef pair<int,int> P;
typedef long long ll;
typedef long double ld;
const ll inf = 0x7ffffffffffffff;
const int maxn = 102;
ll dp[maxn][maxn];
struct edge{
    int f,t;
    ll c;
}e[maxn * maxn * 2];
int main()
{
    freopen("C-large-practice.in","r",stdin);
    freopen("C-large-practice.out","w",stdout);
    int t;
    scanf("%d",&t);
    for(int ti = 1;ti <= t;ti++){
        printf("Case #%d:\n",ti);
        int n,m;
        scanf("%d%d",&n,&m);
        for(int i = 0;i < n;i++){fill(dp[i],dp[i] + n,inf);dp[i][i] = 0;}
        for(int i = 0;i < m;i++){
            scanf("%d%d%lld",&e[i].f,&e[i].t,&e[i].c);
            dp[e[i].f][e[i].t] = min(dp[e[i].f][e[i].t],e[i].c);
            dp[e[i].t][e[i].f] = min(dp[e[i].t][e[i].f],e[i].c);
        }
        for(int k = 0;k < n;k++){
            for(int i = 0;i < n;i++){
                for(int j = 0;j < n;j++){
                    if(dp[i][k] != inf && dp[k][j] != inf && dp[i][j] > dp[i][k] + dp[k][j]){
                        dp[i][j] = dp[i][k] + dp[k][j];
                    }
                }
            }
        }
        for(int i = 0;i < m;i++){
            if(e[i].c > dp[e[i].f][e[i].t]){
                printf("%d\n",i);
            }
        }
    }

    return 0;
}

```