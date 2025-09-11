</br>

# A. Collatz Conjecture

</br>

<p>You are doing a research paper on the famous Collatz Conjecture. In your experiment, you start off with an integer 𝑥, and you do the following procedure 𝑘 times:</p>

- If 𝑥 is even, divide 𝑥 by 2.

- Otherwise, set 𝑥 to 3⋅𝑥+1.

<p>For example, starting off with 21 and doing the procedure 5 times, you get 21→64→32→16→8→4.</p>

<p>After all 𝑘 iterations, you are left with the final value of 𝑥. Unfortunately, you forgot the initial value. Please output any possible initial value of 𝑥.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤400). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑘 and 𝑥 (1≤𝑘,𝑥≤20).</p>

<b>Output</b>

<p>For each test case, print any possible initial value on a new line. It can be shown that the answer always exists.</p>

```
#include <iostream>

using namespace std;

int main()
{
    int t; 
    cin >> t;
    while(t --)
    {
        int k, x;
        cin >> k >> x;

        for(int i = 0; i < k; i ++)
            x *= 2;

        cout << x << endl;
    }
}
```

</br>

# B. Fun Permutation

</br>

<p>You are given a permutation∗ 𝑝 of size 𝑛.</p>

<p>Your task is to find a permutation 𝑞 of size 𝑛 such that GCD†(𝑝𝑖+𝑞𝑖,𝑝𝑖+1+𝑞𝑖+1)≥3 for all 1≤𝑖<𝑛. In other words, the greatest common divisor of the sum of any two adjacent positions should be at least 3.</p>

<p>It can be shown that this is always possible.</p>

<p>∗A permutation of length 𝑚 is an array consisting of 𝑚 distinct integers from 1 to 𝑚 in arbitrary order. For example, [2,3,1,5,4] is a permutation, but [1,2,2] is not a permutation (2 appears twice in the array), and [1,3,4] is also not a permutation (𝑚=3 but there is 4 in the array).</p>

<p>† gcd(𝑥,𝑦) denotes the greatest common divisor (GCD) of integers 𝑥 and 𝑦.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains an integer 𝑛 (2≤𝑛≤2⋅105).</p>

<p>The second line contains 𝑛 integers 𝑝1,𝑝2,…,𝑝𝑛 (1≤𝑝𝑖≤𝑛).</p>

<p>It is guaranteed that the given array forms a permutation.</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b></b>

<p>For each test case, output the permutation 𝑞 on a new line. If there are multiple possible answers, you may output any.</p>

```
#include <iostream>
#include <vector>
#include <numeric>

void solve() {
    int n;
    std::cin >> n;
    std::vector<int> p(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> p[i];
    }
    
    std::vector<int> q(n);
    
    for (int i = 0; i < n; ++i) {
        q[i] = n - p[i] + 1;
    }

    for (int i = 0; i < n; ++i) {
        std::cout << q[i] << (i == n - 1 ? "" : " ");
    }
    std::cout << "\n";
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);
    int t;
    std::cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```

</br>

# C. Maximum Even Sum

</br>

<p>You are given two integers 𝑎 and 𝑏. You are to perform the following procedure:</p>

<p>First, you choose an integer 𝑘 such that 𝑏 is divisible by 𝑘. Then, you simultaneously multiply 𝑎 by 𝑘 and divide 𝑏 by 𝑘.</p>

<p>Find the greatest possible even value of 𝑎+𝑏. If it is impossible to make 𝑎+𝑏 even, output −1 instead.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑎 and 𝑏 (1≤𝑎,𝑏≤𝑎⋅𝑏≤1018).</p>

<b>Output</b>

<p>For each test case, output the maximum even value of 𝑎+𝑏 on a new line.</p>

```
#include <iostream>

using namespace std;

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        long long a, b;
        cin >> a >> b;
        if(a*b & 1) cout << a*b+1 << endl;
        else
        {
            if(b & 1) cout << -1 << endl;
            else
            {
                if(a*b/2 & 1) cout << -1 << endl;
                else cout << a*b/2 + 2 << endl;
            }
        }
    }
}
```

</br>

# D. Replace with Occurrences

</br>

<p>Given an array 𝑎, let 𝑓(𝑥) be the number of occurrences of 𝑥 in the array 𝑎. For example, when 𝑎=[1,2,3,1,4], then 𝑓(1)=2 and 𝑓(3)=1.</p>

<p>You have an array 𝑏 of size 𝑛. Please determine if there is an array 𝑎 of size 𝑛 such that 𝑓(𝑎𝑖)=𝑏𝑖 for all 1≤𝑖≤𝑛. If there is one, construct it.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains an integer 𝑛 (1≤𝑛≤2⋅105).</p>

<p>The second line contains 𝑛 integers 𝑏1,𝑏2,…,𝑏𝑛 (1≤𝑏𝑖≤𝑛).</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b>Output</b>

<p>For each test case, output −1 if there is no valid array 𝑎.</p>

