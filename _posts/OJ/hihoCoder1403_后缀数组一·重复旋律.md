# 题目
小Hi平时的一大兴趣爱好就是演奏钢琴。我们知道一个音乐旋律被表示为长度为 N 的数构成的数列。

小Hi在练习过很多曲子以后发现很多作品自身包含一样的旋律。旋律是一段连续的数列，相似的旋律在原数列可重叠。比如在1 2 3 2 3 2 1 中 2 3 2 出现了两次。

小Hi想知道一段旋律中出现次数至少为K次的旋律最长是多少？
# 思路
求出原数组的高度数组，当k>=2时，问题就能转化为求连续k-1个高度的最小值
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
#include <iterator>
using namespace std;
typedef long long ll;
typedef pair<int,int> P;
typedef unsigned long long ull;
typedef long double ld;
const int maxn = 2e5 + 5;
const int maxm = 102;
int cntA[maxn],cntB[maxn],A[maxn],B[maxn],sa[maxn],tsa[maxn],rk[maxn],a[maxn],h[maxn];
void debugrk(int n,int l){
    for(int i = 0;i <= n;i++){
        printf("sa[%d]:%d ",i,sa[i]);
    }
    puts("");
    for(int i = 0;i <= n;i++){
        printf("rk[%d]:%d ",i,rk[i]);
        for(int j = i;j < n && j < i + l;j++){
            printf("%d ",a[j]);
        }
        puts("");
    }
    puts("");
}
void debugh(int n){
    for(int i = 0;i <= n;i++){
        printf("h[%d]:%d ",i,h[i]);
        for(int j = sa[i];j < n;j++){
            printf("%d ",a[j]);
        }
        puts("");
    }
    puts("");
}
int main(){
    int n,k;
    freopen("input.txt","r",stdin);
    scanf("%d%d",&n,&k);
    for(int i = 0;i < n;i++){
        scanf("%d",a + i);
        cntA[a[i]]++;
    }
    a[n] = 0;
    for(int i = 1;i < maxn;i++){
        cntA[i] += cntA[i - 1];
    }
    for(int i = 0;i <= n;i++){
        sa[cntA[a[i]]--] = i;
    }
    sa[0] = n;rk[n] = 0;
    for(int i = 1;i <= n;i++){
        rk[sa[i]] = rk[sa[i - 1]] + (a[sa[i]] == a[sa[i - 1]]?0:1);
    }
    //debugrk(n,1);
    for(int l = 1;l < n;l<<=1){
        memset(cntA,0,sizeof cntA);memset(cntB,0,sizeof cntB);
        for(int i = 0;i < n;i++){
            cntA[A[i] = rk[i]]++;
            cntB[B[i] = rk[min(i + l,n)]]++;
        }
        for(int i = 1;i <= n;i++){
            cntA[i] += cntA[i - 1];
            cntB[i] += cntB[i - 1];
        }
        for(int i = 0;i <= n;i++){
            tsa[cntB[B[i]]--] = i;
        }
        for(int i = n;i >= 0;i--){
            sa[cntA[A[tsa[i]]]--] = tsa[i];
        }
        for(int i = 1;i <= n;i++){
            rk[sa[i]] = rk[sa[i - 1]] + ((A[sa[i]] == A[sa[i - 1]] && B[sa[i]] == B[sa[i - 1]])?0:1);
        }
      //  debugrk(n,2 * l);
    }
    for(int i = 0,height = 0;i < n;i++){
        if(height)height--;
        for(;sa[rk[i] - 1] + height < n && i + height < n && a[i + height] == a[sa[rk[i] - 1] + height];height++){}
        h[rk[i] - 1] = height;
    }
 //   debugh(n);
    int ans = k == 1?n:0;
    k--;
    priority_queue<P,vector<P>,greater<P> > que;
    for(int i = 0;i < n;i++){
        que.push(P(h[i],i));
        while(!que.empty() && que.top().second <= i - k){que.pop();}
        if(!que.empty() && i >= k - 1){ans = max(ans,que.top().first);}
    }
    printf("%d\n",ans);
    return 0;
}

```