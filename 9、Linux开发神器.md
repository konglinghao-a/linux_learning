# 9、Linux 开发神器

## 9-1 java web 应用的世界 Servlet，Tomcat 和 Jenkins

### Jenkins

- 用 Java 语言开发的一种持续集成（CI）工具
- CI 是 Continuous Integration 的缩写，表示 “持续集成”
- 能够让软件的测试、编译和部署自动化
- 通常与版本管理工具（SCM）、构建工具结合使用
- 常用的版本管理工具有 SVN、GIT
- 常用的构建工具有 Ant、Maven、Gradle
- Jenkins 是以 Servlet 形式提供的
- 它采用扩展名为 .war 的二进制文件的形式
- war 是 Web Archive 的缩写，表示 "网络归档文件"

### Servlet

- Java 中旨在动态生成 HTML 代码的应用程序通常采用 Servlet 的形式
- Servlet 是尊重 Java Servlet API 的 Java Web 应用程序
- Servlet = Service + Applet，表示 “小程序服务”

### 创建 Servlet

- 要么编写纯 Java 代码并编译
- 要么写一个 JSP（Java Server Pages）

### JSP

- JSP 实际上是一个 HTML 页面，其中添加了对 Java 代码的调用

- JSP 编译器会编译 JSP，将其转换为 Servlet

### Servlet 容器

- 要能够在服务器上运行 Servlet 并将 HTTP 请求传递给它们，需要一个 Servlet 容器
- Tomcat 是 Apache 软件基金会发布的 Servlet 容器

### Tomcat

- Tomcat 由几个组件构成：Catalina、Coyote、Jasper

  **Tomcat 组件 Catalina**

- Catalina 本身是 Servlet 的容器，并负责其执行

**Tomcat 组件 Coyote**

- Coyote 是一个 HTTP 链接器，因此是一个微型 Web 服务器，它将 HTTP 请求传输到 Catalina

**Tomcat 组件 Jasper**

- Jasper 是 Tomcat 的 JSP 编译器

### Jenkins 的运行

- 为了使用 Jenkins 应用程序，需要安装 Tomcat 服务器
- Jenkins 也可以独立运行，因为它自身页包含了名为 “Winstone” 的 Servlet 微型容器

## 9-2 配置 java 环境并安装 Tomcat

- 安装 tomcat：**yum install tomcat**
- 上面这条语句会直接去安装 java 的**运行时环境（JRE）**，但是不会安装 JDK
- 如果你想安装开发环境：**yum install java-1.8.0-openjdk-devel.x86_64**
- 开启 tomcat：**systemctl start tomcat**
- 开机自动启动：**systemctl enable tomcat**
- tomcat 的默认端口是 8080

现在在浏览器里面输入：192.168.1.101:8080，这时候会发现它什么都没有显示，那是因为还要安装下面的东西：

- **yum install tomcat-webapps tomcat-admin-webapps**
- 安装参考的文档：**yum install tomcat-docs-webapp tomcat-javadoc**
- 然后重启 tomcat：**systemctl restart tomcat**

这个时候还是访问不了，因为防火墙挡住了，现在要让防火墙放行:

- **firewall-cmd --zone=public --add-port=8080/tcp --permanent**
- **firewall-cmd --reload**

这个时候 192.168.1.101:8080 就能访问了；但是发现他的很多东西是需要登录的，下面就要创建一个用户：

```shell
vim /etc/tomcat/tomcat-user.xml
```

`vim /etc/tomcat/tomcat-user.xml`

```shell
# 可以在下面的区域里面添加用户
<tomcat-users>
	# 可以放开下面的注释
	<user name="admin" password="adminadmin" roles="admin,manager,admin-gui,admin-script,manager-gui,manager-script,manager-jmx,manager-status" />
</tomcat-users>
```

