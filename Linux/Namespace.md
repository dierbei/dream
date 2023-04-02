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