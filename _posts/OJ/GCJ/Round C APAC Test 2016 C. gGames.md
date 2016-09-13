# Problem

The country of elves is planning to hold an elimination tournament, and there are 2N elves who would like to take part. At the start of the tournament, they will be given unique ID numbers from 1 to 2N, and the Elf President will line them up in some order.

The tournament is a series of matches between two elves, and every match has one winner and one loser (there are no ties). In the first round, the first elf in the line competes against the second elf in the line, the third elf competes against the fourth elf, and so on. After the first round, the 2N-1 elves who lost leave the line, and the 2N-1 elves who won remain where they are. Then, the remaining elves play the second round in the same way: the first remaining elf in the line competes against the second remaining elf in the line, the third remaining elf competes against the fourth remaining elf, and so on. After N rounds, there will be only one elf remaining, and that elf is the winner.

M of the elves are sensitive, which means that they will be very sad if they have to compete in matches against their friends during the games. Specifically, the ith elf will be sad if they have to compete with their friends in the first Ki rounds. (Note that friendship is not necessarily mutual: if one elf considers another elf to be a friend, the other elf does not necessarily consider that elf to be a friend.)

The Elf President wants to know: is there a way to specify the initial positions of all 2N elves to guarantee that no elf will be sad, no matter what happens in the tournament?
# 题意
1到(1<<n)都是某高度为n的二叉树的叶节点，其中有m个节点不希望和某些其他点在至少k[i]的高度上祖先相同，求能否做到
# 思路
johng提供的思路是高度为n时，所有的节点祖先都相同，也就是说对于当前的树来说，状态为111111111...，==1代表某个节点在这棵树里==，于是这时可以检查是否违反条件，然后，把这些点分为两棵n-1高度的树，（一棵树是另一棵对于当前状态的异或），继续进行对子树存在的节点的审查，所有这些状态都可以通过dp数组记录结果进行==记忆搜索==，由于状态中1的数目会唯一决定当前所在子树大小，所以不会发生父亲和子树同时修改使用一个dp值的情况
# Code
```
//start of jonathanirvings' template v2.0.0 (BETA)
//省略
//end of jonathanirvings' template v2.0.0 (BETA)

int T;
int dp[1<<17];
int n,m,nn;
bool teman[20][20];
int k[20],e,K,b;
vi nyala[1<<17];
vi mungkin[1<<17];

int jahja(int bit,int tahap)
{
  if (__builtin_popcount(bit) == 1) return 1;
  int &ret = dp[bit];
  if (ret >= 0) return ret;
  ret = 0;
  REP(i,SIZE(nyala[bit]))
  {
    int x = nyala[bit][i];
    if (k[x] < tahap) continue;
    REP(j,n) if(teman[x][j] && (bit & (1 << j)))
    {
      return ret = 0;
    }
  }
  REP(i,SIZE(mungkin[bit]))
  {
    int temp1 = mungkin[bit][i];
    int temp2 = bit ^ temp1;
    ret |= (jahja(temp1,tahap-1) & jahja(temp2,tahap-1));
    if (ret > 0) return ret;
  }
  return ret;
}

int main()
{
  REP(i,(1<<16))
  {
    REP(j,16) if(i & (1 << j)) nyala[i].pb(j);
    REP(j,1 << SIZE(nyala[i]))
    {
      if (__builtin_popcount(j) == SIZE(nyala[i])/2)
      {
        int temp = 0;
        REP(k,SIZE(nyala[i])) if(j & (1 << k)) temp += (1 << nyala[i][k]);
        mungkin[i].pb(temp);
      }
    }
  }
  scanf("%d",&T);
  REPN(cases,T)
  {
    printf("Case #%d: ",cases);
    scanf("%d %d",&nn,&m);
    n = 1 << nn;
    RESET(teman,0);
    REP(i,n) k[i] = 0;
    TC(m)
    {
      scanf("%d %d %d",&e,&K,&b);
      k[e-1] = K;
      TC(b)
      {
        int x;
        scanf("%d",&x);
        teman[e-1][x-1] = 1;
      }
    }
    RESET(dp,-1);
    int risan = jahja((1 << n) - 1, nn);
    puts(risan ? "YES" : "NO");
  }
  return 0;
}
```