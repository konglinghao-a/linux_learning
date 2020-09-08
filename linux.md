# 1、Linux的安装与配置

## 1-1 初识 Linux

### 电脑启动的顺序：

- 第一步：启动界面（主板）
- 第二步：操作系统（例如 Windows）的启动
- 第三步：其他程序（或称软件）的启动

### 能否在一台电脑上有两个（甚至更多）的 OS？

- 一台电脑可以拥有多个 OS
- 当启动界面结束以后，会有一个被成为 `bootloader` 的程序显示出来
- `bootloader`让你做出选择，到底选择哪个操作系统来启动

### 什么是 bootloader?

- boot（表示 “启动”），loader（表示 “加载器”）
- 通过这段小程序，初始化硬件设备、建立内存空间的映射图
- 为最终调用操作系统内核准备好正确的环境
- 通常 `bootloader`是严重依赖于硬件而实现的，特别在嵌入式领域
- 一般在 Linux 和 Windows 之间做出选择的 `bootloader` 叫 GRUB
- 如果没有做出选择，GRUB 在几秒之后就会启动默认的操作系统

### 不同操作系统上的程序

- Windows 的程序在 Linux 下不能运行，反之亦然
- 有些技术使 Windows 的程序在 Linux 下可以运行，例如 Wine
- 但终归是使用转为 Linux 定制的程序比较好

### Linux 上的程序有很多优点

- 免费：基本上 Linux 上的所有程序都是免费的
- 更新频繁，更新也是免费的
- 不少程序的 Linux 版更优秀，有些程序没有 Windows 版

## 1-2 linux 的不同发行版

### GNU 项目

- GNU 在英语里是 “牛羚” 的意思
- GNU 是 “GNU is Not Unix” 的递归缩写
- 1984年，理查德·斯托曼 创立了 GNU 项目
- GNU 项目在当时的首要目的是创立一个类 Unix 的操作系统
- Unix 需要复刻，因为它不是免费的

### Linus Torvalds（李纳斯·特沃兹）

- 1991年他在业余时间百年写了一个类 Unix 的内核
- Linux 这个名字可以说是 Linus 和 Unix 的合并
- Linux 也可以说是 “Linux Is Not Unix” 的递归缩写

### Linux 和 GNU 项目的联系

- 这两个项目是互补的：Linus 其实就是写了一个类 Unix 的内核
- 1991年，GNU 项目已经创建了不少操作系统的外围软件了
- GNU 的软件：cp 命令，rm 命令，Emacs，GCC，GDB等
- 后来完善 Linux 的工作交给了 Linus 和广大开源社区的黑客们
- GNU 项目 + Linux（系统内核）= **GNU/Linux** 完整的操作系统

### 总结

