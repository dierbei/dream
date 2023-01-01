## 代码
```go
package main

import "log"

const N = 4
const M = 5

var v [4 + 1]int
var w [4 + 1]int
var q [N + 1][M + 1]int

func main() {
	//4 5
	//1 2
	//2 4
	//3 4
	//4 5
	v = [4 + 1]int{1, 2, 3, 4}
	w = [4 + 1]int{2, 4, 4, 5}

	for i := 1; i <= N; i++ {
		for j := 0; j <= M; j++ {
			q[i][j] = q[i-1][j]
			if j >= v[i] {
				q[i][j] = max(q[i][j], q[i-1][j-v[i]]+w[i])
			}
		}
	}

	log.Println(q[N][M])
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

```