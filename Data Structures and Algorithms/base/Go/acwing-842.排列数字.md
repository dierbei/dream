## 1. 代码
```go
package main

import (
	"fmt"
)

var path [4]int
var st [4]bool

var n = 3

func dfs(u int) {
	if u == n {
		for i := 0; i < n; i++ {
			fmt.Printf("%d ", path[i])
		}
		fmt.Println()
		return
	}

	for i := 1; i <= n; i++ {
		if !st[i] {
			path[u] = i
			st[i] = true
			dfs(u + 1)
			st[i] = false
		}
	}
}

func main() {
	dfs(0)
}
```