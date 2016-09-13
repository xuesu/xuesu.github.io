# Problem
The DNA of the Albocede alien species is made up of 4 types of nucleotides: a, b, c, and d. Different Albocedes may have different sequences of these nucleotides, but any Albocede's DNA sequence obeys all of the following rules:

- It contains at least one copy of each of a, b, c, and d.
- All as come before all bs, which come before all cs, which come before all ds.
- There are exactly as many 'a's as 'c's.
- There are exactly as many 'b's as 'd's.

For example, abcd and aabbbccddd are valid Albocede DNA sequences. acbd, abc, and abbccd are not.

The Albocede-n is an evolved species of Albocede. The DNA sequence of an Albocede-n consists of one or more valid Albocede DNA sequences, concatenated together end-to-end. For example, abcd and aaabcccdaabbbccdddabcd are valid Albocede-n DNA sequences. (Observe that a valid Albocede-n DNA sequence is not necessarily also a valid Albocede DNA sequence.)

From one of your alien expeditions, you retrieved an interesting sequence of DNA made up of only as, bs, cs, and ds. You are interested in how many of the different subsequences of that sequence would be valid Albocede-n DNA sequences. (Even if multiple different selections of nucleotides from the sequence produce the same valid subsequence, they still all count as distinct subsequences.) Since the result may be very large, please find it modulo 1000000007 (109 + 7). 

# 题意
Alboced序列是a+b+c+d+这种顺序的序列，并且a的个数与c的个数相同，b和d的个数相同

Alboced-N序则是若干个Alboced序列相连

现在有一个字符串，它的子串可能有多少个Alboced-N序列（只要index不同就算不同的序列）

# 思路
本来想枚举a的开始,b的开始,c的开始,d的结束,a的长度,b的长度来解决这个问题，但是时间复杂度太高

题解的方法则是==采用dp数组来记录状态==，用dp的一维来记录a-c的数量，一维来记录b-d的数量，然后a->b->c->d这个顺序累加dp，用一维来记录现在累加到a,b,c,d的哪一个，控制状态累计的时候，比如a->b的时候a的数量不能为0，即可保证第1点

由于一开始初始化dp[0][0][0][0]=1，且这种空情况一路传递，所以后来需去除这个影响，答案需要-1，

完成a->b->c->d之后，可以直接累计到下一次的d[i][0][0][0]中

# Code
```c++
#include <iostream>
#include <cstdio>
#include <vector>
#include <cstring>
#include <cmath>
#include <algorithm>
#include <map>
#include <queue>
#include <set>
using namespace std;
const int MOD = (int)1e9 + 7;
int dp[510][260][260][4];
int n;
char s[510];

int calc( char s[] ) {
	memset( dp, 0, sizeof(dp) );
	dp[0][0][0][0] = 1;

	for ( int i = 0; i < n; i ++ ) {
		for ( int j = 0; j <= n / 2; j ++ ) {
			for ( int k = 0; k <= n / 2; k ++ )	{
				if ( dp[i][j][k][0] + dp[i][j][k][1] + dp[i][j][k][2] + dp[i][j][k][3] == 0 ) {
					continue;
				}
				/*for ( int l = 0; l < 4; l ++ ) {
					if ( dp[i][j][k][l] ) cout <<i<<" "<<j<<" "<<k<<" "<<l<<" "<<dp[i][j][k][l]<<endl;
				}*/
				//cout <<i<<" "<<j<<" "<<k<<" "<<0<<" "<<dp[i][j][k][0]<<endl;

				// situation 0
				( dp[i + 1][j][k][0] += dp[i][j][k][0] ) %= MOD;
				if ( s[i] == 'a' ) {
					( dp[i + 1][j + 1][k][0] += dp[i][j][k][0] ) %= MOD;
				}
				if ( s[i] == 'b' && j ) {
					( dp[i + 1][j][k + 1][1] += dp[i][j][k][0] ) %= MOD;
				}

				//situation 1
				( dp[i + 1][j][k][1] += dp[i][j][k][1] ) %= MOD;
				if ( s[i] == 'b' ) {
					( dp[i + 1][j][k + 1][1] += dp[i][j][k][1] ) %= MOD;
				}
				if ( s[i] == 'c' ) {
					if ( j == 1 ) {
						( dp[i + 1][0][k][3] += dp[i][j][k][1] ) %= MOD;
					} else {
						( dp[i + 1][j - 1][k][2] += dp[i][j][k][1] ) %= MOD;
					}
				}

				//situation 2
				( dp[i + 1][j][k][2] += dp[i][j][k][2] ) %= MOD;
				if ( s[i] == 'c' ) {
					if ( j == 1 ) {
						( dp[i + 1][0][k][3] += dp[i][j][k][2] ) %= MOD;
					} else {
						( dp[i + 1][j - 1][k][2] += dp[i][j][k][2] ) %= MOD;
					}
				}

				//situation 3
				( dp[i + 1][j][k][3] += dp[i][j][k][3] ) %= MOD;
				if ( s[i] == 'd' ) {
					if ( k == 1 ) {
						( dp[i + 1][0][0][0] += dp[i][j][k][3] ) %= MOD;
					} else {
						( dp[i + 1][0][k - 1][3] += dp[i][j][k][3] ) %= MOD;
					}	
				}

			}
		}
	}

	//cout <<dp[5][1][1][1]<<endl;
	//cout <<dp[6][0][1][2]<<endl;
	//cout <<dp[7][0][0][0]<<endl;

	return dp[n][0][0][0];
}
int main() {
	freopen( "a.in", "r", stdin );
	freopen( "a.out", "w", stdout );

	int T;
	scanf( "%d", &T );

	for ( int cas = 1; cas <= T; cas ++ ) {
		scanf( "%s", s );
		n = strlen( s );

		int ret = calc( s );
		ret = ( ret - 1 + MOD ) % MOD;
		printf( "Case #%d: %d\n", cas, ret );
	}

	return 0;
}

```