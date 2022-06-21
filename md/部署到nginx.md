# 记录一个部署静态到服务器（nginx）

## 一、前置知识



### 1、linux系统

#### 什么是Linux

> Linux是一套免费使用和自由传播的类Unix操作系统，是一个多用户、多任务、支持多线程和多CPU的操作系统。它能运行主要的UNIX工具软件、应用程序和网络协议。它支持32位和64位硬件。Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。

#### Linux 的主要应用场景

1. 服务器领域
2. 嵌入式设备 (路由器,交换机,空调,冰箱…)
3. 移动端 

#### 常见命令

|       操作       |  命令   |                    例如                    |
| :--------------: | :-----: | :----------------------------------------: |
|     切换目录     |   cd    |             cd ..  和 cd /test             |
|   显示当前目录   |   pwd   |                    pwd                     |
|     创建目录     |  mkdir  |                mkdir 目录名                |
|     创建文件     |  touch  |                touch 文件名                |
|     查看文件     |   cat   |                 cat 文件名                 |
| 查看当前路径文件 |   ls    |       查看隐藏文件 ls -a  和 详细 ll       |
|     复制文件     |   cp    |  cp 源路径 目标路径(可以覆盖原来有的文件)  |
|     移动节点     |   mv    |       mv 源路径 目标路径(修改文件名)       |
|     删除文件     |   rm    |                rm 文件路径                 |
|     删除目录     |  rm -r  | rm -r 目录路径  -r表示 一直往下找 全部删除 |
|   强行删除目录   | rm -rf  |         rm -rf 目录路径 -f表示强行         |
|    建立软链接    |  ln -s  |            ln -s 真实文件 链接             |
|     编辑文件     |   vi    |                  vi 文件                   |
|     查看进程     | ps -ef  |                   ps -ef                   |
|   强行杀死进程   | kill -9 |                kill -9 PID                 |

#### Linux 发行版

1. **ubuntu** 可以用来在网上查询一些 Linux 的资料
2. **debian** 致力于创建自由操作系统的合作组织及其作品
3. **redhat** （红帽）是企业中使用的最多的一个 Linux 系统.收费,但是提供商业服务.
4. **centos** 这个和redhat代码一样,只是把 redhat 发行的源代码去掉了 log 商标.
5. **deepin** 深度,这是一个国产的操作系统

ubuntu

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101320.png"/>



debian

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101301.png"/>



CentOS

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101318.png"/>