<p>Otherwise, print the array 𝑎 of 𝑛 integers on a new line. The elements should satisfy 1≤𝑎𝑖≤𝑛.</p>

```
#include <iostream>
#include <vector>

using namespace std;

const int N = 2e5 + 10;
int a[N];
vector<int> b[N];

int main()
{
    int t;
    cin >> t;
    while(t --)
    {   
        int n;
        cin >> n;
        for(int i = 0; i < n; i ++)
        {
            int c;
            cin >> c;
            b[c].push_back(i);
        }
        int flag = 0;
        int c = 0;
        for(int i = 1; i <= n; i ++)
        {
            if(b[i].size() % i != 0) 
            {
                flag = 1;
                break;
            }
            for(int j = 0; j < b[i].size(); j ++)
            {
                if(j % i == 0) c ++;
                a[b[i][j]] = c;
            }
        }
        if(flag) cout << -1;
        else
            for(int i = 0; i < n; i ++)
                cout << a[i] << " ";
        cout << endl;
        for(int i=1;i<=n;i++)b[i].clear();
    }
}
```

</br>

# E. Mexification

</br>

<p>You are given an array 𝑎 of size 𝑛 and an integer 𝑘. You do the following procedure 𝑘 times:</p>

<p>For each element 𝑎𝑖, you set 𝑎𝑖 to mex∗(𝑎1,𝑎2,…,𝑎𝑖−1,𝑎𝑖+1,𝑎𝑖+2,…,𝑎𝑛). In other words, you set 𝑎𝑖 to the mex of all other elements in the array. This is done for all elements in the array at the same time.</p>

<p>Please find the sum of elements in the array after all 𝑘 operations.</p>

<p>∗The minimum excluded (MEX) of a collection of integers 𝑑1,𝑑2,…,𝑑𝑘 is defined as the smallest non-negative integer 𝑥 which does not occur in the collection 𝑑.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line contains two integers 𝑛 and 𝑘 (2≤𝑛≤2⋅105,1≤𝑘≤109) – the number of elements in 𝑎 and the number of operations done.</p>

<p>The second line contains 𝑛 integers 𝑎1,𝑎2,…,𝑎𝑛 (0≤𝑎𝑖≤𝑛).</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b>Output</b>

<p>For each test case, output the sum of elements after all 𝑘 operations on a new line.</p>

```
#include <iostream>
#include <algorithm>
#include <cstring>

using namespace std;
typedef long long LL;

const int N = 2e5 + 10;
int a[N];
int c[N];

void solve(int n)
{
    memset(c, 0, sizeof c);

    int mex = -1;

    for(int i = 0; i < n; i ++) c[a[i]] ++;

    for(int i = 0; i <= n; i ++)
        if(!c[i])
        {
            mex = i;
            break;
        }
    
    for(int i = 0; i < n; i ++)
    {
        if(c[a[i]] == 1) a[i] = min(mex, a[i]);
        else a[i] = mex;
    }
}

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        int n, k;
        cin >> n >> k;
        for(int i = 0; i < n; i ++) cin >> a[i];

        if(k > 1)
            k = (1 << 1) + (k & 1);

        for(int i = 0; i < k; i ++) solve(n);

        LL res = 0;
        for(int i = 0; i < n; i ++) res += a[i];
        cout << res << endl;
    }
}
```

<p>依次介绍几种情况吧：</p>

1. 如果存在从零开始的排列，且排列内无重复数字

   - 第一次操作：属于排列的部分保持不变，剩下的变为 mex。
  
   - 第二次操作：.....M -> .....M+1
  
   - 第三次操作：.....M+1 -> .....M
  
   - 呈现周期性（波动性）

2. 如果存在从零开始的排列，但排列内有重复数字

   - 可能会出现一个或多个不从零开始的排列，但这些排列内无重复数字 -> OOOOO.....OOOOO......M or .....OOOOOM
  
   - -> M or .....M
  
   - 呈现周期性（波动性）

3. 可以证明所有情况都符合，

</br>

# F. Prefix Maximum Invariance

</br>

<p>Given two arrays 𝑥 and 𝑦 both of size 𝑚, let 𝑧 be another array of size 𝑚 such that the prefix maximum at each position of 𝑧 is the same as the prefix maximum at each position of 𝑥. Formally, max(𝑥1,𝑥2,…,𝑥𝑖)=max(𝑧1,𝑧2,…,𝑧𝑖) should hold for all 1≤𝑖≤𝑚. Define 𝑓(𝑥,𝑦) to be the maximum number of positions where 𝑧𝑖=𝑦𝑖 over all possible arrays 𝑧.</p>

<p>You are given two sequences of integers 𝑎 and 𝑏, both of size 𝑛. Please find the value of ∑𝑛𝑙=1∑𝑛𝑟=𝑙𝑓([𝑎𝑙,𝑎𝑙+1,…,𝑎𝑟],[𝑏𝑙,𝑏𝑙+1,…,𝑏𝑟]).</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains an integer 𝑛 (1≤𝑛≤2⋅105).</p>

