# Problem
gNumbers

Googlers are crazy about numbers and games, especially number games! Two Googlers, Laurence and Seymour, have invented a new two-player game based on "gNumbers". A number is a gNumber if and only if the sum of the number's digits has no positive divisors other than 1 and itself. (In particular, note that 1 is a gNumber.)

The game works as follows: First, someone who is not playing the game chooses a starting number N. Then, the two players take turns. On a player's turn, the player checks whether the current number C is a gNumber. If it is, the player loses the game immediately. Otherwise, the player chooses a prime factor P of C, and keeps dividing C by P until P is no longer a factor of C. (For example, if the current number were 72, the player could either choose 2 and repeatedly divide by 2 until reaching 9, or choose 3 and repeatedly divide by 3 until reaching 8.) Then the result of the division becomes the new current number, and the other player's turn begins.

Laurence always gets to go first, and he hates to lose. Given a number N, he wants you to tell him which player is certain to win, assuming that both players play optimally.
# 题意
取子游戏，每次将现在的数字除去某种质因数的影响，若现在的数字各位数字加和为质数或1，那么就算输
# 思路
由于一次除去所有的某种质因数，也就是说假如一种质因数为a,次数为num,则现在的数字C = C/pow(a,num),所以遍历的状态有限，不会超过2的14次方，可以使用sg函数进行遍历
# 错误
sg(x) = 0,fail, 而不是sg(x)&1
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
typedef pair<int,int> P;
typedef long long ll;
typedef long double ld;
const int maxs = 102;
bool ntprime[maxs];
void init(){
    ntprime[1] = true;
    for(int i = 4;i < maxs;i += 2){ntprime[i] = true;}
    for(int i = 3;i < maxs;i += 2){
        if(!ntprime[i]){
            for(int j = 3;i * j < maxs;j += 2){
                ntprime[i * j] = true;
            }
        }
    }
}
map<ll,int>sg;
bool check(ll n){
    int sum = 0;
    while(n > 0){
        sum += n%10;
        n/= 10;
    }
    if(sum == 1)return true;
    return !ntprime[sum];
}

int a[maxs],len;
ll num[maxs];

void split(ll n){
    len = 0;
    if(n > 0 && (n & 1) == 0){
        a[len] = 2;
        num[len] = 1;
        while(n > 0 && (n & 1) == 0){
            n >>= 1;
            num[len] *= 2;
        }
        len++;
    }
    for(int i = 3;(ll)i * i < n;i+=2){
        if(n % i == 0){
            a[len] = i;
            num[len] = 1;
            while(n % i == 0){
                n /= i;
                num[len] *= i;
            }
            len++;
        }
    }
    if(n > 1){
        a[len] = n;
        num[len] = n;
        len++;
    }
}

int getsg(ll n){
    if(sg.count(n) != 0)return sg[n];
    if(check(n)){
        return sg[n] = 0;
    }
    bool used[maxs];
    memset(used,0,sizeof used);
    for(int i = 0;i < len;i++){
        if(n % num[i] == 0){
            int sub = getsg(n/num[i]);
            used[sub] = true;
        }
    }
    for(int i = 0;i < maxs;i++){
        if(!used[i]){
            sg[n] = i;
            break;
        }
    }
    return sg[n];
}

int main()
{
   // freopen("input.txt","r",stdin);
    freopen("C-large-practice.in","r",stdin);
    freopen("C-large-practice.out","w",stdout);
    init();
    int T;
    scanf("%d",&T);
    for(int ti = 1;ti <= T;ti++){
        ll n;
        scanf("%lld",&n);
        split(n);
        sg.clear();
        int ans = getsg(n);
        printf("Case #%d: %s\n",ti,ans?"Laurence":"Seymour");

    }

    return 0;
}

```