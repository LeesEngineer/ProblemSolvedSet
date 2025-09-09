</br>

# A. Collatz Conjecture

</br>

<p>You are doing a research paper on the famous Collatz Conjecture. In your experiment, you start off with an integer 𝑥, and you do the following procedure 𝑘 times:</p>

- If 𝑥 is even, divide 𝑥 by 2.

- Otherwise, set 𝑥 to 3⋅𝑥+1.

<p>For example, starting off with 21 and doing the procedure 5 times, you get 21→64→32→16→8→4.</p>

<p>After all 𝑘 iterations, you are left with the final value of 𝑥. Unfortunately, you forgot the initial value. Please output any possible initial value of 𝑥.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤400). The description of the test cases follows.</p>

<p>The first line of each test case contains two integers 𝑘 and 𝑥 (1≤𝑘,𝑥≤20).</p>

<b>Output</b>

<p>For each test case, print any possible initial value on a new line. It can be shown that the answer always exists.</p>

```
#include <iostream>

using namespace std;

int main()
{
    int t; 
    cin >> t;
    while(t --)
    {
        int k, x;
        cin >> k >> x;

        for(int i = 0; i < k; i ++)
            x *= 2;

        cout << x << endl;
    }
}
```

</br>

# B. Fun Permutation

</br>

<p>You are given a permutation∗ 𝑝 of size 𝑛.</p>

<p>Your task is to find a permutation 𝑞 of size 𝑛 such that GCD†(𝑝𝑖+𝑞𝑖,𝑝𝑖+1+𝑞𝑖+1)≥3 for all 1≤𝑖<𝑛. In other words, the greatest common divisor of the sum of any two adjacent positions should be at least 3.</p>

<p>It can be shown that this is always possible.</p>

<p>∗A permutation of length 𝑚 is an array consisting of 𝑚 distinct integers from 1 to 𝑚 in arbitrary order. For example, [2,3,1,5,4] is a permutation, but [1,2,2] is not a permutation (2 appears twice in the array), and [1,3,4] is also not a permutation (𝑚=3 but there is 4 in the array).</p>

<p>† gcd(𝑥,𝑦) denotes the greatest common divisor (GCD) of integers 𝑥 and 𝑦.</p>

<b>Input</b>

<p>Each test contains multiple test cases. The first line contains the number of test cases 𝑡 (1≤𝑡≤104). The description of the test cases follows.</p>

<p>The first line of each test case contains an integer 𝑛 (2≤𝑛≤2⋅105).</p>

<p>The second line contains 𝑛 integers 𝑝1,𝑝2,…,𝑝𝑛 (1≤𝑝𝑖≤𝑛).</p>

<p>It is guaranteed that the given array forms a permutation.</p>

<p>It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.</p>

<b></b>

<p>For each test case, output the permutation 𝑞 on a new line. If there are multiple possible answers, you may output any.</p>

```
#include <iostream>
#include <vector>
#include <numeric>

void solve() {
    int n;
    std::cin >> n;
    std::vector<int> p(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> p[i];
    }
    
    std::vector<int> q(n);
    
    for (int i = 0; i < n; ++i) {
        q[i] = n - p[i] + 1;
    }

    for (int i = 0; i < n; ++i) {
        std::cout << q[i] << (i == n - 1 ? "" : " ");
    }
    std::cout << "\n";
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);
    int t;
    std::cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```




































































































































































































































































































































































































