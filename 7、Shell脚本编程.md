# 7、shell 脚本编程

## 7-1 来玩 shell 吧 ^_^

### 什么是 shell

- 有点像嵌入在 Linux 这样的操作系统中的一个“微型编程语言”；shell 不像 c 语言、c++、java 等语言那么完整，但是它可以帮我们完成很多自动化任务，例如：保存数据，监测系统的负载，等等；shell 相比 c 等语言的优势在于它是完全嵌入在 Linux 中的，不需要安装，不需要编译。

### shell 脚本

- 脚本（script）是批处理文件的延伸，是一种纯文本保存的程序
- 计算机脚本程序是确定的一系列控制计算机进行运算操作动作的组合，在其中可以实现一定的逻辑分支等

### 关于不同的环境

- Linux 的图形界面环境有很多：GNOME，KDE，XFCE 等
- 中断命令环境其实也有很多（虽然看起来都是黑框框）：它对应的就是不同的 shell ，shell不同命令的功能可能也不一样

### 几种主流的 shell

- Sh：Bourne Shell，是目前所有 Shell 的祖先
- Bash：Bourne Again Shell，是 Sh 的一个进阶版本，是目前大多数 Linux 发行版和 macOS 操作系统的默认 shell
- Ksh：Korn Shell，在收费的 Unix 版本上比较多见
- Csh：C Shell，此 Shell 语法有点类似 C 语言
- Tsh：Tenex C Shell，Csh 的优化版本
- Zsh：Z Shell，比较新的一个 Shell，集 Bash，Ksh 和 Tcsh 各家之大成

![](./media/87.png)

### shell 可以干啥捏？

- shell 是管理命令行的程序；其实是 shell 这个程序在等待你输入那些命令
- 记住你在终端输入过的命令（向上键）
- 控制进程
- 重定向命令（用到 <，>，|，等符号）

![](./media/88.png)

### 以 rc 结尾的文件

- .bashrc，.zshrc，.init.rc，.vimrc，等等；
- 一般以 rc 结尾的多为配置文件，里面包含了软件运行前会去读取并运行的那些初始化命令

### 安装 shell

- 安装 zsh：**sudo yum install zsh**

### 切换 shell

- **chsh**（Change Shell）：切换 shell

### 为什么切换 shell 很重要？

- shell 脚本需要依赖于某一个 shell，在使用不同的 shell（Sh，Bash，Zsh，Ksh，等等）的时候，语法其实是不一样的。下面来学 Bash 上的 shell 脚本编写。

## 7-2 第一个 shell 脚本

### 创建脚本文件

- **vim test.sh**
- 实际上 shell 和普通的文本文件没啥区别，只是后缀名 .sh 已经称为一种约定俗称的命名管理

### 指定脚本要使用的 shell

- 在写一个 shell 脚本的时候，第一要做的事情就是指定要使用哪种 shell 来 “解析/运行” 它，因为不同的 shell 语法不一样。

```shell
#!/bin/bash
```

- #！被称为 Sha-bang（或者 Shebang）；当第一行都头两个字母出现 #! 的时候，类 unix 操作系统的载入器会分析 #! 后面的内容，将这些内容作为解释器指令并调用该指令，并将载有 #! 的文档路径作为该解释器的参数。比如上面的那行，它并不是必不可少的，但是它确保会用 /bin/bash 来解析后面要写的命令（也就是说被指定的 shell 执行）。

### 运行命令

- 原则很简单：只需要写入你想要执行的命令就行了。

### 注释

- 注释是不会被执行的行，但是可以用于解释我们的脚本做了什么，Shell 脚本的注释以 #（井号）开头

```shell
#!/bin/bash

# 列出目录的文件
ls
```

### 给脚本文件添加可执行的权限

- 加上可执行权限：**chmod +x test.sh**

### 运行脚本

- 运行脚本文件：**./test.sh**

### 以调试模式运行

- 调试一个脚本程序：bash -x test.sh