---
title: Hexo + GitHub搭建个人博客 --- Standard Edition
date: 2017-09-18 11:44:59
tags: 
	- web 
	- html5
cover_picture: http://oerolc7og.bkt.clouddn.com/images/miho/theme/github-second.jpg

---
``
    摘要：想搭建博客这个想法，相信很多人都有过。而像我这个高中时期就开始玩blog的人更是早早萌生过想法。但是想和做还是差了一点，最近花些时间来搭建，希望能给需要的朋友提供一些帮助。
``
## 搭建博客原理简介
Github提供信息库托管个人，组织或项目页面。
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
上面的描述就很清楚了。Github提供了一个放资源的地方；Hexo提供了一个快速生成静态网页的功能。
下面就开始搭建本地Hexo，但是Hexo依赖于Node.js和git。
	
### 1.Node.js   [首页](https://nodejs.org/en/)                                                        [下载地址](https://nodejs.org/en/download/)                                                        [安装教程](http://www.runoob.com/nodejs/nodejs-install-setup.html)

```	
node -v   //验证node是否安装成功（windows下基本就是点下一步就可以了）
```
	
### 2.Git   [首页](https://git-scm.com/)                                                        [下载地址](https://git-scm.com/downloads)                                                                                                                [安装教程](http://www.runoob.com/git/git-install-setup.html)

```
git --version   //验证git是否安装成功（windows下基本就是点下一步就可以了）
```

### 3.Hexo  [首页](https://hexo.io/)                                                        [文档](https://hexo.io/docs/)                                                        [主题](https://hexo.io/themes/)

```
npm install -g hexo			// 安装hexo
hexo init				// 初始化hexo(当前文件夹)
目录结构：
    初始化hexo目录
       ├─node_modules			// hexo的插件目录
       ├─scaffolds			// layout模板文件目录，其中的md文件可以添加编辑
       |    ├─draft.md
       |    ├─page.md
       |    └─post.md
       ├─source				// 文章源码目录，该目录下的markdown和html文件均会被hexo处理
       |	|			// 该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等都应该放在这里
       |	└─_posts		// 发布文章
       ├─themes				// 主题文件目录
       |	└─landscape		// hexo初始化默认提供的模板，改模板时就是将需要的模板放到此目录
       ├─.gitignore			// git的忽略规则文件
       ├─_config.yml			// 全局配置文件，大多数的设置都在这里
       └─package.json			// 应用程序数据，指明hexo的版本等信息，类似于一般软件中的关于按钮
       
```

### 4.在其他电脑下载分支hexo

git clone -b hexo https://github.com/yourname/yourname.github.io.git

```
npm install hexo --save     // 安装hexo
npm install -g hexo-cli     // 安装hexo的client
npm install 				// 

git push origin hexo:hexo
```
