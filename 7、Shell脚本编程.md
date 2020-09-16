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
- -x 参数：表示以调试模式运行
- 以调试模式运行的时候 shell 就会把我们的脚本文件运行时的细节打印出来了

### 创建属于自己的命令

我们只能 ./test.sh 的形式运行 shell 脚本，而且还得在正确的目录，这太麻烦了；我们之前的命令例如：ls，cp 等，它们是存在 **PATH 环境变量**里面的。

### PATH 环境变量

- PATH 是 Linux 的一个系统环境变量，这个变量包含了你系统里所有可以被直接执行的程序的路径。
- 打印输出 PATH 变量的值：echo $PATH；每个路径之间用冒号来分割；因此只用把 `test.sh` 文件拷贝到上述文件的任意一个目录当中，这样就能够随便在哪里运行 `test.sh` 这个脚本了，前面就不需要加上 `./ `了

```
/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin:/home/konglinghao/.local/bin:/home/konglinghao/bin
```

- 我们将目录拷贝到 `/usr/bin` 目录中：**sudo cp test.sh /usr/bin**

## 7-3 shell 的变量

### 定义变量

- message='hello world'**（要注意等号的两边不要加空格！）**
- message：变量名
- 'hello world'：变量值

### echo：显示内容

-  作用是在终端上显示传入的信息
- **echo hello world**：在终端里打印出 hello world
- 如果要插入换行符（\n），那么需要用到 **-e 参数**，这是为了使 "转义字符" 发生作用（不然即使有转义字符也木有用）
- 在 bash 脚本中，如果要显示一个变量，用 echo 后接变量名还不够，需要在变量名前加上美元符号（$）

```shell
#!/bin/bash

message='hello world'
echo $message
```

### 引号

- 可以用引号来界定包含空格的字符串

| 类型   | 表示 |
| ------ | ---- |
| 单引号 | '    |
| 双引号 | "    |
| 反引号 | `    |

单引号：

- 如果变量被包含在单引号里面，那么变量就不会被解析，美元符号（$）保持原样输出
- 单引号忽略被它括起来的所有特殊字符

双引号

- 双引号会忽略大多数特殊字符，但不包括：美元符号（$）、反引号（`）、反斜杠（\）
- 不忽略美元符号意味着 shell 在双引号内部可以进行变量名替换

反引号

- 反引号要求 shell 执行被它括起来的内容

```shell
#!/bin/bash

message=`pwd`
echo "you are in the directory $message"

# 最后执行这个 shell 脚本，会显示出：you are in the directory /home/konglinghao
```

### read：请求输入

- read 命令读取到的文本会立刻被存储在一个变量里

```shell
#!/bin/bash

read name
echo "hello $name"

# 最后运行这个脚本的时候会让你输入，然后按回车，这样你输入的值就会赋值给 name
```

**同时给多个变量赋值**

```shell
#!/bin/bash

read firstname lastname
echo "hello $firstname $lastname"

# 最后运行的时候输入：linghao kong ；输出就是 hello linghao kong
```

- 可以用 read 命令一次性给多个变量赋值，read 命令一个单词一个单词（用空格隔开）地读取你输入地参数，并且把每个参数赋值给对应变量

**-p：显示提示信息**

- read 命令地 -p 参数，p 是 prompt（提示） 的首字母

```shell
#!/bin/bash

read -p 'Please enter your name：' name
echo "hello $name"

# 这个时候让你打印前会有一行提示信息"Please enter your name："来提示你打印
```

**-n：限制字符数目**

- 用 -n 参数可以限制用户输入的字符串的最大长度（字符数）

```shell
#!/bin/bash

read -p 'Please enter your name：' -n 5 name
echo "hello $name"

# 这个时候长度就会被限制为 5 
```

**-t：限制输入时间**

- 限定用户输入的时间（以秒为单位），超过这个时间，就不读取输入了

**-s（secret）：隐藏输入内容**

- 用 -s 参数可以隐藏输入内容，如果你想用户输入的是一个密码，可以用一波

### 数学运算

**牢记！在 bash 中，所有的变量都是字符串！**

**let 命令**

- bash 本身不会操纵数字，因此它也不会做运算；但是可以用 **let 命令**来达到这个目的

```shell
#!/bin/bash

let "a = 5"
let "b = 2"
let "c = a + b"

echo "c = $c" # 此时 c 打印出来的就是 7
```

**bs 命令**

