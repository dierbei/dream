## 1. 代码
```go
package main

import "log"

func main() {
	for i := 100000; ; i++ {
		flag := true

		for j := 2; j*j <= i; j++ {
			if i%j == 0 {
				flag = false
				break
			}
		}

		if flag {
			log.Println(i)
			break
		}
	}
}
```