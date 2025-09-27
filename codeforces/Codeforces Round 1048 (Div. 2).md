</br>

# A. Maple and Multiplication

</br>

<p>Maple has two positive integers 𝑎 and 𝑏. She may perform the following operation any number of times (possibly zero) to make 𝑎 equal to 𝑏:</p>

<p>Choose any positive integer 𝑥, and multiply either 𝑎 or 𝑏 by 𝑥.</p>

<p>Your task is to determine the minimum number of operations required to make 𝑎 equal to 𝑏. It can be proven that this is always possible.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤100). The description of the test cases follows.</p>

<p>The first and only line of each test case contains two positive integers 𝑎 and 𝑏 (1≤𝑎,𝑏≤1000) — the numbers Maple currently has.</p>

<b>Output</b>

<p>For each test case, output a single integer representing the minimum number of operations Maple needs to make 𝑎 equal to 𝑏.</p>

```
#include <iostream>

using namespace std;

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        int a, b;
        cin >> a >> b;
        
        if(a == b)
        {
            cout << 0 << endl;
            continue;
        }
        else
        {
            if(((a % b) == 0) || ((b % a) == 0)) 
                cout << 1 << endl;
            else
                cout << 2 << endl;
        }

    }
}
```

</br>

# B. Cake Collection

</br>

<p>Maple wants to bake some cakes for Chocola and Vanilla.</p>

<p>One day, she discovers 𝑛 magical cake ovens. The 𝑖-th oven bakes 𝑎𝑖 cakes every second. The cakes remain in their respective ovens until they are collected.</p>

<p>At the end of each second, she may teleport to any oven (including the one she is currently at) and collect all the cakes that have accumulated in that oven up to that point.</p>

<p>Your task is to determine the maximum number of cakes Maple can collect in 𝑚 seconds.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤1000). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑛 and 𝑚 (1≤𝑛≤105, 1≤𝑚≤108) — the number of magical ovens and the number of seconds during which Maple will collect cakes.</p>

<p>The second line of each test case contains 𝑛 integers 𝑎1,𝑎2,…,𝑎𝑛 (1≤𝑎𝑖≤105) — the number of cakes the 𝑖-th oven bakes every second.</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b>Output</b>

<p>For each test case, output a single integer representing the maximum number of cakes Maple can collect in 𝑚 seconds.</p>

```
#include <iostream>
#include <algorithm>

using namespace std;
typedef long long ll;

const int N = 1e5 + 10;

ll a[N];

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        ll n, m;
        cin >> n >> m;

        for(int i = 1; i <= n; i ++)
            cin >> a[i];

        sort(a + 1, a + n + 1);

        ll ans = 0;
        if(m >= n)
        {
            ll k = m-n;
            for(ll i = n; i; i --)
                ans +=  a[i] * (k + i);
        }
        else
        {
            for(ll i = 0; i < m; i ++)
                ans += a[n-i] * (m - i);
        }

        cout << ans << endl;
    }
}
```

</br>

# C. Cake Assignment

</br>

<p>Chocola and Vanilla love cakes. Today, the manager of a cake shop gave them a total of 2𝑘+1 cakes. The cakes were distributed evenly, so each of them initially received 2𝑘 cakes.</p>

<p>However, Chocola and Vanilla now want to redistribute the cakes such that Chocola ends up with exactly 𝑥 cakes and Vanilla gets the remaining 2𝑘+1−𝑥 cakes.</p>

<p>In one step, they can perform exactly one of the following two operations:</p>

1. Chocola gives half of her cakes to Vanilla. This operation is only allowed if Chocola currently has an even number of cakes.

2. Vanilla gives half of her cakes to Chocola. This operation is only allowed if Vanilla currently has an even number of cakes.

<p>Your task is to determine the minimum number of steps required to reach the target distribution and to output any valid sequence of operations achieving that minimum.</p>

<p>It can be proven that, under the given constraints, a valid solution always exists, and the minimum number of steps required is at most 120.</p>

<b>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤1000). The description of the test cases follows.</b>

<p>The first line of each test case contains two integers 𝑘 and 𝑥 (1≤𝑘≤60, 1≤𝑥≤2𝑘+1−1) — each person initially received 2𝑘 cakes, and 𝑥 is the number of cakes Chocola should have after redistribution.</p>

<b>Output</b>

<p>For each test case, output a single integer 𝑛 (0≤𝑛≤120) representing the minimum number of steps required for them to redistribute the cakes accordingly.</p>

<p>On the next line, output 𝑛 integers 𝑜1,𝑜2,…,𝑜𝑛 (𝑜𝑖=𝟷 or 𝑜𝑖=𝟸), where 𝑜𝑖=𝟷 means that in the 𝑖-th step, Chocola gave half of her cakes to Vanilla (operation 1), and 𝑜𝑖=𝟸 means that Vanilla gave half of her cakes to Chocola (operation 2).</p>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 130;
typedef long long ll;

