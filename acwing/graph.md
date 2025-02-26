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

</br>

# 走迷宫

</br>

```
#include <iostream>
#include <algorithm>
#include <cstring>

using namespace std;

const int N = 110;

int g[N][N];
int d[N][N];
pair<int, int> q[N * N];
int n, m;

int bfs()
{
    memset(d, -1, sizeof d);
    d[0][0] = 0;
    q[0] = {0, 0};
    int hh = 0, tt = 0;
    
    int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, -1, 0, 1};
    while(hh <= tt)
    {
        auto t = q[hh ++];
        
        for(int i = 0; i < 4; i ++)
        {
            int x = t.first + dx[i], y = t.second + dy[i];
            if((x >= 0) && (x < n) && (y >= 0) && (y < m) && (d[x][y] == -1) && (g[x][y] == 0))
            {
                q[++ tt] = {x, y};
                d[x][y] = d[t.first][t.second] + 1;
            }
        }
        
    }
    return d[n - 1][m - 1];
}

int main()
{
    cin >> n >> m;
    for(int i = 0; i < n; i ++)
        for(int j = 0; j < m; j ++)
            cin >> g[i][j];
    
    cout << bfs();
    
    return 0;
}
```








































































































































































































