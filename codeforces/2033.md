# A. Sakurako and Kosuke

</br>

![09049aa32f98448e67bd9a727b38af4c](https://github.com/user-attachments/assets/0bacbdb5-e1bf-42d5-ae71-137b7cf09921)

![221643100e17062e99cae5c792a191a1](https://github.com/user-attachments/assets/c0593e26-aabc-43b4-931b-7d856b77c34e)

<b>constructive algorithms, math</b>

<p>构造性算法关注如何一步一步地构造出满足条件的解：</p>

- 直接构造解：构造性算法通常不会遍历所有可能的解，而是通过问题的条件和约束来一步步构建一个有效解。
- 策略性构建：通常需要根据问题的性质制定策略，确保在构造过程中不会出现冲突或不符合题目要求的情况。
-	顺序生成解：许多构造性算法都是从空解开始，按照一定规则依次添加元素，直到完成整个解。例如，矩阵填充问题、图的构建问题等常常采用这种方法。

<p>举例：在一个棋盘填充问题中，我们可能会被要求放置棋子，使得彼此不相互攻击。构造性算法可能会按行或按列逐个放置棋子，并在每次放置后确保没有冲突，这样逐步构造出满足条件的解。</p>

```
#include <iostream>

using namespace std;

int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int n;
        cin >> n;
        
        int pos = 0;
        int i = 1;
        while(true)
        {
            
            pos -= 2 * i - 1;
            if(abs(pos) > n)
            {
                cout << "Sakurako" << endl;
                break;
            }
            i++;
            
            pos += 2 * i - 1;
            if(abs(pos) > n)
            {
                cout << "Kosuke" << endl;
                break;
            }
            i++;
        }
    }
    return 0;
}
```

<b>模拟了游戏的流程</b>

</br>

# B. Sakurako and Water

</br>

![e4e8d385512ef63ef4d1450907d4166d](https://github.com/user-attachments/assets/b4e228f5-4a4b-4b93-9630-4afade33b287)

![978470748e75e9ee6744dc086a5b518b](https://github.com/user-attachments/assets/014aa082-8c26-460a-b509-38c68caae212)

<b>constructive algorithms, greedy</b>

```
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<vector<int>> a(n, vector<int>(n));
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> a[i][j];

        int operations = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (a[i][j] < 0) {
                    // We can perform magic here, and increase the diagonal
                    int delta = -a[i][j];
                    operations += delta;
                    for (int k = 0; k < n - max(i, j); k++) {
                        if (i + k < n && j + k < n) {
                            a[i + k][j + k] += delta;
                        }
                    }
                }
            }
        }

        cout << operations << endl;
    }
    return 0;
}
```

</br>

# D. Kousuke's Assignment

</br>

![ce4cde7cca4bea54e77f82e2cea1eed7](https://github.com/user-attachments/assets/26cfaf65-2cae-44f1-8197-6bef5fc27b13)

<p>我的代码在test5就TLE了</p>

```
#include <iostream>

using namespace std;

const int N = 1e5 + 10;

int a[N], sum[N];

int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int dp = 0;
        int prev = 0;
        int n;
        cin >> n;
        for(int i = 1; i <= n; i++) cin >> a[i];
        
        for(int i = 1; i <= n; i++) sum[i] = sum[i - 1] + a[i];
        
        for(int i = 1; i <= n; i++)
            for(int j = 1; j <= i; j++)
                if(j > prev && (sum[i] - sum[j - 1] == 0))
                {
                    prev = i;
                    dp++;
                    break;
                }
        cout << dp << endl;
    }
}
```

<p>第二次在test9遇到了整数溢出</p>

```
#include <iostream>
#include <unordered_map>

using namespace std;

const int N = 1e5 + 10;

int a[N];
int sum[N];

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;

        for (int i = 1; i <= n; i++) cin >> a[i];
        
        unordered_map<int, int> last_occurrence;
        last_occurrence[0] = 0; // 初始化0的出现位置
        int dp = 0;             // 记录当前的“美丽段”数量
        int last_position = 0;  // 记录上一个“美丽段”结束的位置
        
        sum[0] = 0;
        for (int i = 1; i <= n; i++) {
            sum[i] = sum[i - 1] + a[i];
            
            if (last_occurrence.count(sum[i])) {
                int pos = last_occurrence[sum[i]];
                if (pos >= last_position) {
                    dp++;
                    last_position = i; // 只有在找到新“美丽段”时更新
                }
            }
            
            last_occurrence[sum[i]] = i; // 更新当前前缀和的位置
        }

        cout << dp << endl;
    }
    
    return 0;
}
```

<p>改为long long，同时优化一下</p>

```
#include <iostream>
#include <unordered_map>

using namespace std;

const int N = 1e5 + 10;

int a[N];

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;

        for (int i = 1; i <= n; i++) cin >> a[i];

        unordered_map<long long, int> prefix_sum_map;
        prefix_sum_map[0] = 0; // 初始化前缀和为0的位置
        int dp = 0;
        int last_position = 0;
        long long current_sum = 0;

        for (int i = 1; i <= n; i++) {
            current_sum += a[i];

            if (prefix_sum_map.count(current_sum)) {
                int pos = prefix_sum_map[current_sum];
                if (pos >= last_position) {
                    dp++;
                    last_position = i;
                }
            }

            prefix_sum_map[current_sum] = i;
        }

        cout << dp << endl;
    }

    return 0;
}
```





