<p>The second line contains 𝑛 integers 𝑎1,𝑎2,…,𝑎𝑛 (1≤𝑎𝑖≤2⋅𝑛).</p>

<p>The third line contains 𝑛 integers 𝑏1,𝑏2,…,𝑏𝑛 (1≤𝑏𝑖≤2⋅𝑛).</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b>Output</b>

<p>For each test case, output the sum of 𝑓([𝑎𝑙,𝑎𝑙+1,…,𝑎𝑟],[𝑏𝑙,𝑏𝑙+1,…,𝑏𝑟]) over all pairs of (𝑙,𝑟).</p>

```
#include<bits/stdc++.h>
using namespace std;
int a[200000],b[200000],l[200000];
int stk[200000],p;
int main(){
	ios::sync_with_stdio(false),cin.tie(0);
	int T,n,i,L,R,mid;
	long long ans;
	for(cin>>T;T>0;T--)
	{
		cin>>n;
		for(i=0;i<n;i++)cin>>a[i];
		for(i=0;i<n;i++)cin>>b[i];
		p=0;
		for(i=0;i<n;i++)
		{
			while(p>0&&a[stk[p-1]]<a[i])p--;
			if(a[i]==b[i])l[i]=i;
			else
			{
				L=-1;
				R=p;
				while(R-L>1)
				{
					mid=(L+R)/2;
					if(a[stk[mid]]>=max(a[i],b[i]))L=mid;
					else R=mid;
				}
				if(L==-1)l[i]=-1;
				else l[i]=stk[L];
			}
			stk[p]=i;
			p++;
		}
		ans=0;
		for(i=0;i<n;i++)ans+=(long long)(l[i]+1)*(long long)(n-i);
		cout<<ans<<'\n';
	}
	return 0;
}
```

</br>

# G. Cry Me a River

</br>

<p>There is a directed acyclic graph with 𝑛 nodes and 𝑚 edges. Each node is initially colored blue.</p>

<p>Let's define the fun graph game as follows:</p>

- Initially, a token is placed on node 𝑠

- Cry and River take turns moving the token to a node such that there exists a directed edge from its current position to that node, with Cry going first.

- Cry wins if the token ever reaches a node with no outgoing edges, after either player's turn.

- River wins if the token reaches a red node after either player's turn.

- If the players reach a node that is both red and does not have outgoing edges, River wins.

<p>Since the graph is acyclic, it can be shown that the game always ends in a finite number of turns.</p>

<p>Note that Cry and River can win the game immediately if the starting node 𝑠 doesn't have outgoing edges, or is red respectively.</p>

<p>You must handle 𝑞 queries of the following kind:</p>

- 1 u: update the color of node 𝑢 to red. It is guaranteed that node 𝑢 was blue before this update.

- 2 u: If a fun graph game is played with the token initially at node 𝑢, and both players play optimally, does Cry win?

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains three integers 𝑛, 𝑚, 𝑞 (2≤𝑛≤2⋅105 ,1≤𝑚,𝑞≤2⋅105).</p>

<p>The following 𝑚 lines each contain two integers 𝑢 and 𝑣 (1≤𝑢,𝑣≤𝑛), meaning that there is an edge from 𝑢 to 𝑣.</p>

<p>The following 𝑞 lines each contain two integers 𝑥 and 𝑢 (1≤𝑥≤2,1≤𝑢≤𝑛) – denoting the type of query and the node that the query is done on.</p>

<p>It is guaranteed that the given graph is a directed acyclic graph. Additionally, no edge is given more than once.</p>

<p>It is guaranteed that the sum of 𝑛, the sum of 𝑚, and the sum of 𝑞 each do not exceed 2⋅105 over all test cases.</p>

<b>Output</b>

<p>For each query of the second type, output YES if Cry wins. Otherwise, output NO. Each letter may be outputted in uppercase or lowercase.</p>

```
#include <iostream>
#include <cstring>

using namespace std;

const int N = 2e5 + 10;
int h[N], e[N], ne[N], idx, p[N];
int dp[N][2];

void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx ++;
}

void dfs(int u, int tag)
{
    if(dp[u][tag]) return;
    dp[u][tag] = 1;

    for(int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if(tag == 0) dfs(j, 1);
        else
        {
            p[j] --;
            if(!p[j]) dfs(j, 0);
        }
    }
}

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        memset(dp, 0, sizeof dp);
        memset(h, -1, sizeof h);
        memset(p, 0, sizeof p);
        idx = 0;

        int n, m, q;
        cin >> n >> m >>q;
        for(int i = 0; i < m; i ++)
        {
            int a, b;
            cin >> a >> b;
            add(b, a);
            p[a] ++;
        }

        while(q --)
        {
            int op, u;
            cin >> op >> u;
            if(op == 1)
            {
                dfs(u, 1);
                dfs(u, 0);
            }
            else
            {
                if(dp[u][0] == 0) cout << "YES" << endl;
                else cout << "NO" << endl;
            }
        }
    }
}
```

<p></p>




















































































































































































































































































































































