---
title: Hexo+Github搭建个人博客
date: 2018-08-28 15:34:25
cover_picture: images/IMG_1568.jpg
tags:
- github
- 部署
categories:
- github
---
欢迎来到我的博客驿站，本站是使用Hexo+Github基于基于Node.js的静态博客框架, 官方文档请参考[Hexo](https://hexo.io)

## Quick Start

### 环境要求
#### 安装Node（基础环境）
[Node官网](https://nodejs.org/en/download/)你可以根据不同平台系统选择你需要的Node.js安装包
注意：Linux上安装Node.js需要安装Python，建议安装Python 3.6以上版本。
#### 安装Git
目的：把本地的hexo内容提交到github上去.首先去[GitHub](http://www.github.com)申请个人账号，以便后期用来做博客的远程创库、域名、服务器之类的，github账号不再啰嗦了,跟一般的注册账号差不多，方便起见，顺便配置SSH Keys

### 安装Hexo
开始之前，先切换NPM源， 解释一下，NPM是随同 NodeJS 一起安装的包管理工具，我们经常使用它来下载第三方包到本地。
但在使用 NPM 过程很多人估计都知道，在国内下载第三方包的速度极其之慢。因此推荐使用淘宝 NPM 镜像，它是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 ，操作如下：
终端/CMD里面：
``` bash
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
如此一来就可以使用 cnpm 命令来安装模块了：
``` bash
$ cnpm install xxxx
```
接下来开始安装Hexo，首先在你个人的workspace创建博客文件夹，如myblog
然后cd到myblog里安装Hexo：
``` bash
$ cnpm install -g hexo-cli
```
接下来执行init命令初始化你的hexo：
``` bash
$ hexo init
```
至此，安装工作顺利完成！myblog就是你以后写博客的目录，所有的操作都在里面进行。


### 生成博客

``` bash 
$ hexo g
```

### 预览博客

``` bash 
$ hexo s
```
接下来在浏览器地址栏输入：localhost:4000回车就可以预览你的博客了


### 发布博客

``` bash
$ hexo d
```
### 托管到gitHub
#### 创建repository
创建一个与自己用户名同名的repository
在自己Github主页右下角，创建一个新的repository。比如我的Github账号是NicolasGui，那么我应该创建的repository名字应该是NicolasGui.github.io。
#### 添加git配置
首先在主题的配置文件_config.yml里面添加
``` bash
deploy:
  type: git
  repository: http://github.com/NicolasGui/NicolasGui.github.io.git
  branch: master
```
repository：就是你的gitHub同名仓库的地址
#### 代码上传
安装 hexo-deployer-git依赖包
```
npm install hexo-deployer-git --save
```
然后使用如下命令

```` bash
hexo d
````
此时你可以在浏览器地址栏输入 “用户名.github.io.git”来访问你的个人博客  
(用户名：你gitHub的用户名)
### 域名绑定
#### 域名申请
域名申请的途径非常多，建议使用[阿里云](http://www.aliyun.com)的，方便后期备案，在阿里云购买了域名之后，到域名管理中心进行域名解析，添加以下几条记录值：

记录类型|主机记录|解析线路(isp)|记录值
-|-|-|-
CNAME|www|默认|用户名.github.io
A|@|默认|192.30.252.153
A|@|默认|192.30.252.154

接下来在source目录新建名为CNAME的文件，注意，没有后缀名
然后在CNAME文件里面填写你的域名，如：xxx.com   注意：不带www也不带http，只需要域名就好
接下来分别执行hexo g重新生成一下博客
``` bash
hexo g
```
然后再上传到git
``` bash
hexo d
```
之后就可以使用域名访问你的个人博客了
