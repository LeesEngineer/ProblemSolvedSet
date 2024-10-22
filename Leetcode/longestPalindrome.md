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

</br>

# myDPSolution

</br>

<p>对于一个子串而言，如果它是回文串，并且长度大于 2，那么将它首尾的两个字母去除之后，它仍然是个回文串。根据这样的思路，我们就可以用动态规划的方法解决本题。</p>

- 集合：表示字符串 s 的第 i 到 j 个字母组成的串
- 属性：dp(i, j)是否为回文数

`dp(i, j) = dp(i + 1, j - 1) && (s[i] == s[j])`

<p>也就是说，只有 s[i+1:j−1] 是回文串，并且 s 的第 i 和 j 个字母相同时，s[i:j] 才会是回文串。</p>

</br>

<p>上文的所有讨论是建立在子串长度大于 2 的前提之上的，我们还需要考虑动态规划中的边界条件，即子串的长度为 1 或 2。对于长度为 1 的子串，它显然是个回文串；对于长度为 2 的子串，只要它的两个字母相同，它就是一个回文串。因此我们就可以写出动态规划的边界条件</p>

`dp(i, i) = true`
`dp(i, i + 1) = (s[i] == s[i + 1])`

```
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<bool> > dp(n, vector<bool>(n, false));

        for(int i = 0; i < n; i++) dp[i][i] = true;

        for(int i = 0; i < n - 1; i++) dp[i][i + 1] = (s[i] == s[i + 1]);
        
        int i = 0;
        for(int j = 2; j < n; j++)
        {
            for(; i + j < n; i++)
                dp[i][i + j] = (dp[i + 1][i + j - 1] && (s[i] == s[i + j]));
            i = 0;
        }
        //第一次写这样的枚举方式
        //先枚举子串长度，再枚举起点


        int min_i = 0;
        int max_j = 0;
        int max = 1;
        for(int i = 0; i < n; i++)
            for(int j = i; j < n; j++)
                if((dp[i][j] == true) && ((j - i + 1) > max)) //找最大的j - i + 1
                {
                    min_i = i;
                    max_j = j;
                    max = (j - i + 1); //更新max，我就忘了
                }
        
        string ss(s.begin() + min_i, s.begin() + max_j + 1);
        return ss;
    }       
};
```

<p>934ms_26.2mb</p>

</br>

# 官方解答DP

</br>

```
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        if (n < 2) {
            return s;
        }

        int maxLen = 1;
        int begin = 0;
        // dp[i][j] 表示 s[i..j] 是否是回文串
        vector<vector<int>> dp(n, vector<int>(n));
        // 初始化：所有长度为 1 的子串都是回文串
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }
        // 递推开始
        // 先枚举子串长度
        for (int L = 2; L <= n; L++) {
            // 枚举左边界，左边界的上限设置可以宽松一些
            for (int i = 0; i < n; i++) {
                // 由 L 和 i 可以确定右边界，即 j - i + 1 = L 得
                int j = L + i - 1;
                // 如果右边界越界，就可以退出当前循环
                if (j >= n) {
                    break;
                }

                if (s[i] != s[j]) {
                    dp[i][j] = false;
                } else {
                    if (j - i < 3) {
                        dp[i][j] = true;
                    } else {
                        dp[i][j] = dp[i + 1][j - 1];
                    }
                }

                // 只要 dp[i][L] == true 成立，就表示子串 s[i..L] 是回文，此时记录回文长度和起始位置
                if (dp[i][j] && j - i + 1 > maxLen) {
                    maxLen = j - i + 1;
                    begin = i;
                }
            }
        }
        return s.substr(begin, maxLen);
    }
};
```

</br>

# 民解_DP

</br>

<p>直接正向或者反向遍历一次，然后移动j相当于一个字串</p>

```
class Solution {
public:
   string longestPalindrome(string s) {
       vector<vector<int>> dp(s.size(), vector<int> (s.size(),false));
       int result = 0;
       string str;
       for(int i = s.size()-1;i >= 0;i--){ 
           for(int j = i;j < s.size();j++){
               if(s[i] == s[j] && (j-i <= 1 || dp[i+1][j-1])) //j-i <= 1 : 长度为 1 或 2
               {
                   dp[i][j] = true;
                   result = max(result,j-i);
                   if(j-i == result) str = s.substr(i,j-i+1);
               }
           }
       }
       return str;
   }
};
```

<p>300ms_300mb</p>

# 中心扩展算法

<p>观察上述方法的状态转移方程：</p>

1. dp(i, i) = true
2. dp(i, i + 1) = (s[i] == s[i + 1])
3. dp(i, j) = dp(i + 1, j - 1) && (s[i] == s[j])

<p>找出其状态转移链</p>

`dp(i, j) <- dp(i + 1, j − 1) <- dp(i + 2, j − 2) <- ... <- "某一边界情况"`

<p>可以发现，所有的状态在转移的时候的可能性都是唯一的。也就是说，我们可以从每一种边界情况开始「扩展」，也可以得出所有的状态对应的答案。</p>

