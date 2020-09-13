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

![](D:/1mynotes/linux/media/1.png)

![](D:/1mynotes/linux/media/2.png)

![](D:/1mynotes/linux/media/3.png)

![](D:/1mynotes/linux/media/4.png)

![](D:/1mynotes/linux/media/5.png)

![](D:/1mynotes/linux/media/6.png)

### 在虚拟机中安装 centos 系统

![](D:/1mynotes/linux/media/7-1.png)

![](D:/1mynotes/linux/media/7-2.png)

![](D:/1mynotes/linux/media/7.png)

![](D:/1mynotes/linux/media/8.png)

![](D:/1mynotes/linux/media/9.png)

![](D:/1mynotes/linux/media/10.png)

![](D:/1mynotes/linux/media/11.png)

![](D:/1mynotes/linux/media/12.png)

![](D:/1mynotes/linux/media/13.png)

![](D:/1mynotes/linux/media/14.png)

![](D:/1mynotes/linux/media/15.png)

![](D:/1mynotes/linux/media/16.png)

![](D:/1mynotes/linux/media/17.png)

![](D:/1mynotes/linux/media/18.png)

![](D:/1mynotes/linux/media/19.png)

![](D:/1mynotes/linux/media/20.png)

![](D:/1mynotes/linux/media/21.png)

![](D:/1mynotes/linux/media/22.png)

![](D:/1mynotes/linux/media/23.png)

![](D:/1mynotes/linux/media/24.png)

![](D:/1mynotes/linux/media/25.png)

![](D:/1mynotes/linux/media/26.png)

![](D:/1mynotes/linux/media/27.png)

![](D:/1mynotes/linux/media/28.png)

![](D:/1mynotes/linux/media/29.png)

![](D:/1mynotes/linux/media/30.png)

![](D:/1mynotes/linux/media/31.png)

![](D:/1mynotes/linux/media/32.png)

![](D:/1mynotes/linux/media/33.png)

![](D:/1mynotes/linux/media/34.png)

## 1-6 配置虚拟机中的 CentOS

![](D:/1mynotes/linux/media/35.png)

![](D:/1mynotes/linux/media/36.png)

![](D:/1mynotes/linux/media/37.png)

![](D:/1mynotes/linux/media/38.png)

![](D:/1mynotes/linux/media/39.png)

### 安装增强功能

![](D:/1mynotes/linux/media/40.png)

若出现了错误：

> VirtualBox安装增强功能时报错：未能加载虚拟光盘 到虚拟电脑

那就进入命令行，然后输入 eject 命令来弹出光盘，然后再执行安装增强功能（重启以后才有用）。

![](D:/1mynotes/linux/media/41.png)

![](./media/42.png)