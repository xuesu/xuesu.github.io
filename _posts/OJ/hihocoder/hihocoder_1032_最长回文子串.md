# 题意
给若干字符串，输出最长回文子串长度
# 思路
1. **当以i为中心的回文子串长度为dp[i]时，若i>=2,则在以i为中心的回文子串范围内，以i-1为中心的回文子串恰好等于以i+1为中心的回文子串**，利用**以i为中心对称**的性质，可以减少对比次数
2. 以i+1为中心的回文子串在以i为中心的回文子串的范围内的最大长度是dp[i]-2
3. 可以在首尾和中间都加入特殊字符，将偶长度的回文字符串转化为奇数长度的回文字符串,新字符串的有效长度为长度/2（整除）
# 代码
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
//typedef pair<int,int> P;
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
const int maxn = 2e6 + 6;
char org[maxn],maz[maxn];
int dp[maxn];
int main(){
    int T;
    freopen("input.txt","r",stdin);
    scanf("%d",&T);
    for(int ti = 1;ti <= T;ti++){
        scanf("%s",org);
        for(int i = 0;org[i];i++){
            maz[2 * i] = '#';
            maz[2 * i + 1] = org[i];
            dp[2 * i] = dp[2 * i + 1] = 1;
            if(org[i + 1] == 0){
                maz[2 * i + 2] = '#';
                maz[2 * i + 3] = 0;
                dp[2 * i + 2] = dp[2 * i + 3] = 1;
            }
        }
        int ans = 1;
        for(int i = 1;maz[i];i++){
            if(i >= 2)dp[i] = max(dp[i],min(dp[i - 2],dp[i - 1] - 2));
            int j = dp[i] / 2 + 1;
            for(;i - j >= 0 && maz[i + j];j++){
                if(maz[i - j] != maz[i + j])break;
            }
            dp[i] = j * 2 - 1;
            ans = max(dp[i],ans);
        }
        printf("%d\n",ans / 2);
    }
    return 0;
}

```