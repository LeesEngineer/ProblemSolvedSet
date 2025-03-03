# A - 水仙花数

![649fa856-deac-4170-a9e7-933c791da159](https://github.com/user-attachments/assets/47daae61-0509-4e03-8c43-260aeb6cbb76)

```
#include <algorithm>
#include <iostream>
#include <cmath>

using namespace std;

int f[5];

int main()
{
    int t;
    cin >> t;

    int x = 0;
    while(true)
    {
        int n = t ++;
        
        int a = 0;
        for(int i = 0; i < 4; i ++)
        {
            if(n == 0) break;
            f[i] = n % 10;
            n /= 10;
            a ++;
        }
        
        x = 0;
        for(int i = 0; i < a; i ++)
            x += pow(f[i], a);
        
        if(x == t - 1) break;
    }
    cout << x;
}
```

# B - 亲和数

![47f707e2-5951-4dcb-8d51-2602de4e015d](https://github.com/user-attachments/assets/3053e80f-d01b-41a6-80fd-54598cc08881)

```
#include <iostream>
#include <unordered_map>

using namespace std;

// 计算一个数的所有真因子之和
int sumof(int value)
{
    int sum = 0;
    for (int i = 1; i <= value / 2; i++)
    {
        if (value % i == 0)
        {
            sum += i;
        }
    }
    return sum;
}

int main()
{
    int n;
    cin >> n;
    int i = n;

    unordered_map<int, int> m; // 记录每个数的 sumof 值

    while (true)
    {
        int x = sumof(i);
        
        // 检查是否满足亲和数的条件： sumof(x) == i 且 i != x
        if (x != i && sumof(x) == i)
        {
            cout << i << " " << x << endl;
            break; // 找到后退出
        }

        i++;
    }

    return 0;
}
```

# C - Switches and Lamps

![60f5fc17-e972-49a4-a4fc-78fd4bba0b5a](https://github.com/user-attachments/assets/1d81351f-e73e-49bb-8566-f65335da2b8e)

![ac3957b7-f821-4474-b06f-ae5c407d576e](https://github.com/user-attachments/assets/0ceaf5d0-a768-47c5-8228-853c3bc3ae6e)

```

```

# D - Calling Extraterrestrial Intelligence Again

![2c2f98e5-702e-48cd-b40c-26986d53ed12](https://github.com/user-attachments/assets/c45eb9c2-3e8a-4d12-85e5-ee923114e572)

![5f879745-ad91-4f84-8f89-0d4e816d7365](https://github.com/user-attachments/assets/a55c5ccd-be2c-455a-8f60-c3ea9779044c)

```

```

# E - The Clocks

![1dbdb3ea-59d0-4f77-bae5-00096c747928](https://github.com/user-attachments/assets/af2298ad-5552-4bf2-9ecf-a9055a22445e)

![f312247c-5f99-4bc4-ad12-42df5355dc2a](https://github.com/user-attachments/assets/4e5737e1-d89e-4e59-ac1f-e7dbbcb7d0f6)

```

```

# F - Integer Approximation

![a33288e9-225f-4f7a-937b-cf365c27f264](https://github.com/user-attachments/assets/cb2f168e-3ba6-42fd-93b0-2d01f4f8f6a9)

```

```















































































































































































































































































