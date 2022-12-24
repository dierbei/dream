## 1. 题解
> https://www.acwing.com/activity/content/code/content/47097/

## 2. 代码
```c++
#include <iostream>

using namespace std;

const int N = 20;

char g[N][N];
bool col[N], dg[N], edg[N];

int n;

void dfs(int u) {
    if (u == n) {
        for (int i = 0; i < n; i++) {
            cout << g[i] << endl;
        }
        cout << endl;
        
        return;
    }
    
    for (int i = 0; i < n; i++) {
        if (!col[i] && !dg[u + i] && !edg[n - u + i]) {
            g[u][i] = 'Q';
            col[i] = dg[u + i] = edg[n - u + i] = true;
            
            dfs(u + 1);
            
            g[u][i] = '.';
            col[i] = dg[u + i] = edg[n - u + i] = false;
        }
    }
}

int main() {
    cin >> n;
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            g[i][j] = '.';
        }
    }
    
    dfs(0);
    
    return 0;
}
```