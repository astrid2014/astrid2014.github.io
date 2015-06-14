---
layout: post
title: "在 Win7 下使用 Octopress 搭建个人博客"
date: 2015-05-18 21:33:49 +0800
comments: true
categories: 
---
##说在前面的话
不同于 QQ 空间、朋友圈，记录的多是一时的心情；不同于微博，更多的时候也只是转发
一些大 V 的观点。一个属于自己的个人博客，就像是一个温暖的窝，可以让你来到这方净土时充满归属感，只有在这片土地上，你并不是临时的租户。
##搭建博客环境
搭建博客跟搭建房子一样，首先要布置好环境、准备好建筑材料，来搭建房子的框架。那么搭建博客首先，也是重中之重，就是要搭建好博客的环境：
###Step1：安装 Git
下载并安装 [git](http://git-scm.com/) ，我安装的是1.9.4版本，此步骤比较简单，这里就不做赘述；
###Step2：安装 Ruby
下载并安装 [Ruby](http://rubyinstaller.org/downloads/)，我安装的是2.0.0版本。本步骤十分关键也非常容易出错，本步骤没有执行好，后面将会导致各种错误，这可是妹纸我血和泪的教训。  
**注意事项：**  
安装时记得勾选 *`“Add Ruby executables to your PATH”`* ，将 Ruby 的执行路径加入到环境变量中，如果忘记勾选，亦可手动设置。  
安装完成后在命令提示符中输入 *`ruby --version`* 来确认是否安装成功。   
###Step3：安装DevKit
下载并安装 [DevKit](http://rubyinstaller.org/downloads/)，DevKit下载是一个压缩文件，将其解压到 *`E:/DevKit`*。  
**注意：** 

- 安装目录中没有中文和空格  
- 必须先安装 Ruby ，而且 Ruby 需要是 *`RubyInstallser`* 安装  
- DevKit 的版本必须跟 Ruby 的版本相对应，否则会报错，切记切记！——妹纸我在搭建过程中就栽在了

解压后在命令行先后输入以下命令来进行安装：  
```javascript 
e:  
cd DevKit  
ruby dk.rb init  
ruby dk.rb install
```
###Step4：安装 Python
下载并安装 [Python](http://www.python.org/ftp/python/2.7.5/python-2.7.5.msi) ，注意要把 E:\Python27\Scripts 和安装文件的根目录 E:\Python27 写进环境变量中，否则后续操作会引起报错——这个同样是妹纸我血泪的教训。  
博客的代码高亮用到了 *`Python`* 的 *`Pygments`* 模块，在 Python 中安装第三方库需要使用 *`easy_install`* 。

###Step5：安装 Octopress
在 *`GitBash`* 先后输入如下命令将 Octopress 代码拉到本地：  
```javascript 
cd d:/GitProject   
git clone git://github.com/imathis/octopress.git octopress  
```
然后需要安装 *`Octopress`* 的依赖项：  
  安装依赖项需要用到 *`Ruby`* 的 *`gem`* ，使用下面的命令可以更换 gem 的更新源，使用国内的淘宝镜像速度相对快点。  
```javascript 
  gem sources -a http://ruby.taobao.org/   
  gem sources -l
```
修改 *`Octopress`* 目录下的 *`Gemfile`* 文件：  
  将第一行的 *`http://rubygems.org/ `* 修改为 *`http://ruby.taobao.org/`*   

在命令提示符中进入到 *`Octopress`* 目录，输入下面命令进行依赖项的安装  
```javascript   
gem install bundler  
bundle install
```
输入下面的命令来安装 *`Octopress`* 的默认主题  
```javascript  
rake install
```

###Step6：解决中文问题

到此所有的准备工作已经结束，可以写博客了。

***
##写博客之前
在写博客之前，你首先需要花几分钟来了解一下[ markdown](http://wowubuntu.com/markdown/#list) 的语法；此外这里有一个[在线编辑工具](http://mahua.jser.me/)，可以帮助你一边写博客一边查看页面的效果，十分方便；另 [Sublime Text3](http://www.sublimetext.com/3) 也是一个非常棒的编辑工具。

***
##写博客 
  **在环境搭建好的情况下，使用 *`Octopress`* 写博客大致有以下几个步骤：**  
  1. 执行以下语句来生成一篇博文：  
```javascript  
rake new_post['title']  
```  
其中 “title” 并不是博文标题，而是和生成的文件名以及 URL 有关，该名称不支持中文；博客的标题可以在生成的 markdown 文件中的 “title” 修改，可为中文。  
  2.在 octopress\source\_posts 目录下 ，找出对应生成的 *`markdown`* 文件，使用 Sublime Text3 和 markdown 语法来编辑博客内容；  
  3. 执行 *`rake generate`* 来生成文章；  
  4. 执行 *`rake preview`* 在本地 localhost:4000 进行预览；  
  5. 执行 *`rake deploy`* 发布到 *`Github`* 中;   
  6. 执行下面命令,将修改的源码推送到 *`source`* 分支：  
```javascript
git add .
git commit -m “your message”
git push origin source
```

***
##将 Octopress 发布到  GitHub Pages

***
##一些心得体会
* 不要看到命令行就不爽，要仔细读：我仅以我个人来说，我看到黑屏就不是很爽，有时更有种犯晕的感觉，不知道是不是只有妹纸才会这样反感，反正我以往是压根不会仔细看命令行中的提示的，仅仅执行命令就行了，除了发生了error会看一下，其他的提示信息都不看，其实这是不行的，黑屏其实除了error还有一些提示，或者注意事项，是应该仔细看看的，不加以注意，很容易会导致在后续的步骤中报错。在这次搭建博客的额过程中我就吃到了苦头了。

* 不知道是否因为我个人网络的原因，很多命令执行的时候都有报错，但是重复执行几次命令就可以了，error都不见了。

* 遇到问题多多百度、多google，要有耐心，学会自己解决问题。当自己一个个把问题都解决掉的时候，你将会产生一股成就感，而这种成就感将会成为你继续前进的信心与动力。

