## 1. 代码
```go
package main

import "fmt"

const N = 8

var col [N]bool
var dg [N]bool
var udg [N]bool
var g [N][N]string

var n = 4

func dfs(u int) {
	if u == n {
		for i := 0; i < n; i++ {
			fmt.Println(g[i])
		}
		fmt.Println()
		return
	}

	for i := 0; i < n; i++ {
		if !col[i] && !dg[i+u] && !udg[n-u+i] {
			g[u][i] = "Q"
			col[i] = true
			dg[i] = true
			udg[i] = true

			dfs(u + 1)

			g[u][i] = "."
			col[i] = false
			dg[i] = false
			udg[i] = false
		}
	}
}

func main() {
	for i := 0; i < n; i++ {
		for j := 0; j < n; j++ {
			g[i][j] = "."
		}
	}

	dfs(0)
}
```