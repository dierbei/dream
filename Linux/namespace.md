## 常用命令
```shell
# 列出网络命名空间
ip netns list

# 添加网络命名空间
ap netns add <namespace-name>

# 删除指定命名空间
ip netns delete <namespace-name>

# 在指定命名空间执行命令
ip netns exec <namespace-name> <commands>

# 启动网卡
ip netns exec <namespace-name> ip link set <card-name> up
```

## go 示例代码
```go
package cmds

import (
	"github.com/spf13/cobra"
	"log"
	"os"
	"os/exec"
	"syscall"
)

//在 Linux中 代表当前执行的程序（go run main.go == main.go）
const self = "/proc/self/exe"

//写死的
const alpine = "/root/alpine"

var runCommand = &cobra.Command{
	Use: "run",
	Run: func(cmd *cobra.Command, args []string) {
		runCmd := exec.Command(self,"exec","/bin/sh")
		runCmd.SysProcAttr = &syscall.SysProcAttr{
			Cloneflags: syscall.CLONE_NEWUTS,
		}
		runCmd.Stdin = os.Stdin
		runCmd.Stdout = os.Stdout
		runCmd.Stderr = os.Stderr
		if err := runCmd.Start(); err != nil {
			log.Fatalln(err)
		}
		runCmd.Wait()
	},
}

```