- 如果要做带小数的运算，那么需要用到 bc 的命令

### 环境变量

- shell 的环境变量可以被此种 shell 的任意脚本程序使用，有时也把环境变量称为“全局变量”
- 可以用 **env 命令**来显示你所有的环境变量
- **SHELL**：指明目前你使用的是哪种 shell
- **PATH**：是一系列路径的集合，只要有可执行程序位于任意一个存在于 PATH 中的路径，那就可以直接输入可执行程序的名字来执行

```shell
#!/bin/bash

# 使用全局变量
echo "Your default shell is $SHELL, and your path is $PATH"
```

设置环境变量

- 可以用 **export** 关键字来设置环境变量

### 参数变量

- 可以这样调用我们的脚本文件：./variable.sh 参数1 参数2 参数3 ...
- 上面的 参数1， 参数2， 参数3 等等就被称为“参数变量”

| 变量 | 含义               |
| ---- | ------------------ |
| $#   | 参数的数目         |
| $0   | 被运行的脚本的名称 |
| $1   | 第 1 个参数        |
| $2   | 第 2 个参数        |
| $N   | 第 N 个参数        |

```shell
#!/bin/bash

echo "You have executed $0，there are $# parameters"
echo "The first parameter is $1"

# 在运行的时候：./variable.sh parameter1 parameter2 parameter3
# 输出：You have excuted ./variable.sh, there are 3 parameters
# 	   The first parameter is parameter1
```

- 可以用 shift 命令来"挪移"参数，以便依次处理，此命令常被用在**循环中**

```shell
#!/bin/bash

echo "The first parameter is $1"
shift
echo "The first parameter is now $1"

# 在运行的时候：./variable.sh parameter1 parameter2 parameter3
# 输出：The first parameter is parameter1
# 	   The first parameter is now parameter2
```

### 数组

```shell
#!/bin/bash

array=('value1' 'value2' 'value3' 'value3' )
array[5]='value5'
echo ${array[1]} # 这是数组的用法
echo ${array[*]} # 打印出数组中所有的数
```

- 数组可以包含任意大小的元素数目
- 数组的元素编号不需要是连续的

## 7-4 shell 的条件

### if 

```shell
# 基本格式：
if [ 条件测试 ] # 注意，条件测试的两边都必须要空一格
then
	做这个
fi # 表示 if 语句结束
```

- 在 shell 语言中，“等于” 是用一个等号（=）来表示的（其实用两个等号也 ok 的 ^_^）

```shell
#!/bin/bash

name="konglinghao"

if [ $name = "konglinghao" ]
then
	echo "hello $name"
fi
```

- 条件不成立用 else

```shell
# 基本格式：
if [ 条件测试 ]
then
	做这个
else 
	做那个
fi
```

```shell
#!/bin/bash

name1="kong"
name2="linghao"

if [ $name1 = $name2 ]
then 
	echo "You two have the same name!"
else
	echo "You two have different names!"
fi
```

- elif：否则如果

```shell
# 基本格式
if [ 条件测试1 ]
then
	做事情1
elif [ 条件测试2 ]
then
	做事情2
elif [ 条件测试3 ]
then
	做事情3
else
	做其他事情
fi
```

### 条件测试

- 测试类型：
  - 测试字符串
  - 测试数字
  - 测试文件

**测试字符串**

| 条件                 | 意义                                                       |
| -------------------- | ---------------------------------------------------------- |
| $string1 = $string2  | 两个字符是否相等。shell 大小写敏感，因此 A 和 a 是不一样的 |
| $string1 != $string2 | 两个字符串是否不同                                         |
| -z $string           | 字符串 string 是否为空（zero）                             |
| -n $string           | 字符串 string 是否为不空（not）                            |

**测试数字**

| 条件            | 意义                          |
| --------------- | ----------------------------- |
| $num1 -eq $num2 | 两个数字是否相等              |
| $num1 -ne $num2 | 两个数字是否不同              |
| $num1 -lt $num2 | 数字 num1 是否小于 num2       |
| $num1 -le $num2 | 数字 num1 是否小于或等于 num2 |
| $num1 -gt $num2 | 数字 num1 是否大于 num2       |
| $num1 -ge $num2 | 数字 num1 是否大于或等于 num2 |

**测试文件**

| 条件     | 意义 |
| -------- | ---- |
| -e $file |      |
|          |      |
|          |      |
|          |      |
|          |      |
|          |      |
|          |      |
|          |      |
|          |      |

