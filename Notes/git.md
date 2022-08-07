

## git操作

### 基础操作

参考链接：[(3条消息) git的正确打开方式_leeayu的博客-CSDN博客_git文件怎么打开](https://blog.csdn.net/qq_23225073/article/details/105613864)



### 项目拉取

>1. git clone url      将远程仓库克隆到本地
>
>2. git pull origin master     拉取远程仓库的代码（本地已经有版本库了，拉取最新代码，非公开仓库需要输入用户名
>     和密码）



### 项目提交

#### 一、在git上创建好仓库后

参考链接:[手把手教你用git上传项目到GitHub（图文并茂，这一篇就够了），相信你一定能成功！！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/193140870)

> 红色  修改了代码，还没有add
> 绿色  修改了代码，也add了，还没有commit
> 白色   没有修改过代码。 或者修改了add了commit了

```
git init //把这个目录变成Git可以管理的仓库
git add README.md //文件添加到仓库
git add . //不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了 
git commit 文件（不写全部） -m "first commit" //把文件提交到仓库
git remote add origin git@github.com:wangjiax9/practice.git //关联远程仓库
git push -u origin master //把本地库的所有内容推送到远程库上
```



#### 二、提交本地项目初始化好的项目

参考链接：[(3条消息) Git 提交 vue 教程_yiyiyiyi_的博客-CSDN博客_git提交vue代码](https://blog.csdn.net/qiqiyiyi_/article/details/106499340)[(3条消息) 手把手教你初始化Vue项目并部署在github上_爆椒小土豆的博客-CSDN博客_vue项目部署到git](https://blog.csdn.net/xuan950205/article/details/107709722)

```
1. git status   
	查看在你上次提交之后是否有对文件进行再次修改  通常使用 -s 获得简单的查看
2. git add . 
	. 表示所有文件  git add [dir] 指定目录
	命令可将指定文件添加到暂存区  报错了可能需要输入git config core.autocrlf false解决
3. git commit -m "add files（随便写）"
	本地提交 加注释
4. git status  
	本地准备 成功显示：nothing to commit, working tree clean
5. git remote add origin https://github.com/apu-li/first-vue-shop.git（仓库地址） （后续不需要操作）
	创建远程仓库地址别名
	git remote -v 查看提交地址没有则显示为空 就没没提交过
6. git push -u origin main  
	将项目提交到main上  报错 src refspec main does not match any  main改成master
7. git branch  
	查看分支  只是查看可不用操作
8. 报错Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
	在这个日期后，需要个人访问令牌
	pu_liang@163.com Personal asscess token ：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
```

出现的问题

参考：[(5条消息) git restore 和 git restore --staged 的区别_一醉自救的博客-CSDN博客_git restore](https://blog.csdn.net/u013493841/article/details/104451987)

[GIT撤销修改 restore - 简书 (jianshu.com)](https://www.jianshu.com/p/dcef204dba74)

```
git restore --staged 将文件从暂存区撤回工作区
git restore 将在工作区的文件撤销更改

```





### 版本追溯

>通过不同的版本号追溯到之前版本，想回来切换回最新版本号即可
>
>git reset --hard 版本号
>
>例如：git reset --hard 55ee14e13e64f51170832413e5c567c323c73a0a



### 后悔操作

> 要在 commit（提交）之前撤销 `git add`，运行  `git reset <file>` 或  `git reset` 取消所有更改即可。



### 代码冲突

合并时冲突

>  Merge conflict : 合并冲突
>
> CONFLICT (content): Merge conflict in index.js
> Automatic merge failed; fix conflicts and then commit the result.
>
> 自动合并失败；修复冲突，然后提交结果。



### git分支

> 1. 查看分支
>
> git branch 
>
> 2. 创建分支
>
> git branch develop (develop为分支名，一下用这个做例子)
>
> git branch -b develop 表示创建并切换到新分支
>
> 3. 切换分支
>
> git checkout develop
>
> 4. 提交项目到该分支 添加 提交到缓存区 
>
> git push origin develop:develop
>
> 5. 切换到master分支合并分支
>
> git merge develop
>
> 6. 在master分支push代码
>
> 
>
> 老师的代码：
>
> git branch   查看分支情况
> git checkout -b dev   创建并切换到dev分支
> git checkout dev 切换到dev分支
> 切换前先要进行  add 和commit



合并分支：

```
// 当前在master分支 将develop分支合并到master分支
普通：使用merge合并
	git merge develop
高级：rebase合并分支是更高级的合并，也是更推荐的一种合并。Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。
	git rebase develop
tip:看着懂了百度发现并没有那么简单,反正是看不懂
```

> 去b站看了下基本了解，rebase就是会'变基'，这跟merge就区分开来了，变基就是重新合并后会在最新的那里形成新的基点，大概是这样，而merge就是直接合并过去

链接：[Git命令之rebase合并分支 - 南风丶轻语 - 博客园 (cnblogs.com)](https://www.cnblogs.com/rainbow-tan/p/15312981.html#:~:text=1、git rebase实现合并分支的步骤（举例说明） ①在master分支上拉出一个branch4分支，拉出一个branch5分支，拉出一个branch6分支，进行测试。 ②先直接在master上添加一个文件，便于后续的观察，添加完文件后，使用git,add 和git commit 以及git push推送到远端master分支上。)



### 免密提交

> 想要免密提交要配置好公钥
>
> 1. 生成公钥
>
> 打开C:\Users\Pu-liang\.ssh 在这个目录打开git bash，输入： ssh-keygen -t rsa   密码可甜可不填，打开pub结尾的就是公钥
>
> 2. 打开码云个人中心的ssh公钥那里添加公钥，输入密码即可
> 3. 回到项目 使用ssh这个链接 重新克隆项目即可



### 常见问题

> 项目的初次git add 文件时，需要配置：
> 设置个人信息：
> git config --global user.email "xxx@xxx.com"
> git config --global user.name "xxxxe"

>当你本地的项目是落后于仓库里面的项目时，把本地项目push上去是不可行的汇报如下错误(错误一)，这时候只需要把仓库里面的项目拉取过来（git pull origin master），再重新push上去既可。

```git

git pull origin master            // 把远程仓库最新代码拉取到本地
git status                     	  // 查看状态
git add .(文件name)                //添加文件到本地 
git commit -m “push commit”      //添加文件描述信息
git status                        // 再次查看状态
git push origin master        // 重新推送 
```

```
错误一、
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```



> 报错：Unable to negotiate with 106.52.160.162 port 22: no matching host key type found. Their offer: ssh-rsa

>到当前用户目录下的.ssh文件中创建config文件（config没有后缀），使用记事本打开添加如下
>
>Host *
>HostkeyAlgorithms +ssh-rsa
>PubkeyAcceptedKeyTypes +ssh-rsa

随后就遇到了个权限问题： 

> Permission denied (publickey).
> fatal: Could not read from remote repository.

这时候重新生成新的公钥或者客户端要与服务端的公钥匹配



### 进阶（新增）

场景：在其他分支修改了代码，但是不想删，其他分支需要

这时候可以使用 git stash 先暂存起来

```bash
git stash 
```





## svn操作

所需要文件

> svn服务器VisualSVN server：[Apache Subversion Binary Packages](https://subversion.apache.org/packages.html)
>
> svn客户端TortoiseSVN：[Downloads · TortoiseSVN](https://tortoisesvn.net/downloads.html)
>
> 安装自行百度
>
> 参考链接：[SVN的安装与搭建及使用 - 活在记忆里的人 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ftx3q/p/15340160.html)







## nmp常用命令

### 查看包版本

```
查看多个版本：
	npm view xxx versions
	如：npm view less-loader versions
```



### 安装脚手架和初始化项目

参考链接：[一. Vue项目初始化 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/399838171)

```
1. npm安装
	npm install -g @vue/cli
2. 查看版本
	Vue -V
3. 创建项目
	3.1.可视化方式：vue ui
	3.2.命令方式：vue create my-project (有一堆配置选择)
```



### 安装nanoid或者uuid

```
1.安装
	npm i nanoid //uuid为npm i uuid   
2.引入
	import {nanoid} from 'nanoid'  //nanoid为函数
3.使用
	nanoid() 
```

