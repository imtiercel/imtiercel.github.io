---
title: Hexo + GitHub搭建个人博客 --- Standard Edition
date: 2017-09-20 11:44:59
tags: 
	- hexo
	- blog
categories: blog搭建
cover_picture: http://ojirj5wkr.bkt.clouddn.com/github+hexo.jpg

---
``
摘要：想搭建博客这个想法，相信很多人都有过。而像我这个高中时期就开始玩blog的人更是早早萌生过想法。但是想和做还是差了一点，最近花些时间来搭建，希望能给需要的朋友提供一些帮助。
``
## 搭建基础
本博客是基于Hexo + GitHub 在 Windows 10(64位) 和 windows7(64位) 环境下搭建的，搭建前默认有GitHub账号并会基本的Git命令，如果没有请先自行了解学习。

**使用GitHub Pages服务搭建博客的好处有：**

- 全是静态文件，访问速度快；
- 免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；
- 可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；
- 数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行；
- 博客内容可以轻松打包、转移、发布到其它平台；

## 特别提示


- [x] 务必使用Git Bash，可以避免很多问题。
- [x] 如果使用`hexo s`后打不开`http://localhost:4000`网址，那么请检查是否安装了**福昕阅读器**，就是它，占用了端口。
- [x] 上一条的解决办法：`hexo s -p 5000` 改用端口5000。
- [x] 为了避免出现问题，请将本文中写入的hexo插件都执行一遍。

## 一、环境准备

### 1.Node.js   [首页](https://nodejs.org/en/)                                                        [下载地址](https://nodejs.org/en/download/)                                                        [安装教程](http://www.runoob.com/nodejs/nodejs-install-setup.html)

```	
node -v   //验证node是否安装成功（windows下基本就是点下一步就可以了）
```
	
### 2.Git   [首页](https://git-scm.com/)                                                        [下载地址](https://git-scm.com/downloads)                                                                                                                [安装教程](http://www.runoob.com/git/git-install-setup.html)

```
git --version   //验证git是否安装成功（windows下基本就是点下一步就可以了）
```

## 二、安装Hexo

### ①Hexo  [首页](https://hexo.io/)                                                        [文档](https://hexo.io/docs/)                                                        [主题](https://hexo.io/themes/)

```
npm install hexo-cli -g 		//安装hexo命令
hexo init				// 部署hexo，初始化命令
npm install 				// 安装插件命令
目录结构：
    初始化hexo目录
       ├─node_modules			// hexo的插件目录
       ├─scaffolds			// layout模板文件目录，其中的md文件可以添加编辑
       |    ├─draft.md
       |    ├─page.md
       |    └─post.md
       ├─source				// 文章源码目录，该目录下的markdown和html文件均会被hexo处理
       |    |				// 该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等都应该放在这里
       |    └─_posts			// 发布文章
       ├─themes				// 主题文件目录
       |    └─landscape			// hexo初始化默认提供的模板，改模板时就是将需要的模板放到此目录
       ├─.gitignore			// git的忽略规则文件
       ├─_config.yml			// 全局配置文件，大多数的设置都在这里
       └─package.json			// 应用程序数据，指明hexo的版本等信息，类似于一般软件中的关于按钮
       
```

**初始化结束可能会看到如下打印信息**
```
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.2:
wanted{"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"ia32"})
```

可以直接无视，网上查了下，意思就是FS Events这个工具不匹配。这个工具是Mac下的，所以在windows下无视即可，无影响。

### ②几个常用的hexo插件
```
npm install hexo-generator-index --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-tag --save
npm install hexo-server --save
npm install hexo-deployer-git --save			// 集成git进行deploy
npm install hexo-deployer-heroku --save
npm install hexo-deployer-rsync --save
npm install hexo-deployer-openshift --save
npm install hexo-renderer-marked@0.2 --save
npm install hexo-renderer-stylus@0.2 --save
npm install hexo-generator-feed@1 --save		// 安装 RSS 插件
npm install hexo-generator-sitemap@1 --save 		// 生成站点地图
npm install hexo-filter-flowchart --save 		// 支持流程图解析
npm install hexo-generator-search --save		// 站内搜索
npm install hexo-generator-searchdb --save		// 站内搜索
npm install hexo-generator-baidu-sitemap --save 	// 生成百度站点地图
npm install hexo-generator-seo-friendly-sitemap --save  // SEO优化
npm install hexo-html-minifier --save 			// HTML压缩
npm install hexo-clean-css --save 			// CSS压缩
npm install hexo-uglify --save 				// JS压缩
npm install hexo-imagemin --save 			// imagages压缩
```
`强行插入一条(坑)：在执行hexo s之前一定要检查一下4000端口是否被占用`
```
netstat -ano | findstr 4000
如果被占用就用下面的方法更换端口或者卸载**福昕阅读器**你没看错，就是这个坑爹的阅读器。
```
### ③几个常用的hexo命令
```
hexo new "postName"			// 新建文章
hexo new page "pageName" 		// 新建页面
hexo clean				// 清理目录
hexo generate				// 生成静态页面至public目录
hexo server				//开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy				// 将.deploy目录部署到GitHub
### 以上命令对应的简写
hexo n
hexo clean
hexo g
hexo s
hexo d
### 当然，每次一个命令也是比较烦的，尤其是调试效果的时候，所以可以这样
hexo s -g				// 先生成再启动
hexo s -g -p 5000			// 先生成再启动，端口使用5000
### 这里调试的时候直接刷新页面就可以看到更新，之前不知道净关闭，重启了。也是醉了！
### 如果写个脚本来执行也可以。
```
## 三、GitHub注册及创建仓库

### 1.GitHub账号注册(略)

### 2.创建仓库
	
创建仓库：Repository name 使用自己的用户名，仓库名规则：

注意：`yourname` 必须是你的用户名。
	
`yourname/yourname.github.io`

![repository](http://oph264zoo.bkt.clouddn.com/17-5-28/42622869.jpg)

访问 `yourname.github.io`，如果可以正常访问，那么 Github 的配置已经结束了。

## 四、hexo和GitHub创建联系

在hexo的配置文件中 `_config.yml`  加入以下内容(把yourname替换成自己的)
```
deploy:
  type: git 								#推送方式
  repository: https://github.com/yourname/yourname.github.io.git	#你的推送地址
  branch: master 							#你要推送的分支
```
`这里冒号后面有一个空格，需要注意。不然报错。`

## 五、将blog发布到GitHub上

hexo clean
hexo g
hexo d

执行以上三条命令即可，最后一步会有提示输入用户名和密码。但是每次提交都要写用户名和密码岂不是很麻烦，下一篇将讲述如何避免此问题。

目前技术博客简单列表

| 名字      |    地址  | 创办年  |  备注  |
| :--------:|:--------:| :--: |
| 新浪      | www.sina.com.cn/ |  1998年 | 非技术起家 |
| CSDN  | www.csdn.net/ |  1999年   |-----|
| iteye      |    www.iteye.com/ | 2003年  |原名javaEye|
| 博客园    |   www.cnblogs.com/ |  2004年  |-----|
| 51CTO      |    www.51cto.com/ | 2005年  |-----|	
| Stack Overflow      |    stackoverflow.com/ | 2008年  |问题命中率很高，前身也是两个blog|	
| 简书      |    www.jianshu.com/ | 2013年  |-----|
