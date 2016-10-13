# 题目
Recently Maxim has found an array of n integers, needed by no one. He immediately come up with idea of changing it: he invented positive integer x and decided to add or subtract it from arbitrary array elements. Formally, by applying single operation Maxim chooses integer i (1 ≤ i ≤ n) and replaces the i-th element of array ai either with ai + x or with ai - x. Please note that the operation may be applied more than once to the same position.

Maxim is a curious minimalis, thus he wants to know what is the minimum value that the product of all array elements (i.e. ) can reach, if Maxim would apply no more than k operations to it. Please help him in that.
# 题意
有n个整数a[i],可以执行k次操作，每次挑选i使得a[i]+x或者-x，最终使得n个整数的乘积最小
# 思路
1. 每次都能加上或者减去x,对于加上x的情况，使得乘积/a[i]最小（除了a[i]之外的n-1个整数乘积）的最优，对于减去x的情况，使得乘积/a[i]最大的最优
2. 综合起来考虑，每次选择abs(a[i])最小的，如果剩下的数乘积为负数则加上x,否则减去x
3. 可证明这样局部最优将使得整体最优
# 注意
1. 注意维护剩下的数的符号问题，因为之前的实现较为复杂所以错了几次
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
typedef long long ll;
typedef pair<ll,int> P;
typedef unsigned long long ull;
typedef long double ld;
const int maxn = 2e5 + 5;
const int maxm = 5e3 + 3;
ll a[maxn];
int n,k,x;
int mn;
priority_queue<P,vector<P>,greater<P> > que;
bool similar(ll x0,ll x1){
    return (x0 == 0 && x1 == 0) || (x0 < 0 && x1 < 0) || (x0 > 0 && x1 > 0);
}

int getmax(){
    int mx = que.top().second;
    que.pop();
    return mx;
}

int main(){
    freopen("input.txt","r",stdin);
    scanf("%d%d%d",&n,&k,&x);
    for(int i = 0;i < n;i++){
        scanf("%I64d",a + i);
        if(a[i] < 0){mn++;}
        que.push(P(abs(a[i]),i));
    }
    for(int i = 0;i < k;i++){
        int sig = que.top().first == 0L?0:((mn & 1)?-1:1);
        int ind = getmax();
        if(a[ind] < 0L)mn--;
        if(similar(a[ind],sig) && (a[ind] != 0L || (mn & 1) == 0)){
            if(a[ind] < x)mn++;
            a[ind] -= x;
        }else{
            if(a[ind] < -x)mn++;
            a[ind] += x;
        }
        que.push(P(abs(a[ind]),ind));
    }
    for(int i = 0;i < n;i++){
        printf("%I64d%c",a[i],i == n - 1?'\n':' ');
    }
    return 0;
}

```
# 学习
## Code #1.1: shortest size
```c++
#include<iostream>
#include<cstdio>
#include<algorithm>
#define SGN(x) ((x)<0?-1:1) 
typedef long long LL;
using namespace std;
const int N = 200005;
LL a[N];
int n,k,x,b[N];
bool cmp(int x, int y){return abs(a[x])>abs(a[y]);}
int main() {
	cin>>n>>k>>x; int sgn=1;
	for (int i=1;i<=n;i++) {scanf("%I64d",&a[i]); sgn*=SGN(a[i]); b[i]=i;}
	make_heap(b+1,b+n+1,cmp);
	while (k--) {
		int tmp=sgn*SGN(a[b[1]]); a[b[1]]-=tmp*x; sgn=tmp*SGN(a[b[1]]); pop_heap(b+1,b+n+1,cmp); push_heap(b+1,b+n+1,cmp);
	}
	for (int i=1;i<=n;i++) printf("%I64d ",a[i]);
	return 0;
}
```
## Code#1.1:Tips
1. 特殊的建堆技巧
    1. 初始化一个数组，内容为本身序号
    2. 使用cmp函数比较序号所代表的内容
    3. 使用make_heap建堆
## Code#1.2
```python
import heapq

n,k,x = map(int, raw_input().split())
a = map(int, raw_input().split())
q = []
checker = 1
for i in xrange(n):
  heapq.heappush(q, (abs(a[i]), i))
  if a[i] < 0: checker *= -1
while k > 0:
  nxt = heapq.heappop(q)
  if checker > 0:
    if a[nxt[1]] >= 0:
      a[nxt[1]] -= x
      if a[nxt[1]] < 0: checker *= -1
    else:
      a[nxt[1]] += x
      if a[nxt[1]] >= 0: checker *= -1
  else:
    if a[nxt[1]] >= 0:
      a[nxt[1]] += x
    else:
      a[nxt[1]] -= x
  heapq.heappush(q, (abs(a[nxt[1]]), nxt[1]))
  k -= 1
print " ".join(map(str, a))
```
## Code #1.2:Tips
1. n,k,x = map(int, raw_input().split())
2. q=[],heapq.heappush(q, (abs(a[i]), i))
3. print " ".join(map(str, a))
