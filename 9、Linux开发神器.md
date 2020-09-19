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

## 9-3 安装 Jenkins 持续集成软件

- 下载 Jenkins 的 war 文件:  **wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war**
- 移动 war 文件：**mv jenkins.war /var/lib/tomcat/webapps**；要安装 jenkins 只需要将 jenkins.war 这个文件放到包含应用程序的目录，然后**重启 tomcat** 就会为我生成 jenkins 这个目录，这是自动部署的。
- 然而，在经过上一步了以后可能没有看见 jenkins 这个目录（ls /var/lib/tomcat/webapp），这是因为受到 SELinux 的捣蛋（从主机下载了 war 文件，然后用 scp 命令传送到服务器的 root 目录下，安全上下文可能发生了改变。如果直接传送到 /var/lib/tomcat/webapp 目录可能安全上下文不变，那么就没有这个问题），我们可以看一看当前目录的安全上下文：

```shell
pwd # /var/lib/tomcat/webapps
ls -Zd # 显示安全上下文
# drwxrwxr-x. root tomcat system_y:object_r:tomcat_var_lib_t:s0 .

# 看看 jenkins.war 这个文件的安全上下文
ls -Zd jenkins.war
# -rw-r--r--. root root unconfined_u:object_r:admin_home_t:s0 jenkins.war

# 修改 jenkins 文件的安全上下文
semanage fcontext -a -t tomcat_var_lib_t jenkins.war
restorecon -Rv . # 当前目录去重载一下配置

# 接下来它就会去自动部署，这样就生成了 jenkins 文件
```

- 接下来输入 192.168.1.101:8080/jenkins 就能看到一波显示
- 这时候可能看到页面上显示了 offline，这是因为证书的关系，我们改成 http 就行了

```shell
vim /var/lib/jenkins/hudson.model.UpdateCenter.xml
```

`/var/lib/jenkins/hudson.model.UpdateCenter.xml`

```shell
# 修改成 http
<url>http://updates.jenkins.io/update-center.json</url>
```



### jenkins 的运行

- 可以直接运行：**java -jar jenkins.war**
- 也可以修改端口运行：**java -jar jenkins.war --httpPort=8081**
- 或者在 Tomcat 这样的 Servlet 容器里运行

### Tomcat 的 Coyote Web 服务器的局限

- Coyote Web 服务器不能用于直接服务客户端连接
- 它在处理静态文件时效率较低
- 并且本身不支持 HTTPS 协议

解决方法：

- 使用功能更强大的 web 服务器（例如 apache 或 nginx）作为代理服务器，将请求转发到 Tomcat
- web 服务器将管理 https 连接、访问限制和静态页面，只有对 java 应用程序的请求会被转发到 Tomcat

### Web 服务器和 Tomcat 应用服务器之间的通信方式

- 使用 HTTP 协议，web 服务器将会做一个 HTTP 重定向到 Tomcat 服务器
- 使用某些插件，例如仅适用于 apache 的 mode_jk 插件，该插件使用特殊协议在 apache 和 tomcat 之间进行通信

## 9-4 安装 Nginx 服务器

### Nginx

- 高性能、轻量级、功能丰富、配置简单。用 C 语言写的
- Apache、Nginx、IIS 并成为 “服务器三巨头”
- 相比 apache ，Nginx 更适合高并发场景
- apache 阻塞型、同步多进程。Nginx 异步、非阻塞、事件驱动
- 安装：**yum install epel-release**  然后 **yum install nginx**
- 开机启动：systemctl enable nginx
- 启动：**nginx** 或 **systemctl start nginx**
- 启动的时候可能会出错，因为 nginx 和 apache 一样默认都是绑定了 80 端口，我们可以先把 apache 停掉然后再去启动 nginx 。

## 9-5 修改 apache 监听其他端口

```shell
# 首先让 apache 监听其他服务，不要默认监听 80 端口，进入 apache 的主配置文件
vim /etc/httpd/conf/httpd.conf
```

`/etc/httpd/conf/httpd.conf`

```shell
# 修改下面监听的端口
Listen 7080 http
```

```shell
# 然后让 apache 的 https 不要监听 443 端口
vim /etc/httpd/conf.d/ssl.conf
```

`/etc/httpd/conf.d/ssl.conf`

```shell
Listen 7443 https

<VirtualHost _default_:7443>
```

- 接下来重启 apach：**systemctl restart apache**
- 这时候可能会出错，因为 SELinux 不肯放行这些端口（7080 和 7443），防火墙也没放行这些端口

```shell
# 查看允许的端口：
semanage port -l | grep http

# 添加端口
semanage port -a -t http_port_t -p tcp 7080
semanage port -a -t http_port_t -p tcp 7443

# 防火墙放行
firewall-cmd --zone=public --add-port=7080/tcp --permanent
firewall-cmd --zone=public --add-port=7443/tcp --permanent
firewall-cmd --reload

# 然后再启动 apache 就能成功了，apache 监听的端口成功被我们改变了
```

- 接下来就可以配置 nginx 了；
- 可以先用 **rpm -ql nginx** 来查看一下 nginx 的相关文件

## 9-6 配置 Nginx 作为反向代理服务器，虚拟主机和 HTTPS 配置

### 配置 nginx 作为反向代理服务器，虚拟主机

打开 nginx 的配置文件：**vim /etc/nginx/nginx.conf**

`/etc/nginx/nginx.conf`

```shell
# 在配置文件里面加上这么些东西：

# 这些是针对 http 的；定义上游，对应了服务器的地址
upsteam backend-jenkins {
    server 127.0.0.1:8080;
}
upsteam backend-apache {
    server 127.0.0.1:7080;
}

# 类似于 apache 里面的 virtualHost 虚拟主机的配置
server {
	#...

	# 可以修改一下 server_name，改成我们要去访问的域名
	server_name www.xxx.com xxx.com;
	
	# 加一下 location；一个用来反向代理 apache ，一个用来反向代理 jenkins
	# proxy_pass 相当于转接的意思，如果我们去访问 /jenkins，就相当于是访问 127.0.0.1:8080
	location / {
		proxy_pass http://backend-apache;
	}
	location /jenkins {
		proxy_pass http://backend-jenkins;
	}
	
	#...
}
```

### https 配置

```shell
# 首先复制一下证书
pwd # /etc/nginx/pki

mkdir pki
cd pki
# 把以前给 apache 配置的证书和私钥拷贝到当前目录
cp /etc/httpd/pki/server.crt /etc/httpd/pki/server.key .
```

`/etc/nginx/nginx.conf`

```shell
# 这是 http 的 server 块
server {
	# 将原来的 location 删掉，然后做一个重定向
	return 301 https://$host$request_uri;
}

# Settings for a TLS enabled server
server {
	#...
	
	# 修改一下证书和密钥的路径
	ssl_certificate "/etc/nginx/pki/server.crt";
	ssl_certificate_key "/etc/nginx/pki/server.key"
	
	# 把上面 http 的 server 里面的 location 删掉，在 https 的这个 server 里面加上：
	location / {
		proxy_pass http://backend-apache;
	}
	location /jenkins {
		proxy_pass http://backend-jenkins;
	}
	
	#...
}
```

## 9-7 安装 Squid 作为代理服务器