---
layout:     post
title:      "github 的配置和使用"
subtitle:   "如何配置ssh 以及常用的命令"
date:       2016-09-15 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - github
---

>github是代码管理的利器，他可以帮助你管理项目代码，如果你有开源项目，希望大家一起帮你完成，那么Github一定是首选。


## 作用

**学一样东西应该先了解，它解决了什么问题，根据问题去思考他问什么要这样处理**

1. 解决了多人开发，代码共享的问题
2. 解决了代码版本控制的问题。
3. 解决了开源项目，代码冲突的问题。
4. 可以集成到测试工具里面

## 入门

去[github 官网](https://github.com/)注册一个自己的账号

输入邮箱密码。。。。下一步

## 创建一个代远端库

两种方式，看图

![](http://www.qinguolei.com/img/in-post/git/git-new.jpeg)

## 初始化

![](http://www.qinguolei.com/img/in-post/git/git-init.jpeg)


## ssh配置

***为什么要配置ssh呢***

问得好，因为不配置的话，谁都有权限提交代码到你的远程库，那你的代码和JN有没有区别

也可以用***HTTPS***的方式 克隆代码，每次提交到远程的是时候，需要输入账号密码（奔溃）

配置好ssh之后，就不需要每次都输入账号密码了

*** mac下 ***

先配置一个git **邮箱**和**姓名**

$ git config --global user.name "thunderqin"
$ git config --global user.email "549458812@qq"

```js
ssh-keygen -t rsa -C “549458812@qq.com”
```

连续按三个确认，得到***id_rsa***和***id_rsa.pub***文件

![](http://www.qinguolei.com/img/in-post/git/ssh.jpeg)

把id_rsa.pub的里面的密钥复制到git官网上面

![](http://www.qinguolei.com/img/in-post/git/git-ssh.png)


然后就可以愉快的写代码了。

## 常用命令

** 克隆 **
进入自己的开发目录

``` js
git clone git@github.com:thunderqin/wx_app.git
```

这段代码不仅会把远端的README 克隆下来，还会将目录和远程建立联系 可以直接Push

** 添加修改

创建一个index.js文件

```js
touch index.js
```
我们需要先添加修改到缓存区

```js
git add index.js
```

## 提交

```js
git commit -m 'add index.js'
```

## 发布

```js
git push origin master
```

## 黑科技

* 每次clone的时候,会把根目录wx_app下载过来，但是有时候不想要这个根目录，怎么办呢？

需要设置当前目录的remote地址

**首先初始化**

```js
git init
```

**设置远端地址**

```js
git remote add origin git@github.com:thunderqin/wx_app.git
```

这样就可以直接pull了

```js
git pull origin master
```

然而 每次拉取提交都需要指定分支 origin master
写多了就烦了

解决方法就是设置默认上游分支
```js
git branch --set-upstream-to=origin/master master
```

![](http://www.qinguolei.com/img/in-post/git/git-upstream.jpeg)
这段代码的作用就是 把当前分支(master)指向远端master分支

这样**pull**或**push**就不需要指定分支了

![](http://www.qinguolei.com/img/in-post/git/git-push.jpeg)

## 其他常用命令

* git status 对比本地和缓存区的修改
* git commit --amend -C HEAD  本次提交追加到上次Log
* git log 查看提价日志
* git diff a.js b.js 查看a和b的不同
* git merge b 把b分支合并到当前分支


## 思考

1. 和svn最大的区别是多了一个缓存区，为什么需要这个缓存区，直接Push不可以吗

答： 因为缓存区可以在你本地形成一个Log树，记录你所有的操作，你从远端fetch代码，也是存在缓存区，
而不是直接拉取到你本地。你可以把缓存区当成一个分支，就这么简单，有利于代码的管理。


![](http://www.qinguolei.com/img/in-post/git/git-cache.png)

2. fetch 和 pull的区别

每次修改代码之前需要执行

```js
git pull origin master
```

pull = fetch + merge.

fetch： 把远程的代码，合并到缓存区里（这个时候本地是没有任何修改的）
merge： 合并缓存区和本地代码

3. 提交时候，提示冲突，怎么解决

* 这种情况很可能是你开发的时候 没有pull最新代码 冲突了 解决的办法就是手动解决


*** 举个栗子 ***

```js
<<<<<<< HEAD

code in master

=======

code in dev

>>>>>>> dev
```

** <<<<<< ** 代表冲突的开始 >>>>代表冲突的结束，把这段代码改成正确的代码就行，然后再次提交

4. git rebase temp

新手老师搞不懂什么时候用rebase,这样说吧，你的commit 中和服务器中的有些commit不再同一时间轴上，即：你的有些commit要插入到服务器中的某些commit之间，这样就会造成代码的冲突。

解决的办法就是，新建一个分支temp，然后把temp的代码rebase过来，这样就保证项目的Log是在一个时间轴上。



### 著作权声明

无