<p>边界情况即为子串长度为 1 或 2 的情况。我们枚举每一种边界情况，并从对应的子串开始不断地向两边扩展。如果两边的字母相同，我们就可以继续扩展，例如从 P(i+1,j−1) 扩展到 P(i,j)；如果两边的字母不同，我们就可以停止扩展，因为在这之后的子串都不能是回文串了。</p>

<p>「边界情况」对应的子串实际上就是我们「扩展」出的回文串的「回文中心」。该方法的本质即为：我们枚举所有的「回文中心」并尝试「扩展」，直到无法扩展为止，此时的回文串长度即为此「回文中心」下的最长回文串长度。我们对所有的长度求出最大值，即可得到最终的答案。</p>

```
class Solution {
public:
    pair<int, int> expandAroundCenter(const string& s, int left, int right) {
        while (left >= 0 && right < s.size() && s[left] == s[right]) {
            --left;
            ++right;
        }
        return {left + 1, right - 1};
    }

    string longestPalindrome(string s) {
        int start = 0, end = 0;
        for (int i = 0; i < s.size(); ++i) {
            auto [left1, right1] = expandAroundCenter(s, i, i);     //难道我是天才
            auto [left2, right2] = expandAroundCenter(s, i, i + 1); //果然，天才的想法总是不谋而合
            if (right1 - left1 > end - start) {
                start = left1;
                end = right1;
            }
            if (right2 - left2 > end - start) {
                start = left2;
                end = right2;
            }
        }
        return s.substr(start, end - start + 1);
    }
};
```

<p>7ms_8.25mb</p>

</br>

# Manacher

</br>

<p>Manacher算法是一种用于在线性时间内（O(n)）求解一个字符串的最长回文子串问题的算法。相比于传统的中心扩展方法（时间复杂度为 O(n²)），Manacher算法通过优化中心扩展的过程，大大提高了效率。</p>

<p>主要思想：Manacher算法通过记录和利用回文的对称性来加快查找过程。它会构造一个辅助字符串，将所有字符之间插入特殊字符（如 #），以确保奇数长度和偶数长度的回文能够统一处理。算法还维护一个变量 R 来表示回文的右边界，以及 C 来表示当前回文的中心。通过回文对称性，可以减少重复的中心扩展过程。</p>

<p>算法步骤：</p>

1.	预处理字符串：将原字符串中的每个字符间插入特殊字符，如 #，并在首尾也插入 ^ 和 $ 作为边界，防止越界问题。例如，原字符串 "abc" 会被转换为 ^#a#b#c#$。
2.	维护回文半径数组 P：P[i] 表示以位置 i 为中心的最大回文半径，P 数组初始为 0。
3.	遍历字符串：
-	对于每个位置 i，检查它是否在当前回文的右边界内（i < R）。如果在，可以利用回文对称性直接得到 P[i] 的初始值。
-	在此基础上，尝试进一步扩展当前中心的回文。
-	如果扩展后的回文超出了当前的右边界，则更新中心 C 和右边界 R。
4.	找到最长回文子串：遍历 P 数组，最大值对应的位置就是最长回文子串的中心，通过半径可以推导出它在原始字符串中的位置。</p>

```
class Solution {
public:
    int expand(const string& s, int left, int right) {
        while (left >= 0 && right < s.size() && s[left] == s[right]) {
            --left;
            ++right;
        }
        return (right - left - 2) / 2;
    }

    string longestPalindrome(string s) {
        int start = 0, end = -1;
        string t = "#";
        for (char c: s) {
            t += c;
            t += '#';
        }
        t += '#';
        s = t;

        vector<int> arm_len;
        int right = -1, j = -1;
        for (int i = 0; i < s.size(); ++i) {
            int cur_arm_len;
            if (right >= i) {
                int i_sym = j * 2 - i;
                int min_arm_len = min(arm_len[i_sym], right - i);
                cur_arm_len = expand(s, i - min_arm_len, i + min_arm_len);
            } else {
                cur_arm_len = expand(s, i, i);
            }
            arm_len.push_back(cur_arm_len);
            if (i + cur_arm_len > right) {
                j = i;
                right = i + cur_arm_len;
            }
            if (cur_arm_len * 2 + 1 > end - start) {
                start = i - cur_arm_len;
                end = i + cur_arm_len;
            }
        }

        string ans;
        for (int i = start; i <= end; ++i) {
            if (s[i] != '#') {
                ans += s[i];
            }
        }
        return ans;
    }
};
```

<p>Leetcode解释：</p>

![c0190418d7d85d4e67edd43831bf38c6](https://github.com/user-attachments/assets/18ac987a-7c60-424f-b650-58d04ede80bb)

![b2103b489fab30cc9e08d47d6a839f09](https://github.com/user-attachments/assets/a3caffb7-f114-4897-be07-d0ce5efcefdd)

![6648cbcd9c2cca6c3cf507de40549fba](https://github.com/user-attachments/assets/9ff45afa-0e4a-46e9-89c4-4b112b9ba144)



















