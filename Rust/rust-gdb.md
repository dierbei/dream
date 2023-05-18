## 命令
```text
# 进入调试
rust-gdb target/debug/hello_world

# main 函数打断点
b main:11

# 文件打断点
b src/main.rs:11

# 下一行
n

# 执行上一条命令（回车）
enter

# 运行到断点处，但并未执行
c

# 查看断点
info b

# 删除断点
d 1

# 批量删除断点
d 1 2

# 终止程序调试
k

# 显示源代码
layout src
```

## 详细信息
```text
run: 启动程序
break: 在指定行或函数处设置断点
continue: 继续执行程序直到下一个断点
step: 执行当前行，并进入函数调用
next: 执行当前行，并跳过函数调用
print: 打印变量的值
backtrace: 打印函数调用栈
quit: 退出 GDB
```