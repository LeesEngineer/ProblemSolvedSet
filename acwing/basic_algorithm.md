# 785.快速排序

</br>

```
#include <iostream>

using namespace std;

const int N = 1e6 + 10;

int n;
int q[N];

void quick_sort(int q[], int l, int r)
{
    if(l >= r) return; // l == r ok
    
    int x = q[(l + r) >> 1];
    int i = l - 1, j = r + 1;
    
    while(i < j)
    {
        do i ++; while(q[i] < x);
        do j --; while(q[j] > x);
        
        if(i < j) swap(q[i], q[j]);
    }
            
    quick_sort(q, l, j);
    quick_sort(q, j + 1, r);
}

int main()
{
    scanf("%d", &n);
    for(int i = 0; i < n; i ++ ) scanf("%d", &q[i]);
    
    quick_sort(q, 0, n - 1);
    
    for(int i = 0; i < n; i ++ ) printf("%d ", q[i]);
    
    return 0;
}
```

</br>

# 第 k 个数

</br>

<p>使用快速选择算法，时间复杂度是 O(n)</p>

<p>快速选择只需要递归一边</p>

```
#include <iostream>
#include <iostream>

using namespace std;

const int N = 1e6;

int q[N];
int n;

int quick_select(int q[], int l, int r, int k)
{
    if(l == r) return q[l];
    
    int x = q[(l + r) >> 1];
    int i = l - 1, j = r + 1;
    
    while(i < j)
    {
        do i ++; while(q[i] < x);
        do j --; while(q[j] > x);
        
        if(i < j) swap(q[i], q[j]);
    }
    
    int sl = j - l + 1;
    int sr = r - j;
    
    if(k <= sl) return quick_select(q, l, j, k); // 这里的等号要注意
    else return quick_select(q, j + 1, r, k - sl);
}

int main()
{
    int k;
    cin >> n >> k;
    for(int i = 0; i < n; i ++) cin >> q[i];
    
    cout << quick_select(q, 0, n - 1, k);
}
```

</br>

# 归并排序

</br>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e6;

int q[N];
int p[N];
int n;

void merge_sort(int q[], int l, int r)
{
    if(l == r) return;
    
    int mid = (l + r) >> 1;
    
    merge_sort(q, l, mid);
    merge_sort(q, mid + 1, r);
    
    int i = l, j = mid + 1, k = 0;
    while((i <= mid) && (j <= r))
    {
        if(q[i] < q[j]) p[k ++] = q[i ++];
        else p[k ++] = q[j ++];
    }
    if(i <= mid) copy(q + i, q + mid + 1, p + k);
    else copy(q + j, q + r + 1, p + k);
    
    copy(p, p + r - l + 1, q + l);
}

int main()
{
    cin >> n;
    for(int i = 0; i < n; i ++) cin >> q[i];
    
    merge_sort(q, 0, n - 1);
    
    for(int i = 0; i < n; i ++) cout << q[i] << " ";
}
```

</br>

# 逆序对的数量

</br>

<p><b>分治！！！！！</b></p>

<p>将逆序对分成三类</p>

- 都在左边：merge_sort(l, mid)

- 都在右边：merge_sort(mid + 1, r)

- 左右各一：在 (l, mid) 中大于 (mid + 1, r) 中第 i 个元素的元素的数量为 si

<p>要让归并排序的函数能在排序的同时返回区间内部逆序对的数量</p>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e6;

typedef long long LL;

int q[N], p[N];
int n;

LL merge_sort(int l, int r)
{
    if(l == r) return 0;
    
    int mid = (l + r) >> 1;
    
    LL x = merge_sort(l, mid) + merge_sort(mid + 1, r);
    
    int i = l, j = mid + 1, k = 0;
    while((i <= mid) && (j <= r))
    {
        if(q[i] <= q[j]) p[k ++] = q[i ++];
        else{
            x += mid - i + 1;
            p[k ++] = q[j ++];
        }
    }
    if(j <= r) copy(q + j, q + r + 1, p + k);
    else{
        copy(q + i, q + mid + 1, p + k);
        //int a = mid - i + 1;
        //x += a * (a - 1) / 2;
        //思维定式了，这里不需要
    }
    copy(p, p + r - l + 1, q + l);
    
    return x;
}

int main()
{
    cin >> n;
    for(int i = 0; i < n; i ++) cin >> q[i];
    
    cout << merge_sort(0, n - 1);
}
```

</br>

# 数的范围

</br>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e6;

int f[N];

int binary_1(int l, int r, int x) // 找左边界
{
    while(l < r)
    {
        int mid = (l + r) >> 1;
        if(f[mid] >= x) r = mid;
        else l = mid + 1;
    }
    if(f[l] != x) return -1;
    return l;
}

int binary_2(int l, int r, int x) // 找右边界
{
    while(l < r)
    {
        int mid = (l + r + 1) >> 1;
        if(f[mid] <= x) l = mid;
        else r = mid - 1;
    }
    if(f[l] != x) return -1;
    return l;
}

int main()
{
    int n, q;
    cin >> n >> q;
    
    for(int i = 0; i < n; i ++) cin >> f[i];
    for(int i = 0; i < q; i ++)
    {
        int p;
        cin >> p;
        cout << binary_1(0, n - 1, p) << " " << binary_2(0, n - 1, p);
        cout << endl;
    }
    return 0;
}
```

























































