- 操作系统的核心称为 “内核”，但内核并不就等于操作系统
- 内核提供系统服务，比如文件管理、虚拟内存、设备 I/O 等
- 还包含一些基本的程序，例如 文本编辑器，编译器，外壳程序 shell
- 单独的 Linux 内核没办法工作，需要有 GNU 项目的众多应用程序
- Linux 的官方称谓应该是 “**GNU/Linux**”，一般简称 **Linux**
- [内核官网](https://www.kernel.org/)

### Linux 发行版

- 因为是开源自由的，Linux 不像 Windows 这么死板，可以自己定制自己的 Linux 系统
- Linux 发行版：因为太自由了这让初学者犯难，究竟该选择哪个版本，安装哪些软件？这个时候就有了发行版，这为了简化用户安装的过程，以及提供一些基本的软件
- 这种 “发行版” 的概念在 Windows 可以说没有

### Linux 发行版之间的主要区别

- 其实内核都是一样的，就是装饰不一样，是 Linux 的变体
- 安装方法不一样：有的复杂，有的简单
- 安装应用程序的方式不一样
- 预装的程序不一样

### 不同的 Linux 发行版

- Red Hat：性能稳定，老牌的 Linux 发行版。收费的是 RHEL。
- Fedora：Red Hat 的社区免费后继版。
- CentOS：算是 RHEL 的克隆版，免费。
- Deepin：**中国**发行。对优秀的开源产品进行集成和配置，开发软件。
- Debian：算是迄今为止，最遵循 GNU 规范的 Linux 系统。
- Ubuntu：Debian 的后继或一个分支。

### Red Hat 家族主要成员

- RHEL：Red Hat 企业版
- Fedora：Red Hat 的社区免费后继版
- CentOS：RHEL 的克隆版，免费。结合了 RHEL 和 Fedora 的特性

## 1-3 Linux 的多面性、定制自由

### 第一面：免费

- windows收费，而 Linux 免费

### Linux 的两种界面

- 不论是哪一个 Linux 发行版，都有两种使用 Linux 的方式。
- 1、命令行界面（类似 DOS 操作系统）
- 2、图形界面（类似 Windows 操作系统）
  - Linux 有多种图形界面。它们都基于一个程序：**X**
  - X 程序是 Linux 图形界面的基石
  - 在 X 程序之上，插入了另一个程序，叫做 “桌面管理器”，其作用是管理窗口，以及它们的外观，选项等等（在 Windows 下并没有 “桌面管理器” 这个概念）
  - 主流的桌面管理器
    - Gnome
    - KDE
    - XFDE

## 1-4 CentOS 下载

- [下载网址](https://www.centos.org/download/)

## 1-5 虚拟机安装 CentOS

### 虚拟技术/虚拟化（Virtualization）

- 一种通过组合或分区现有的计算机资源（CPU、内存、磁盘空间等），使得这些资源表现为一个或多个操作环境，从而提供优于原有资源配置的访问方式的技术。

### 安装 VirtualBox

- VirtualBox 是一款开源虚拟机软件，免费
- **在 Windows 下面下载需要进入 BIOS 开启虚拟化**（我的好像不用）

**VirtualBox对比 VMWare**

- VMWare 的各种版本，安装文件很大；VirtualBox 占用资源少
- VMWare 收费

### 创建虚拟机

![](./media/1.png)

![](./media/2.png)

![](./media/3.png)

![](./media/4.png)

![](./media/5.png)

![](./media/6.png)

### 在虚拟机中安装 centos 系统

![](./media/7-1.png)

![](./media/7-2.png)

![](./media/7.png)

![](./media/8.png)

![](./media/9.png)

![](./media/10.png)

![](./media/11.png)

![](./media/12.png)

![](./media/13.png)

![](./media/14.png)

![](./media/15.png)

![](./media/16.png)

![](./media/17.png)

![](./media/18.png)

![](./media/19.png)

![](./media/20.png)

![](./media/21.png)

![](./media/22.png)

![](./media/23.png)

![](./media/24.png)

![](./media/25.png)

![](./media/26.png)

![](./media/27.png)

![](./media/28.png)

![](./media/29.png)

![](./media/30.png)

![](./media/31.png)

![](./media/32.png)

![](./media/33.png)

![](./media/34.png)

## 1-6 配置虚拟机中的 CentOS

![](./media/35.png)

![](./media/36.png)

![](./media/37.png)

![](./media/38.png)

![](./media/39.png)

### 安装增强功能

![](./media/40.png)

若出现了错误：

> VirtualBox安装增强功能时报错：未能加载虚拟光盘 到虚拟电脑

那就进入命令行，然后输入 eject 命令来弹出光盘，然后再执行安装增强功能（重启以后才有用）。

![](./media/41.png)

![](./media/42.png)

# 2、Linux基础知识和命令

## 2-1 关于终端界面

问题：

- 为什么要发明终端，而不是一开始就用图形界面？
  - 因为计算机一开始的时候计算能力不强。
- 为什么需要终端？
  - 为了节省时间

```
例子：一个目录里有多个文件，你想知道有多少个 JPEG 类型的图片。在图形界面里可能会有点麻烦；
在终端里一句命令搞定：ls -l | grep jpg | wc -l
```

### 什么是 tty？

- 在 Linux 中， TTY 也许是跟终端有关系的最为混乱的术语
- TTY 是 TeleTYpe 的一个缩写
- Teletypes，或者 teletypewriters ，原来指的是电传打字机
- 我的理解，tty就是个真正的全屏幕终端

### 登录 tty 的快捷键

- ctrl + alt + f1：**回到图形界面**
- ctrl + alt + f2：terminal 1 (:0  大致等于 tty1)
- ctrl + alt + f3：terminal 2（tty2）
- ctrl + alt + f4：terminal 3（tty3）
- ctrl + alt + f5：terminal 4（tty4）
- ctrl + alt + f6：terminal 5（tty5）

## 2-2 命令行

- 命令行：Command Line。

### 命令行提示符

- **[konglinghao@localhost ~]$** 是命令提示符， 可以看成电脑在对你打招呼，说 “你好”，提示你要开始写东西了。
- konglinghao 是当前用户的名字。Linux 是多用户的操作系统（windows 也是）。
- @ 后面的是所在的域。localhost 是主机的名字。
- ~ 是当前所在目录的名字，会随着用户进入不同目录而改变
- ~ 表示当前用户的家目录（home directory）
- $ 指示你所具有的权限
  - $表示普通用户，拥有有限的权限
  - #表示超级用户，拥有所有权限

### 简单的命令

- date 用于显示当前时间
- ls 是 list 的缩写，用于列出当前目录下的文件和目录

### 命令的参数

- 参数是写在命令之后的一些补充选项。命令和参数之间要有空格隔开。
- 格式：command parameters
- 参数里可以包含多个参数，由空格隔开
- 参数也可以包含数字，字母，等等
- 参数没有固定的格式，但是一般来说还是遵循一定的规范

### 短参数（一个字母）

- 最常用的参数形式就是一个短横线后接一个字母：command -p
- 一次可以加好几个短参数，可以用空格隔开：command -p -a -T -c
- 多个短参数可以合并到一起：command -paTc
- 字母的大小写有区别，大写的 T 和小写的 t 通常含义不同
- 举一个实际的例子：ls -a；参数中的 a 是 all 的意思（包含隐藏文件，linux 里面以 . 开头的就是隐藏文件）

### 长参数（多个字母）

- 长参数没有短参数那么常用，但也是很有用的，以两个短横线开始
- 格式：command --parameter
- 多个长参数不能合并写，要用空格隔开：command --parameter1 --parameter2
- 可以组合使用短参数和长参数：command -paTc --parameter1
- 有时候同一个意义的参数有长参数和短参数两种形式：ls -a 和 ls --all 意思一样

### 参数赋值

- 有一些参数需要赋值。短参数和长参数赋值方式不一样
- 短参数赋值：command -p 19
- 长参数赋值：command --parameter=10

## 2-3 如何查找命令和命令的历史记录

### 如何找到一个命令

- 有时候想不起来一个命令到底是如何拼写的
- 用 Tab 键来补全命令
- Tab 键还可以不全文件名、路径名：按**两次** tab 键

### 命令的历史记录

- 向上键：按时间顺序向前查找用过的命令
- 向下键：按时间顺序向后查找用过的命令
- **ctrl + r**：用于查找使用过的命令

### history 命令

- history 是英语 “历史，历史记录” 的意思
- 用于列出之前用过的所有命令
- 可以用 **!编号** 这样的格式来重新运行 history 输出中对应编号的命令

### 一些实用的快捷键

- Ctrl + L 用于清理终端的内容，就是清屏的作用。同 clear 命令。
- Ctrl + D 给终端传递 EOF（End Of Life ，文件结束符）。
- Shift + PgUp 用于向上滚屏，与鼠标的滚轮向上滚屏是一个效果。
- Shift + PgDn 用于向下滚屏，与鼠标的滚轮向下滚屏是一个效果。
- Ctrl + U 用于删除光标左侧的内容。
- Ctrl + K 用于删除光标右侧的内容。

## 2-4 文件和目录组织命令

### 文件的组织

- 不像 windows 里面那样有 C盘，E盘这些，Linux 把所有东西都放到一个地方。
- Linux 把文件分为普通文件和特殊文件

### 普通文件

- 文本类型的文件（.txt，.doc，.odt 等）。
- 声音文件（.mp3 等），还有程序。
- 这样的文件在 windows 里也有。

### 特殊文件

- 其他一些文件是特殊的，因为它们表示一些东西
- 例如，光盘驱动器就是这类特殊的文件

**Linux 中一切皆是文件，连目录也是文件。**

### 根目录

Windows 中的根目录：

- windows 中，可以有好几个根目录
- C盘（C:/）是硬盘的根目录（加入没有把 C盘 磁盘分区的话）
- H盘可能是光盘驱动器的根目录

Linux 的根目录：

- Linux 有且只有一个根目录，就是 / （斜杠）
- Linux 中没有比根目录再高一阶的目录，没有目录包含根目录
- 根目录就是 Linux 最顶层的目录：“万有之源，斜杠青年”

### 目录结构

Windows 目录结构：

- Windows 下，一个目录的形式是这样的 C:\Program Files\Baidu
- Baidu 这个目录是 Program Files 这个目录的一个子目录
- Program Files 是 C盘 这个根目录的一个子目录
- Windows 中用反斜杠 \ 来标明目录的层级与包含关系

Linux 目录结构：

- Linux 中用斜杠 / 来标明目录的层级与包含关系（只有斜杠 / 这个根目录）
- Linux 的目录形式是这样的：/usr/bin
- bin 是 usr 目录的子目录，usr 是 / 这个根目录的子目录

## 2-5 Linux 的根目录的直属子目录

### bin

- binary，表示 “二进制文件”
- （我们知道可执行文件是二进制的）
- bin 目录包含了会被所有用户使用的可执行程序

### boot

- 启动；包含与 Linux 启动密切相关的文件

### dev

- device (设备)；包含外设。它里面的子目录，每一个对应一个外设。
- 比如代表我们的光盘驱动器的文件就会出现在这个目录下面

### etc

- etc：有点不能顾名思义了。etc 是法语 et cetera 的缩写
- 翻译成英语就是 and so on ，表示 "...等等"
- etc 目录包含系统的配置文件
- 至于为什么在 /etc 下面存放配置文件，按照原始的 Unix 的说法，这下面放的都是一堆零零碎碎的东西，就叫 etc 好了，是 **历史遗留**

### home

- 家；用户的私人目录
- 在 home 目录中，我们放置私人的文件，类似 windows 中的 Documents 文件夹，也叫 "我的文档"
- Linux 中的每个用户都在 home 目录下有一个私人目录（除了大管家用户 root ），root 用户拥有所有权限，比较 “任性”，跟普通用户不住在一起。
- 我的用户名是 konglinghao ，那么我的私人目录就是 /home/konglinghao

### lib

- library（库）；包含被程序所调用的库文件，例如 .so 结尾的文件
- 在 windows 下这样的库文件则是以 .dll 结尾

### media

- media（媒体）；可移动的外设（USB盘，SD卡，DVD，光盘 等等）插入电脑时，可以通过 media 的子目录来访问这些外设中的内容

### mnt

- mount（挂载）；有点类似于 media 目录，但一般用于临时挂载一些装置

### opt

- optional application software package（可选的应用软件包）；用于安装多数第三方软件和插件

### root

- 根；超级用户 root 的家目录；一般的用户的家目录位于 /home 下，root 用户是个例外

### sbin

- system binary（系统二进制文件）；包含系统级的重要可执行程序

### srv

- service（服务）；包含一些网络服务启动之后所需要取用的数据

### tmp

- temporary（临时的）；普通用户和程序存放临时文件的地方

### usr

- Unix Software Resource （Unix 操作系统软件资源）；类似 etc，也是 **历史遗留** 的命名；
- 是最庞大的文件之一
- 类似 windows 中的 C:\Windows 和 C:\Program Files 这两个文件夹的集合
- usr 目录里安装了大部分用户要调用的程序

### var

- variable（动态的，可变的）；通常包含程序的数据，比如 log（日志）文件

## 2-6 pwd 命令和 which 命令

### pwd 命令

- 显示当前目录的路径
- 刚打开一个终端，你将位于你的用户家目录 ~ 中
- 如果用户是 konglinghao ，那么 ~ 这个目录就是 /home/konglinghao 这个目录
- 通常来说，命令行提示符会告诉你目前位于那个目录下（还有个方法，那就是 **pwd 命令**）
- pwd（Print Working Directory）；打印当前工作目录

### which 命令

- 获取命令的可执行文件的位置
- 不是一个必不可少的命令，平时用到它的机会也不多
- Linux 下，**每一条命令其实对应了一个可执行程序**；
- 在终端中输入命令，按回车的时候，就是执行了对应的那个程序；
- 一个命令，其实只不过是我们随时可以调用的程序罢了
- which 命令接收一个参数，是你想知道其可执行程序位于哪里的命令
- windows 可执行程序以 .exe 结尾，Linux 中一般是没有后缀名的

# 3、Linux进阶知识和命令



# 4、远程连接和SSH



# 5、文本编辑与版本控制



# 6、网络和安全



# 7、Shell脚本编程



# 8、管理服务器和服务



# 9、Linux开发神器



# 10、内存与磁盘管理



