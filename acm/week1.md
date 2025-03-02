</br>

# A - Telecasting station

</br>

<p>加权中位数（Weighted Median）</p>

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <iomanip>

using namespace std;

struct City {
    int x, p;
};

int main() {
    int n;
    cin >> n;
    
    vector<City> cities(n);
    long long total_population = 0;

    for (int i = 0; i < n; i++) {
        cin >> cities[i].x >> cities[i].p;
        total_population += cities[i].p;
    }

    sort(cities.begin(), cities.end(), [](City a, City b) {
        return a.x < b.x;
    });

    long long sum_population = 0;
    for (int i = 0; i < n; i++) {
        sum_population += cities[i].p;
        if (sum_population * 2 >= total_population) {
            cout << fixed << setprecision(5) << (double)cities[i].x << endl;
            break;
        }
    }

    return 0;
}
```






































































































































































































































































