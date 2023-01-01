## 代码1
```c++
#include <iostream>

using namespace std;

const int N = 1010;
int v[N], w[N];
int n, m;
int q[N][N];

int main() {
    cin >> n >> m;
    
    for (int i = 1; i <= n; i++) {
        cin >> v[i] >> w[i];
    }
    
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            q[i][j] = q[i - 1][j];
            if (j >= v[i]) {
                q[i][j] = max(q[i][j], q[i - 1][j - v[i]] + w[i]);
            }
        }
    }
    
    cout << q[n][m] << endl;
    
    return 0;
}
```

## 代码2
```c++
#include <iostream>

using namespace std;

const int N = 1010;
int v[N], w[N];
int n, m;
int q[N];

int main() {
    cin >> n >> m;
    
    for (int i = 1; i <= n; i++) {
        cin >> v[i] >> w[i];
    }
    
    for (int i = 1; i <= n; i++) {
        for (int j = m; j >= v[i]; j--) {
            q[j] = max(q[j], q[j - v[i]] + w[i]);
        }
    }
    
    cout << q[m] << endl;
    
    return 0;
}
```