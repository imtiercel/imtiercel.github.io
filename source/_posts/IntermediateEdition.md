---
title: Hexo + GitHub搭建个人博客 --- Intermediate Edition
date: 2017-09-21 16:21:54
tags:
	- hexo
	- blog
categories: blog搭建
cover_picture: http://ojirj5wkr.bkt.clouddn.com/github+hexo.jpg
---
``
摘要：在成功将hexo默认blog发布到GitHub之后，遇到很多需要解决的问题，下面来讲述遇到的问题和解决的办法，希望对大家有一些帮助。
``
## 一、提交输入账号信息问题

### 1.将用户信息放在链接内
将下面链接中的username和passwd换成你的账号名和密码
```
deploy:
  type: git 										#推送方式
  repository: https://username:passwd@github.com/yourname/yourname.github.io.git	#你的推送地址
  branch: master 									#你要推送的分支
```
当然网上也有其他方法，但基本都是将用户名和密码信息配置起来，拿来用的方式。
简单粗暴的方法，但是感觉个人信息被泄露了，这样就有下面的方式。
### 2.使用SSH  key方式
#### ①检查是否已存在SSH key
运行 git Bash 客户端，输入如下代码：
```
cd ~/.ssh
ls
```
`如果是自己生成的可以直接用，如果不是，可以选择删除重新生成，也可以选择不删除指定秘钥名字生成新key。`
#### ②创建一个 SSH key 
```
ssh-keygen -t rsa -C "your_email@example.com" -f ~/.ssh/github

代码参数含义：
-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。
```
一路回车下去就获得 `github` 和 `github.pub` 两个秘钥文件。
#### ③添加SSH key到GitHub
在git Bash 客户端获取public key信息
```
cat ~/.ssh/github.pub
复制这个key的值
```
打开https://github.com登录后进入 `Settings`，在左侧找到 `SSH and GPG keys`
点击右侧 `SSH keys` 后面的按钮 `New SSH key` 
将刚刚copy的信息放入里面。
#### ④测试一下该SSH key
运行 git Bash 客户端，输入如下代码：
```
ssh-agent bash			#连接gitagent
ssh-add ~/.ssh/github		#将刚才生成的key缓存到ssh-agent中
ssh -T git@github.com		#测试连接
```
#### ⑤修改hexo配置
```
deploy:
  type: git 							#推送方式
  repository: git@github.com:yourname/yourname.github.io.git	#你的推送地址
  branch: master 						#你要推送的分支
```
`好了，到这里就配置完成了，再次使用   hexo d    就可以免输入信息了。`
`但是有个问题，ssh-agent是每次都要去加这个key的信息。总比输入密码安全的多吧！`
## 二、多电脑写blog问题
`把我的思路提供给大家，blog必须传到master分支，而且都是hexo命令。`
git本身有分支管理，所以我的想法是在当前repository创建一个hexo分支。然后将blog的一些文件也用GitHub管理即可。
这里的问题就是怎么在另外一台电脑上继续编辑我的blog

#### 1.需要git管理的目录
```
   ├─scaffolds			// layout模板文件目录，其中的md文件可以添加编辑
   ├─source			// 文章源码目录，该目录下的markdown和html文件均会被hexo处理
   ├─themes			// 主题文件目录
   ├─.gitignore			// git的忽略规则文件
   └─_config.yml			// 全局配置文件，大多数的设置都在这里    
```
#### 2.下载hexo分支
```
git clone -b hexo https://github.com/yourname/yourname.github.io.git
```
#### 3.安装环境
参考 [Hexo + GitHub搭建个人博客 --- Standard Edition](https://imtiercel.github.io/StandardEdition/)
需要安装Git，Node.js
下面是hexo安装
```
进入下载的分支目录内
npm install hexo --save     		// 安装hexo
npm install -g hexo-cli     		// 安装hexo的client
npm install 				// 安装插件命令
npm install hexo-deployer-git --save	// hexo用git执行deploy的插件
```
#### *tips
```
push hexo分支的命令
git add 修改的文件
git push origin hexo:hexo
```
## 三、ico生成及图片调整
推荐以下两个连接，会ps就当我没说好了。
[favicon.ico生成](https://www.ico.la/)
[图片调整](http://www.gaitubao.com/)
## 四、中文乱码
由于手动创建md文件可能不是utf-8无BOM的。调整下编码就好。
## 五、保留CNAME、README.md等文件
在博客根目录下的配置文件_config.yml中配置一下"skip_render"选项就行了，将不需要渲染的文件名称加入的其选项下就行了。
