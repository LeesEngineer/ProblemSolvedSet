# A. Rectangle Arrangement

</br>

![541f6c5131ec8fef8792afaf086106b5](https://github.com/user-attachments/assets/3fc71dc1-3c45-4f5c-b026-5b2fc96fa43f)

![2bbc075c02d266d584dd4f9bf2870810](https://github.com/user-attachments/assets/67b0c071-328c-4268-8dc2-a24e76d601c1)

![1129eedb92f246c1f4e5d51f4b14d109](https://github.com/user-attachments/assets/fab2ad6c-764d-4972-8f5b-d18fba5a8a36)

<p>我的第一次尝试，死活也解不出来</p>

```
#include <iostream>

using namespace std;

const int N = 100 + 10;

int w[N], h[N];

void insertionSort(int length) {
    for (int i = 1; i < length; i++) {
        int key = h[i];
        int k = w[i];
        int j = i - 1;
        
        // 将 h[i] 插入到已排序部分 h[0...i-1]，保持 w 的对应关系
        while (j >= 0 && h[j] < key) {
            h[j + 1] = h[j];
            w[j + 1] = w[j];
            j--;
        }
        h[j + 1] = key;
        w[j + 1] = k;
    }
}

int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int n;
        cin >> n;
        for(int i = 0; i < n; i++) cin >> w[i] >> h[i];
        
        insertionSort(n);  // 对 h 排序 

        int ans = (h[0] + w[0]) * 2;

        for(int i = 1; i < n; i++)  
        {
            // 因为 h 已排序，故只需处理 w 的变化
            if(w[i] > w[i - 1])
            {
                ans += 2 * (w[i] - w[i - 1]);
            }
        }
        cout << ans << endl;
    }
    return 0;
}
```

<p>第二次尝试，突然灵光乍现的产物</p>

```
#include <iostream>

using namespace std;

const int N = 110;

int w[N], h[N];

int max(int a[], int n)
{
    int max = 0;
    for(int i = 0; i < n; i++)
        if(max < a[i])
            max = a[i];
            
    return max;
}

int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        int n;
        cin >> n;
        for(int i = 0; i < n; i++)  cin >> w[i] >> h[i];
        
        int h_max = max(h, n);
        int w_max = max(w, n);
        
        int ans = (h_max + w_max) * 2;
        
        cout << ans << endl;
    }
    return 0;
}
```

</br>

#

































