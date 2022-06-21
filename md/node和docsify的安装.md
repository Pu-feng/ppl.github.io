# Linux安装node和docsify



## node安装

安装node也可以使用nvm进行安装，而且使用nvm切换版本也方便，但是不知道为啥我用nvm安装的node，在下载docsify的时候会报错，说啥啥命令失败，于是乎我用了源码的安装方式。（我用的linux是CentOS 7.6）

1. 使用yum安装wget（下载文件的工具）

```bash
yum install -y gcc make gcc-c++ openssl-devel wget
```



2. 下载node，先创建好目录，待会存放好容易找到，我这里放到了/usr/local/node，版本号可以自己修改

```bash
wget https://nodejs.org/dist/v16.15.1/node-v16.15.1-linux-x64.tar.xz
```

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206201916285.png"/>



3. 对下载好包解压

```bash
tar xvf node-v16.15.1-linux-x64.tar.xz
```



4. 解压好cd进入到解压文件夹找到bin目录再cd进去，查看node版本。在这里pwd看下路径随便复制，方便后面配置环境变量

```bash
./node -v
```

<img src="https://cdn.jsdelivr.net/gh/Pu-feng/mdimages/202206201918753.png"/>

5. 配置全局的环境变量，进入到/etc，编辑profile文件，在最后加上node路径，也就是前面bin目录下的

```bash
vi /etc/profile
```

在配置文件加上export PATH=$PATH:你的路径

```txt
export PATH=$PATH:/usr/local/node/node-v16.15.1-linux-x64/bin
```

6. 让文件生效

```bash
source /etc/profile
```

这时候在哪里都可以使用node -v查看到版本号了



## 安装docsify

node是自带npm的所以我们直接用就行

1. 全局安装docsify

```bash
npm i docsify-cli -g
```



2. 在想要的目录下初始化项目，进入到mydoc可以看到初始化好的文件

```bash
docsify init ./mydoc
```

初始化之后其实有三个文件，`index.html`、`README.md`、`.nojekyll`。

- `index.html`：入口文件，docsify 的各项配置都在此页面设置。
- `README.md`：默认展示的首页就是 `README.md` 里的内容。
- `.nojekyll`：用于阻止 GitHub Pages 会忽略掉下划线开头的文件。



3. 在本地进行预览，默认端口为http://localhost:3000

```bash
docsify serve mydoc
```

