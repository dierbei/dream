## 1. 题解
> https://www.acwing.com/activity/content/problem/content/907/

## 2. 代码
```c++
#include <iostream>
#include <queue>
#include <cstring>

using namespace std;

const int N = 110;
int g[N][N], d[N][N];
int n, m;

typedef pair<int, int>PII;

int bfs() {
    memset(d, -1, sizeof d);
    d[0][0] = 0;
    
    
    queue<PII> q;
    q.push({ 0, 0 });
    
    int dx[4] = { -1, 0, 1, 0 }, dy[4] = { 0, 1, 0, -1 };
    
    while (q.size()) {
        auto t = q.front();
        q.pop();
        
        for (int i = 0; i < 4; i++) {
            int x = t.first + dx[i], y = t.second + dy[i];
            
            if (x >= 0 && x < n && y >= 0 && y < m && g[x][y] == 0 && d[x][y] == -1) {
                d[x][y] = d[t.first][t.second] + 1;
                q.push({ x, y });
            }
        }
    }
    
    return d[n - 1][m - 1];
}

int main() {
    cin >> n >> m;
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> g[i][j];
        }
    }
    
    cout << bfs() << endl;
    
    return 0;
}
```