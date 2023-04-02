## 基本
```text
Mount: 隔离文件系统挂载点

UTS: 隔离主机名和域名信息

IPC: 隔离进程间通信

PID: 隔离进程的ID

Network: 隔离网络资源

User: 隔离用户和用户组的ID
```

## 命令
```text
# 隔离主机名
unshare --fork --uts /bin/bash

# 隔离文件挂载 + 主机名
unshare --fork --uts --mount /bin/bash

# 查看 ID 号
ls -l /proc/self/ns
```