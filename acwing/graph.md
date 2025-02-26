</br>

# 排列数字

</br>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 10;

int path[N];
int st[N];
int n;

void dfs(int u)
{
    if(u == n)
    {
        for(int i = 0; i < n; i ++) cout << path[i] << " ";
        cout << endl;
        return;
    }
    for(int i = 1; i <= n; i ++)
        if(!st[i])
        {
            path[u] = i;
            st[i] = true;
            dfs(u + 1);
            st[i] = false;
        }
}

int main()
{
    cin >> n;
    
    dfs(0);
    
    return 0;
}
```

</br>

# N皇后

</br>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 20;

char g[N][N];
int col[N], dg[N], udg[N];
int n;

void dfs(int u)
{
    if(u == n)
    {
        for(int i = 0; i < n; i ++)
        {
            for(int j = 0; j < n; j ++) cout << g[i][j];
            cout << endl;
        }
        cout << endl;
        return;
    }
    
    for(int i = 0; i < n; i ++)
        if(!col[i] && !dg[n - i + u] && !udg[i + u])
        {
            g[u][i] = 'Q';
            col[i] = dg[n - i + u] = udg[i + u] = true;
            dfs(u + 1);
            col[i] = dg[n - i + u] = udg[i + u] = false;
            g[u][i] = '.';
        }
}

int main()
{
    cin >> n;
    for(int i = 0; i < n; i ++)
        for(int j = 0; j < n; j ++)
            g[i][j] = '.';
            
    dfs(0);
    
    return 0;
}
```

```
一开始写的
const int N = 10;
报错了。应该是 dg 溢出
```










































































































































































































