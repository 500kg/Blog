---
title: 多终端管理Blog
tags: [Blog]
categories: [Blog]
date: 2017-09-09 19:19:56
---

弄了一晚上吧，实现了异地管理博客的想法。

这篇文章主要还是一些经验总结。

<!--more-->
# 一、上传博客文件 #

在github中创建一个New repository，在博客文件夹中右键git bash here后执行如下指令：
```
git init
git config --global user.name "A"
git config --global user.email "B"
git remote add origin git@github.com:C/D.git

```
其中，A是你的用户ID，B是你注册所用邮箱，C也是ID，D是用于储存Blog的位置（即repository)如此即可。


# 二、在异地进行初始化 #

在一台已经安装了Node、Git并在本地有SSD-key后在空文件夹内右键git bash here后执行如下指令：
```
npm install -g hexo
hexo init   #生成静态页面，不确定是否需要

npm install hexo-deployer-git --save   #使得可以使用hexo d指令

git init
git config --global user.name "A"
git config --global user.email "B"
git remote add origin git@github.com:C/D.git

```
其中，A是你的用户ID，B是你注册所用邮箱，C也是ID，D是用于储存Blog的位置（即repository)

如上操作使得你有了一个可以正常发表的初始博客并将此文件夹与网上的repository绑定。

# 三、下载并更新博客 #


执行完“二”后便可以执行如下操作：

```
git fetch --all
git reset --hard origin/master

```

如上操作

1、使你下载了储存在github中的博客文件

2、使当前文件夹拥有上传权限（我猜的我也不知道）

在写完你的博客后智慧三连，更新博客。

```
hexo clean
hexo g
hexo d

```

再智慧三连，更新github中的文件。

```

git add .
git commit -m "更新说明"
git push origin master

```

如此就可以再异地更新完博客了

要在原来的地方更新博客只需要在再进行一遍“三”操作即可。


# 附录 #

以下是我个人的一些指令

在新的地方配置：

```
npm install -g hexo
npm install hexo-deployer-git --save
hexo init
git init
git config --global user.name "500kg"
git config --global user.email "2426958134@qq.com"
git remote add origin git@github.com:500kg/Blog.git
git fetch --all 
git reset --hard origin/master

```

下载：

```
git fetch --all #或git pull
git reset --hard origin/master
```

上传
```
hexo clean
hexo g -d
git add .
git commit -m "date"
git push origin master

```

以下是我的github地址，欢迎follow或star

[https://github.com/500kg/](https://github.com/500kg/)