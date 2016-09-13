# Problem

Googlers are very interested in cubes, but they are bored with normal three-dimensional cubes and also want to think about other kinds of cubes! A "D-dimensional cube" has D dimensions, all of equal length. (D may be any positive integer; for example, a 1-dimensional cube is a line segment, and a 2-dimensional cube is a square, and a 4-dimensional cube is a hypercube.) A "D-dimensional cuboid" has D dimensions, but they might not all have the same lengths.

Suppose we have an N-dimensional cuboid. The N dimensions are numbered in order (0, 1, 2, ..., N - 1), and each dimension has a certain length. We want to solve many subproblems of this type:

1. Take all consecutive dimensions between the Li-th dimension and Ri-th dimension, inclusive.

2. Use those dimensions to form a D-dimensional cuboid, where D = Ri - Li + 1. (For example, if Li = 3 and Ri = 6, we would form a 4-dimensional cuboid using the 3rd, 4th, 5th, and 6th dimensions of our N-dimensional cuboid.)

3. Reshape it into a D-dimensional cube that has exactly the same volume as that D-dimensional cuboid, and find the edge length of that cube.

Each test case will have M subproblems like this, all of which use the same original N-dimensional cuboid. 
# 题意
输出(l - r + 1)个数字的几何平均数
# 思路
这道题一开始想到要用高精来计算，但是usaxena95提供了更好的办法，对每个数字log10,再把对数相加，除以(l - r + 1)得到log10(ans),最终pow(10,log10(ans)),这样就避免了乘法和开方中严重的精度流失
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
const int maxn = 1e3 + 3;
ld a[maxn];
ld lg[maxn];

int main()
{
    freopen("B-large-practice.in","r",stdin);
    freopen("B-large-practice.out","w",stdout);
    int t;
    scanf("%d",&t);
    for(int ti = 1;ti <= t;ti++){
        printf("Case #%d:\n",ti);
        int n,m;
        scanf("%d%d",&n,&m);
        for(int i = 0;i < n;i++){
            scanf("%Lf",a + i);
            lg[i] = log10(a[i]);
        }
        for(int i = 0;i < m;i++){
            int f,t;
            scanf("%d%d",&f,&t);
            ld s = 0;
            for(int j = f;j <= t;j++)s += lg[j];
            s /= (t - f + 1);
            ld ans = pow(10,s);
            printf("%.9Lf\n",ans);
        }
    }

    return 0;
}

```