int ans[N];

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        int k;
        ll x;
        cin >> k >> x;

        ll tot = 1LL << (k+1);
        ll y = tot - x; 

        int op = 0;
        
        while(x != y)
        {
            if(y > x)
            {
                y -= x;
                x += x;
                ans[op] = 1;
            }
            else
            {
                x -= y;
                y += y;
                ans[op] = 2;
            }
            op ++;
        }
        cout << op << endl;

        for(int i = op-1; i >= 0; i --) cout << ans[i] << " ";
        cout << endl;
    }
}
```

</br>

# D. Antiamuny Wants to Learn Swap

</br>

<p>For an array 𝑏 of length 𝑚, you may perform the following two operations:</p>

1. Select an index 1≤𝑖≤𝑚−1. Then, swap the values of 𝑏𝑖 and 𝑏𝑖+1.

2. Select an index 1≤𝑖≤𝑚−2. Then, swap the values of 𝑏𝑖 and 𝑏𝑖+2.

<p>However, you can only perform operation 2 at most once.</p>

<p>We define 𝑓(𝑏) as the minimum number of operations (using both operation 1 and operation 2) required to sort array 𝑏 in non-decreasing order, and 𝑔(𝑏) as the minimum number of operations required to sort array 𝑏 in non-decreasing order using only operation 1.</p>

<p>The array 𝑏 is perfect if 𝑓(𝑏)=𝑔(𝑏). In other words, the ability to use operation 2 does not reduce the number of operations required to sort array 𝑏 compared to using only adjacent swaps.</p>

<p>You are given a permutation 𝑎 of length 𝑛∗, and must answer 𝑞 queries. Each query consists of two integers 𝑙 and 𝑟 (1≤𝑙≤𝑟≤𝑛), representing the subarray 𝑎[𝑙…𝑟]†. For each query, determine whether the subarray 𝑎[𝑙…𝑟] is perfect.</p>

<p>∗A permutation of length 𝑛 is an array consisting of 𝑛 distinct integers from 1 to 𝑛 in arbitrary order. For example, [2,3,1,5,4] is a permutation, but [1,2,2] is not a permutation (2 appears twice in the array), and [1,3,4] is also not a permutation (𝑛=3 but there is 4 in the array).</p>

<p>†The subarray 𝑎[𝑙…𝑟] includes all elements from index 𝑙 to 𝑟, i.e., [𝑎𝑙,𝑎𝑙+1,𝑎𝑙+2,…,𝑎𝑟].</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤5⋅104). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑛, 𝑞 (1≤𝑛,𝑞≤5⋅105) — the length of array 𝑎 and the number of queries.</p>

<p>The second line of each test case contains 𝑛 integers 𝑎1,𝑎2,…,𝑎𝑛 (1≤𝑎𝑖≤𝑛) — the elements in permutation 𝑎.</p>

<p>Each of the next 𝑞 lines contains two integers 𝑙 and 𝑟 (1≤𝑙≤𝑟≤𝑛) — the left and right endpoints of the queried subarray.</p>

<p>It is guaranteed that both the sum of 𝑛 and the sum of 𝑞 over all test cases do not exceed 5⋅105.</p>

<b>Output</b>

<p>For each test case, output "YES" if queried subarray 𝑎[𝑙…𝑟] is perfect, and "NO" otherwise.</p>

<p>You can output the answer in any case (upper or lower). For example, the strings "yEs", "yes", "Yes", and "YES" will be recognized as positive responses.</p>

```
#include <iostream>
#include <algorithm>
#include <cstring>

using namespace std;

const int N = 5e5 + 10;

int a[N], stk[N], p, nxt[N], R[N];
pair<int, int> b[N];
int n, m;

struct Node
{
    int l, r;
    int x;
} tr[N * 4];

