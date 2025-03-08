
# myFirstSolution

</br>

<p>观察回文数的形式，很容易让人想到从中心像两边扩展，不过要要兼顾到奇偶的情况</p>

```
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<int> dp(n, 0);
        
        //if(n == 1) return s;

        //处理奇数
        for(int i = 1; i < n - 1; i++)
            for(int j = 1; (i - j) >= 0 && (i + j) < s.size(); j++)
            {
                if(s[i - j] == s[i + j]) dp[i]++;
                else break;
            }

        int res = 0;
        for(int i = 0; i < n; i++) res = max(res, dp[i]);
        int m = 0;
        for(int j = 0; j < n; j++) if(res == dp[j]) m = j;


        //处理偶数
        dp = vector<int>(s.size(), 0);
        for(int k = 0; k < n - 1; k++)
            for(int i = k, j = k + 1; i >= 0 && j <= n - 1; i--, j++)
            {
                if(s[i] == s[j]) dp[k]++;
                else break;
            }

        int ans = 0;
        for(int i = 0; i < n - 1; i++) ans = max(ans, dp[i]);
        int k = 0;
        for(int j = 0; j < n - 1; j++) if(ans == dp[j]) k = j;

        
        string ss;

        if(res >= ans)
        {
            ss = string(s.begin() + m - res, s.begin() + m + res + 1);
            return ss;
        }

        ss = string(s.begin() + k + 1 - ans, s.begin() + k + 1 + ans);
        return ss;
    }
};
```

<p>15ms_9.25mb</p>

```
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1000 + 10;

bool dp[N][N];

class Solution {
public:
    string longestPalindrome(string s) {
        
        int n = s.size();

        for(int i = 0; i < n; i ++)
            dp[i][i] = true;

        for(int i = 0; i < n - 1; i ++)
            dp[i][i + 1] = (s[i] == s[i + 1]);

        for(int i = 2; i < n; i ++)
            for(int j = 0; i + j < n; j ++)
                dp[j][j + i] = (dp[j + 1][j + i - 1] && (s[j] == s[j + i]));

        int max_j, min_i;
        int max = 0;

        for(int i = 0; i < n; i ++)
            for(int j = i; j < n; j ++)
                if(dp[i][j] && (j - i + 1 > max))
                {
                    min_i = i, max_j = j, max = j - i + 1;
                }

        string ss(s.begin() + min_i, s.begin() + max_j + 1);

        return ss;
    }
};
```








