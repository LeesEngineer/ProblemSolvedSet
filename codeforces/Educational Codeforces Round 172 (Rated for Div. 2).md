# A. Greedy Monocarp

</br>

## 题目

</br>

<p>每次测试的时间限制：2 秒</p>

<p>每次测试的内存限制：512 兆字节</p>

<p>有 $n$ 个箱子；第 $i$ 个箱子最初包含 $a_i$ 个硬币。对于每个箱子，您可以选择任意非负数（ $0$ 或更大）的硬币数量添加到该箱子中，但有一个限制：所有箱子中的硬币总数必须至少为 $k$ 。

在您向箱子中添加完硬币后，贪婪的 Monocarp 来了，他想要硬币。他会一个接一个地拿走箱子，而且由于他很贪婪，他总是会选择硬币数量最多的箱子。一旦他拿走的箱子中的硬币总数至少为 $k$ ，Monocarp 就会停止。

您希望 Monocarp 拿走尽可能少的硬币，因此您必须以这样的方式将硬币添加到箱子中，以便当 Monocarp 停止拿走箱子时，他将拥有 **恰好 $k$ ** 个硬币。计算您必须添加的最少硬币数量。</p>

</br>

<b>输入</b>

<p>第一行包含一个整数 $t$ ( $1 \le t \le 1000$ ) — 测试用例的数量。</p>

<p>每个测试用例包含两行：</p>

- 第一行包含两个整数 $n$ 和 $k$ ( $1 \le n \le 50$ ; $1 \le k \le 10^7$ )；
- 第二行包含 $n$ 个整数 $a_1, a_2, \dots, a_n$ ( $1 \le a_i \le k$ )。

</br>

<b>输出</b>

<p>对于每个测试用例，打印一个整数 — 您必须添加的最小硬币数量，以便当 Monocarp 停止拿走箱子时，他有 **恰好 $k$ ** 个硬币。可以证明，在问题的约束下，这总是可能的。</p>

```
input:
4
5 4
4 1 2 3 2
5 10
4 1 2 3 2
2 10
1 1
3 8
3 3 3
```

```
output:
0
1
8
2
```

<p>**注意**

在示例的第一个测试用例中，您不必添加任何硬币。当 Monocarp 到达时，他将拿走装有 $4$ 个硬币的箱子，因此他将拥有恰好 $4$ 个硬币。

在示例的第二个测试用例中，您可以将 $1$ 个硬币添加到第 $4$ 个箱子中，因此，当 Monocarp 到达时，他将拿走一个装有 $4$ 个硬币的箱子，然后拿走另一个装有 $4$ 个硬币的箱子，以及一个装有 $2$ 个硬币的箱子。

在示例的第三个测试用例中，您可以将 $3$ 个硬币添加到第 $1$ 个箱子中，并将 $5$ 个硬币添加到第 $2$ 个箱子中。

在示例的第四个测试用例中，你可以将 $1$ 枚硬币添加到第 $1$ 枚箱子中，将 $1$ 枚硬币添加到第 $3$ 枚箱子中。</p>

</br>

## 题解

</br>

```
#include <iostream>
#include <algorithm>
#include <functional>

using namespace std;

const int N = 60;

int f[N];

int main()
{
    int t;
    scanf("%d", &t);
    while(t --)
    {
        int n, k;
        scanf("%d%d", &n, &k);
        for(int i = 0; i < n; i++) scanf("%d", &f[i]);

        //for(int i = 0; i < n; i++) cout << f[i] << " "; cout << endl;

        sort(f, f + n, greater<int>());

        //for(int i = 0; i < n; i++) cout << f[i] << " "; cout << endl;

        for(int i = 0; i < n; i++) f[i] += f[i - 1];

        //for(int i = 0; i < n; i++) cout << f[i] << " "; cout << endl;

        for(int i = 0; i < n; i ++)
        {
            if(f[i] == k)
            {
                printf("0\n");
                break;
            }

            if(f[i] > k)
            {
                int ans = k - f[i - 1];
                printf("%d\n", ans);
                break;
            }
        }
        if(k - f[n - 1] > 0)
        {
            int ans = k - f[n - 1];
            printf("%d\n", ans);
        }
    }
    return 0;
}
```











