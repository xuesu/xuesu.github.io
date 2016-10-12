# 题意
单向无环无重边图，每条弧都需花费一段时间，起点为1，终点为n，求在时间T内最多经过多少个点？（节点从1到n,n <= 5000,共有m条弧，m <=5000, T<= 5000）
# 
# 思路
可以在最短路同时，维护目前的路径长度，也即原始版本最短路为dp[i]，代表从起点1到i所经过的最短路径，现在则维护dp[i][j],代表从起点1到i经过j个点的最短路径
# 注意
1. 起点必须为1，所以spfa的queue最初只需要加入起点1
2. 因为起点为1，所以对于点i来说,dp[i]不是严格递增的，因为有些j小于能到达的步数，此时dp[i][j]为初始化的inf
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
typedef unsigned long long ull;
typedef long double ld;
const int maxn = 5e3 + 3;
const int maxm = 5e3 + 3;
int first[maxn];
int nxt[maxn];
int to[maxn];
int cost[maxn];
int len;
int dp[maxn][maxn];
int pre[maxn][maxn];
bool vis[maxn][maxn];
int st[maxn];
void addedge(int u,int v,int c){
    nxt[len] = first[u];
    to[len] = v;
    cost[len] = c;
    first[u] = len++;
}
int main(){
    freopen("input.txt","r",stdin);
    int n,m,t;
    memset(first,-1,sizeof first);
    memset(dp,0x6f,sizeof dp);
    scanf("%d%d%d",&n,&m,&t);
    for(int i = 0;i < m;i++){
        int u,v,c;
        scanf("%d%d%d",&u,&v,&c);
        addedge(u,v,c);
    }
    for(int i = 1;i <= n;i++)dp[i][1] = 0;
    queue<P>que;
    que.push(P(1,1));
    vis[1][1] = true;
    while(!que.empty()){
        int u = que.front().first;int num = que.front().second;que.pop();vis[u][num] = false;
        if(u == n)continue;
        for(int p = first[u];p != -1;p = nxt[p]){
            int v = to[p];
            if(dp[u][num] + cost[p] <= t && dp[u][num] + cost[p] < dp[v][num + 1]){
                dp[v][num + 1] = dp[u][num] + cost[p];
                pre[v][num + 1] = u;
                if(!vis[v][num]){
                    que.push(P(v,num + 1));
                   // printf("%d to %d\n",u,v);
                    vis[v][num] = true;
                }
            }
        }
    }
    int ans = 1;
    for(int i = n;i >= 1;i--){
        if(dp[n][i ] <= t){
            ans = i;
            for(int j = i, u = n;j > 0;j--){
                st[j] = u;
                u = pre[u][j];
            }
            break;
        }
    }
    printf("%d\n",ans);
    for(int i = 1;i <= ans;i++){
        printf("%d%c",st[i],i == ans?'\n':' ');
    }
    return 0;
}

```

# 学习部分

## Code #1 shortest size
```c++
#include <bits/stdc++.h>
using namespace std;

int N, M, T, e[5555][3], d[5555][5555], p[5555][5555], a, i, j, x, y, z;
stack<int> s;

int main() {
	for (cin >> N >> M >> T; i < M * 3; i++) cin >> e[i / 3][i % 3];
	for (i = 0; i <= N; i++) for (j = 0; j <= N; j++) d[i][j] = 1.1e9;
	for (d[1][1] = 0, i = 2; i <= N; i++){
		bool fl = false;
		for (j = 0; j < M; j++){
			if (x = e[j][0], y = e[j][1], z = e[j][2], d[i - 1][x] + z < d[i][y] && T - d[i - 1][x] >= z){
				d[i][y] = d[i - 1][x] + z, p[i][y] = x;
				fl = true;
				if(y == N)a = i;
            }
        }
        if(!fl)break;
    }
	cout << a << '\n';
	for (j = N; j; j = p[a--][j]) s.push(j);
	while (s.size()) cout << s.top() << " ", s.pop();
}