void pushup(int u)
{
    tr[u].x = min(tr[u << 1].x, tr[u << 1 | 1].x);
}
void build(int u, int l, int r)
{
    if(l == r)
    {
        tr[u] = {l, r, R[l]};
        return;
    }

    tr[u] = {l, r};
    int mid = l + r >> 1;
    build(u << 1, l, mid), build(u << 1 | 1, mid + 1, r);
    pushup(u);
}
int query(int u, int l, int r)
{
    if(l <= tr[u].l && r >= tr[u].r)
        return tr[u].x;

    int mid = tr[u].l + tr[u].r >> 1;
    int v = n + 1;
    if(l <= mid) v = query(u << 1, l, r);
    if(r > mid) v = min(v, query(u << 1 | 1, l, r));
    return v;
}
void modify(int u, int x, int v)
{
    if(tr[u].l == tr[u].r)
    {
        tr[u].x = v;
        return;
    }
    int mid = tr[u].l + tr[u].r >> 1;
    if(x <= mid) modify(u << 1, x, v);
    else modify(u << 1 | 1, x, v);
    pushup(u);
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while(t --)
    {
        cin >> n >> m;
        for(int i = 1; i <= n; i++) cin >> a[i];

        p = 0;
        stk[p] = n + 1;
        for(int i = n; i; i --)
        {
            while(p != 0 && a[stk[p]] > a[i])
                p --;
            nxt[i] = stk[p];
            stk[++ p] = i;
        }
        
        for(int i = 1; i <= n; i ++) b[i] = {a[i], i};
        sort(b + 1, b + n + 1);
        for(int i = 1; i <= n; i ++) R[i] = n + 1;
        
        build(1, 1, n);
        
        for(int i = 1; i <= n; i ++)
        {
            R[b[i].second] = query(1, b[i].second, n);
            modify(1, b[i].second, nxt[b[i].second]);
        }

        build(1, 1, n);

        int l, r;
        while(m --)
        {
            cin >> l >> r;

            if(query(1, l, r) > r) cout << "YES\n";
            else cout << "NO\n";
        }
        
    }
}
```

</br>

# E1. Maple and Tree Beauty (Easy Version)

</br>

<p>Maple is given a rooted tree consisting of 𝑛 vertices numbered from 1 to 𝑛, where the root has index 1. Each vertex of the tree is labeled either zero or one. Unfortunately, Maple forgot how the vertices are labeled and only remembers that there are exactly 𝑘 zeros and 𝑛−𝑘 ones.</p>

<p>For each vertex, we define the name of the vertex as the binary string formed by concatenating the labels of the vertices from the root to the vertex. More formally, name1=label1 and name𝑢=name𝑝𝑢+label𝑢 for all 2≤𝑢≤𝑛, where 𝑝𝑢 is the parent of vertex 𝑢 and + represents string concatenation.</p>

<p>The beauty of the tree is equal to the length of the longest common subsequence∗ of the names of all the leaves†. Your task is to determine the maximum beauty among all labelings of the tree with exactly 𝑘 zeros and 𝑛−𝑘 ones.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤50). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑛 and 𝑘 (2≤𝑛≤1000, 0≤𝑘≤𝑛) — the number of vertices and the number of vertices labeled with zero, respectively.</p>

<p>The second line contains 𝑛−1 integers 𝑝2,𝑝3,…,𝑝𝑛 (1≤𝑝𝑖≤𝑖−1) — the parent of vertex 𝑖.</p>

<p>Note that there are no constraints on the sum of 𝑛 over all test cases.</p>

<b>Output</b>

<p>For each test case, output a single integer representing the maximum beauty among all labelings of the tree with exactly 𝑘 zeros and 𝑛−𝑘 ones.</p>

```
#include <iostream>
#include <cstring>

using namespace std;

const int N = 1010;

int depth[N], w[N], isroot[N], dp[N][N];

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        int n, k;
        cin >> n >> k;

        memset(depth, 0, sizeof depth);
        memset(w, 0, sizeof w);
        memset(isroot, 0, sizeof isroot);
        memset(dp, 0, sizeof dp);

        depth[1] = 1;
        w[1] = 1;
        for(int i = 2; i <= n; i ++)
        {
            int x;
            cin >> x;
            depth[i] = depth[x] + 1;
            w[depth[i]] ++;
            isroot[x] = 1;
        }

        int d = n + 1;
        for(int i = 1; i <= n; i ++)
            if(!isroot[i]) d = min(d, depth[i]);

        int rest = 0;
        for(int i = 1; i <= n; i ++)
            if(depth[i] > d) rest ++;

        dp[0][0] = 1;
        for(int i = 1; i <= d; i ++)
            for(int j = 0; j <= k; j ++)
            {
                dp[i][j] = dp[i-1][j];
                if(j >= w[i] && dp[i-1][j-w[i]]) dp[i][j] = 1;
            }
        
        int m;
        for(int i = 0; i <= k; i ++)
            if(dp[d][i]) m = i;

        int x = k - m;
        if(x <= rest) cout << d;
        else cout << d-1;
        cout << endl;
    }
}
```

<b>hard version</b>

```
#include <iostream>
#include <cstring>
#include <bitset>

using namespace std;

const int N = 2e5 + 10;

int depth[N], w[N], isroot[N];
bitset<N> dp;

int main()
{
    int t;
    cin >> t;
    while(t --)
    {
        memset(depth, 0, sizeof depth);
        memset(w, 0, sizeof w);
        memset(isroot, 0, sizeof isroot);
        depth[1] = 1;
        w[1] = 1;
        dp.reset();

        int n, k;
        cin >> n >> k;
        for(int i = 2; i <= n; i ++)
        {
            int x;
            cin >> x;
            depth[i] = depth[x] + 1;
            w[depth[i]] ++;
            isroot[x] = true;
        }

        int d = n + 1;
        for(int i = 1; i <= n; i ++)
            if(!isroot[i])
                d = min(d, depth[i]);

        int rest = 0;
        for(int i = 1; i <= n; i ++)
            if(depth[i] > d)
                rest ++;

        dp[0] = 1;
        for(int i = 1; i <= d; i ++)
            dp |= dp << w[i];
        
        int m;
        for(int i = 0; i <= k; i ++)
            if(dp[i])
                m = i;

        int x = k - m;
        if(x <= rest) cout << d;
        else cout << d-1;
        cout << endl;
    }
}
```

































































































































































































































































































































































































































































































