</br>

# A. Twice

![11958bb0af25b963b719dfd8f95e0f20](https://github.com/user-attachments/assets/4d753992-93c2-4a16-9dfb-e460463712e5)

![2f498f875a197e6ae57b737bec3702a5](https://github.com/user-attachments/assets/3a2f067d-d566-424d-a25c-acdb0f4944bc)

</br>

```
 #include <iostream>
#include <algorithm>

using namespace std;

const int N = 30;
int f[N];

int main()
{
    int t;
    scanf("%d", &t);
    while(t --)
    {
        int n;
        scanf("%d", &n);
        for(int i= 0; i < n; i++)
            scanf("%d",  &f[i]);
        
        
        for(int j = 1; j < n; j ++)
        {
            int i = j - 1;
            int k =  f[j];
            while(i >= 0 && k < f[i])
            {
                f[i + 1] = f[i];
                i --;
            }
            f[i + 1] = k;
        }
        
        //sort(f, f + n);
        
        //for(int i = 0 ; i < n; i ++) cout << f[i] << "   ";
        
        

        int ans = 0;
        int prev = f[0];
        int res = 1;
        for(int i = 1 ; i < n; i ++)
        {
            if(prev == f[i])
            {
                res ++;
            }
            else
            {
                ans += res / 2;
                res = 1;
                prev = f[i];
            }
        }
        ans += res / 2;
        printf("%d\n", ans);
    }
    return 0;
}
```

</br>

# B. Intercepted Inputs

</br>

![4ded258712cd006d9a16cfcf1934fc52](https://github.com/user-attachments/assets/8765abe0-0c3b-46c7-a1b3-af266ef50571)

![5c60ecc756c021ac2ef08fbbb9f1a8ee](https://github.com/user-attachments/assets/82200d45-4c80-42c6-b645-0822a0a21df1)

```
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

const int N = 1e7;

int f[N];

int main()
{
    int t;
    scanf("%d", &t);

    while(t --)
    {
        map<int, int> m;
        int n;
        scanf("%d", &n); 
        for(int i = 0; i < n; i++)
        {
            scanf("%d", &f[i]);
            m[f[i]] = f[i];
        }
        //for(int i = 0 ; i < n ; i++) printf("%d", f[i]);
        //printf("\n");
        int k = n - 2;
        for(auto i = m.begin(); i != m.end(); i ++)
        {
            if(i -> first == 0) continue;
            auto n = m.find(k / i -> first);
            if(n != m.end() && (n -> second * i -> first == k))
            {
                printf("%d %d\n", n -> first, i -> first);
                break;
            }
        }
    }
}
```