Kali Linux是基于[Debian](https://baike.baidu.com/item/Debian/748667)的[Linux](https://baike.baidu.com/item/Linux/27050)发行版

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101319.png"/>



> 有用过的：**deepin** 深度，**Manjaro**是一款基于Arch Linux、对用户友好 

Manjaro

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101298.png"/>



深度OS

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101300.png"/>



### 2、什么是服务器

> **服务器**也是电脑，**服务器是为电脑提供服务的电脑**，既然是电脑，那么它也一样是由CPU，主板，内存条，硬盘，机箱，电源等硬件组成。

#### 为什么是Linux

1. 开源：Linux系统可用于开源用途，通过开源使用者不仅可以看到Linux内核的代码，还可以对代码进行修改和搭建。

2. 稳定性：使用Linux系统的用户很少会遇到系统崩溃的情况，甚至在运行多年的时候也不会出现重大的事故和问题，稳定性是非常不错的。

3. 灵活性：Linux系统最大的特点就是灵活，用户可以对Linux系统进行自定义，通过编程接口，将自己开发的工具和程序添加到系统中，可以打造出更加符合你的标准的用户桌面，其次shell作为Linux系统最大的组件，完全可以让运行的程序与内核进行交互。

4. 硬件：对比Windows系统来说，Linux对于硬件的需求是比较低的，不需要频繁的进行升级。

5. 安全：Linux系统只有管理员以及特定用户才可以访问内核权限，所以安全方面比较高，受到可能性小。

6. 成本低：Linux是免费的操作系统，成本会下降很多，即便购买付费的Linux系统降低也是非常低的。

7. 易变更：可以在不重启服务器的情况下，自由地对系统进行变更，无需购买其他版本才能使用某些特定的功能。

#### 服务器的购买

> 阿里云、腾讯云等网上蛮多





## 二、连接服务器安装

### 1. 连接服务器

> 可以使用页面自带的，我这里用的xshell连接。（如果重装了系统的可能需要重置密码才方便用ssh登录）

连接配置（端口）

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202129784.png"/>

连接成功，可以看到只有黑窗口

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101303.png"/>



### 2. 安装nginx

### 是啥

> Nginx是一款[轻量级](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E8%BD%BB%E9%87%8F%E7%BA%A7/10002835)的[Web](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/Web/150564) 服务器/[反向代理](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86/7793488)服务器及[电子邮件](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E7%94%B5%E5%AD%90%E9%82%AE%E4%BB%B6/111106)（IMAP/POP3）代理服务器，在BSD-like 协议下发行。其特点是占有内存少，[并发](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E5%B9%B6%E5%8F%91/11024806)能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx网站用户有：百度、[京东](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E4%BA%AC%E4%B8%9C/210931)、[新浪](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E6%96%B0%E6%B5%AA/125692)、[网易](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E7%BD%91%E6%98%93/185754)、[腾讯](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E8%85%BE%E8%AE%AF/112204)、[淘宝](https://link.zhihu.com/?target=https%3A//baike.baidu.com/item/%E6%B7%98%E5%AE%9D/145661)等。

### 步骤

1、yun安装

```
yum install nginx
```

2、``whereis nginx`` 查看到哪以及配置信息目录，也可以用```nginx -v```看有没有安装成功。

```
nginx -v
```

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101305.png"/>

3、进入目录，可以看到一堆配置文件

```
cd /etc/nginx
```

4、启动Nginx

```
service nginx start 不行
systmectl start nginx 换这条
// 查看  有没有启动成
systemctl status nginx
```

看到这个绿色的active，就是开启成功了

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101304.png"/>

这时候在浏览器输入公网ip看是否能访问到



> 防火墙设置，没有开过不用管

安装之后开启 Nginx，如果系统开启了防火墙，那么需要设置一下在防火墙中加入需要开放的端口，下面列举几个常用的防火墙操作（没开启的话不用管这个）：

```shell
systemctl start firewalld  # 开启防火墙
systemctl stop firewalld   # 关闭防火墙
systemctl status firewalld # 查看防火墙开启状态，显示running则是正在运行
firewall-cmd --reload      # 重启防火墙，永久打开端口需要reload一下

# 添加开启端口，--permanent表示永久打开，不加是临时打开重启之后失效
firewall-cmd --permanent --zone=public --add-port=8888/tcp

# 查看防火墙，添加的端口也可以看到
firewall-cmd --list-all
```



## 三、部署静态

想办法把打包好的资源放到服务器上面，方法很多，我用的```fileZilla```可视化不用钱。还有也可以使用git将资源弄上去

#### 1、配置站点连接上服务器

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202132386.png"/>

连接成功

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202133642.png"/>



#### 2、修改nginx配置文件```nginx.conf```

- 进入配置文件目录

```
cd /etc/nginx
```

- 使用vi编辑器编辑```nginx.conf```

```
vi nginx.conf
也可以在任意目录编辑配置文件
vi /etc/nginx/nginx.conf
```

Linux vi 命令也就是指 vi 编辑器，它们是一个意思。vi 编辑器是 Linux/UNIX 环境下经典的编辑器。Linux vi 命令非常强大，熟练地使用它可以高效的编辑代码，配置系统文件等，是程序员和运维人员必须掌握的技能。

vim编辑器三个模式

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101309.png"/>

nginx配置文件信息

```
main        # 全局配置，对全局生效
├── events  # 配置影响 Nginx 服务器或与用户的网络连接
├── http    # 配置代理，缓存，日志定义等绝大多数功能和第三方模块的配置
│   ├── upstream # 配置后端服务器具体地址，负载均衡配置不可或缺的部分
│   ├── server   # 配置虚拟主机的相关参数，一个 http 块中可以有多个 server 块
│   ├── server
│   │   ├── location  # server 块可以包含多个 location 块，location 指令用于匹配 uri
│   │   ├── location
│   │   └── ...
│   └── ...
└── ...
```



- 找到server这个配置项，做如下配置

```conf
server {
        listen       80;
        listen       [::]:80;
        server_name  localhost;
        root         /usr/share/nginx/html;


		location / {
			# root 需要部署的静态目录
			root	/usr/local/html;
			index	index.html index.htm;
		}
			
        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
}
```

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202101317.png"/>



#### 3、重启nginx

```
nginx -s reload
```

这时候去访问公网ip就可以看到刚当上去的页面了

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206202135403.png"/>



#### 4、跨域解决

> 添加这个就可以

```
location /api {
	proxy_pass 跨域地址的baseURL;
}
```



#### 5、刷新404

```
location / {
	# root 需要部署的静态目录
	root	/usr/local/html;
	index	index.html index.htm;
	try_files $uri $uri/ /index.html;
}

```

