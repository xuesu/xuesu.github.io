# Problem

Alien tech company G has a very old file transfer tool that is still in use today. While the tool is running, it reassures users by giving status updates on both the percentage of files transferred so far and the number of files transferred so far. The status updates during the process might look like this:

     20% |==>-------|     1 files transferred
    100% |==========|     5 files transferred
But the percentage isn't precise; it is simply truncated before the decimal point (i.e. floored to the next lowest or equal 1%). That is, both 1.2% and 1.7% would be displayed as 1%.

Some users may want to know the exact total number of files, so you want to modify the tool so that the status updates look like this:

     20% |==>-------|     1 out of 5 files transferred
    100% |==========|     5 out of 5 files transferred
But you've realized that it may or may not be possible to know the number of files. Given the status updates that the tool displays, either figure out how many files there are, or determine that it can't be done (i.e., there are multiple possible values for the number of files). The status updates are not guaranteed to occur at regular intervals and are not guaranteed to occur whenever a file is transferred.
# 题意
假设有一个总数ans，给与递增顺序排列的小于ans的数字ki，以及它们分别除以ans的商的百分数表示形式的整数部分pi，求ans，如果有多个ans，输出-1
# 思路
明显 ans <= (ki * 100) / pi,且ans > (ki * 100)/(pi + 1),值得注意的是ki <= ans,所以如果pi=100的时候，ans必然等于ki，不能发生101/100=100%这种情况
# Code
```
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
const int maxp = 102;
const int maxn = 102;
const ll mod = 1e9 + 7;
const ll mxinf = 1e17 + 0.1;
const ld eps = 1e-10;
int p[maxn];
ll k[maxn];
int n;
bool check(ll ans){
    for(int i = 0;i < n;i++){
        if(p[i] && k[i] * 100 / ans != p[i])return false;
        if(p[i] == 100 && k[i] != ans)return false;
    }
    return true;
}
int main()
{
    //freopen("input.txt","r",stdin);
    freopen("/home/iris/Downloads/B-large-practice.in","r",stdin);
    freopen("B-large-practice.out","w",stdout);
    int T;
    cin>>T;
    for(int ti = 1;ti <= T;ti++){
        cin>>n;
        ld mn = 0,mx = mxinf;
        for(int i = 0;i < n;i++){
            cin>>p[i]>>k[i];
            mn = max(mn,(ld)100 * k[i] / (p[i] + 1) - eps);
            mx = min(mx,(ld)100 * k[i] / p[i] + eps);
        }
        ll ans = p[n - 1] == 100?k[n - 1]:mx;
        if(!check(ans))ans--;
        if(!check(ans) || mn >= mx || check(ans + 1) || check(ans - 1)){
            cout<<"Case #"<<ti<<": "<<-1<<endl;
        }else{
            cout<<"Case #"<<ti<<": "<<ans<<endl;
        }

    }

    return 0;
}

```