```
## Code #1:Tips
1. 由于z + d[i - 1][x] <= T 可能超过int范围，所以可以用 T - d[i - 1][x] >= z代替，也即**判断中加法可能超过范围时可以在不等式两边做减法**
2. 每组输入数据数量一定时，可以使用总index来输入遍历各组输入，不过可读性较差
     ```c++
    for (cin >> N >> M >> T; i < M * 3; i++) cin >> e[i / 3][i % 3];
    ```
3. 逗号操作符返回最右边的数值，
    ```c++
    if (x = e[j][0], y = e[j][1], z = e[j][2], d[i - 1][x] + z < d[i][y] && T - d[i - 1][x] >= z){
    ```
4. 思路不同处
    1. dp(d)第一维为路径长度，从动态规划方面考虑，次数固定，不需要spfa算法
    2. 方便跳出循环节约时间，
    3. 且路径长度往往较短，比起使用节点作为第一维更优

## Code#2 :shortest time
```c++
#include<iostream>
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<algorithm>
#include<utility>
#include<vector>
#include<map>
using namespace std;
const int N = 5008;
#define ll long long
#define mp make_pair
#define X first
#define Y second

int n, m, tim, flag;
int minx(int x, int y) { if (x<y)y = x; return y; }
int maxx(int x, int y) { if (x>y)y = x; return y; }
vector< pair<int, int> >a[N];
map<int, int>b[N], c[N];
int d[N];

void yun(int x)
{
	if (d[x]) return;	
	d[x] = 1;

	if (x == n) return;

	int i, p, p1, p2;
	map<int, int>::iterator k;	
	for (i = 0; i<(int)a[x].size(); i++)
	{
		yun(p = a[x][i].X);
		for (k = b[p].begin(); k != b[p].end(); k++)
		{
			p1 = (*k).X; p2 = (*k).Y;
			if ((p2 + a[x][i].Y) <= tim && (b[x].find(p1 + 1) == b[x].end() || b[x][p1 + 1]>p2 + a[x][i].Y))
			{
				b[x][p1 + 1] = p2 + a[x][i].Y;
				c[x][p1 + 1] = p;
			}
		}
	}
	return;
}

void dfs(int x, int y)
{
	if (flag) printf(" ");
	flag = 1;
	printf("%d", x);
	if (x < n) dfs(c[x][y], y - 1);
}

int main(void)
{
	int i, j, p1, p2, p3;
	scanf("%d%d%d", &n, &m, &tim);
	for (i = 1; i <= m; i++) 
	{ 
		scanf("%d%d%d", &p1, &p2, &p3);
		a[p1].push_back(mp(p2, p3));
	}

	b[n][1] = 0;

	yun(1);
	map<int, int>::iterator k;
	j = 0;
	for (k = b[1].begin(); k != b[1].end(); k++)
	{
		j = maxx(j, (*k).X);
	}
	 
	printf("%d\n", j);
	flag = 0;
	dfs(1, j);

	return 0;
}
```

## Code#2:Tips
1. 在单向无环图中，dfs比最短路和dp更优
2. 由于步数的区间并不连续，代码原作者选择了使用**map**
3. stl的使用
    - map<int, int>::iterator k;
    - 在此场景（一个点联通的其它点数目不会很多）下map的效率很高
    - (b[x].find(p1 + 1) == b[x].end() || b[x][p1 + 1]>p2 + a[x][i].Y)
        - 可以使用find查找key值对应的value，找不到返回end()

## Code #2:改编非map版
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
typedef unsigned long long ull;
typedef long double ld;
const int maxn = 5e3 + 3;
const int maxm = 5e3 + 3;
int first[maxn];
int nxt[maxn];
int to[maxn];
int cost[maxn];
int len;
int dp[maxn][maxn];
int pre[maxn][maxn];
int d[maxn];
int st[maxn];
int n,m,t;
void addedge(int u,int v,int c){
    nxt[len] = first[u];
    to[len] = v;
    cost[len] = c;
    first[u] = len++;
}
void dfs(int u){
    if(d[u] != 0)return;
    for(int p = first[u];p != -1;p = nxt[p]){
        int v = to[p];
        if(d[v] == 0)dfs(v);
        if(d[v] == -1)continue;
        for(int num = d[v];num <= n;num++){
            if(t - dp[v][num] >= cost[p] && dp[v][num] + cost[p] < dp[u][num + 1]){
                dp[u][num + 1] = dp[v][num] + cost[p];
                pre[u][num + 1] = v;
                if(d[u] == 0)d[u] = num + 1;
            }
        }
    }
    if(d[u] == 0)d[u] = -1;
}
int main(){
    freopen("input.txt","r",stdin);
    memset(first,-1,sizeof first);
    memset(dp,0x6f,sizeof dp);
    scanf("%d%d%d",&n,&m,&t);
    for(int i = 0;i < m;i++){
        int u,v,c;
        scanf("%d%d%d",&u,&v,&c);
        addedge(u,v,c);
    }
    dp[n][1] = 0;
    d[n] = 1;
    dfs(1);
    for(int i = n;i >= 1;i--){
        if(dp[1][i] <= t){
            printf("%d\n",i);
            for(int j = 1,k = i;k > 0;j = pre[j][k],k--){
                printf("%d%c",j,k == 1?'\n':' ');
            }
            break;
        }
    }
    return 0;
}

```