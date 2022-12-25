## 1. 代码
```go
package main

import "fmt"

const N = 5

var g [N][N]int
var d [N][N]int

type Position struct {
	First  int
	Second int
}

func bfs() int {
	dx := [4]int{-1, 0, 1, 0}
	dy := [4]int{0, 1, 0, -1}

	q := make([]Position, 0)
	q = append(q, Position{
		First:  0,
		Second: 0,
	})

	for len(q) > 0 {
		t := q[0]
		q = q[1:]

		for i := 0; i < 4; i++ {
			x := t.First + dx[i]
			y := t.Second + dy[i]

			if x >= 0 && x < N && y >= 0 && y < N && g[x][y] == 0 && d[x][y] == -1 {
				d[x][y] = d[t.First][t.Second] + 1
				q = append(q, Position{
					First:  x,
					Second: y,
				})
			}

		}
	}

	return d[N-1][N-1]
}

func main() {
	//5 5
	//0 1 0 0 0
	//0 1 0 1 0
	//0 0 0 0 0
	//0 1 1 1 0
	//0 0 0 1 0
	g = [N][N]int{
		{0, 1, 0, 0, 0},
		{0, 1, 0, 1, 0},
		{0, 0, 0, 0, 0},
		{0, 1, 1, 1, 0},
		{0, 0, 0, 1, 0},
	}

	for i := 0; i < N; i++ {
		for j := 0; j < N; j++ {
			d[i][j] = -1
		}
	}
	d[0][0] = 0

	fmt.Println(bfs())
}
```