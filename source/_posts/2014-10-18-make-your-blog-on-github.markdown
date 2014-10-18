---
layout: post
title: "Make Your Blog On GitHub"
date: 2014-10-18 10:36:24 +0800
comments: true
categories: octopress
---
在windows8.1环境下利用octopress在GitHub上搭建一个属于自己博客。

需要的软件
-------
<!-- more -->
 1. GitHub的windows客户端，可以去https://windows.github.com/ 下载
 2. ruby和DevKit，可以去http://rubyinstaller.org/downloads/ 下载，尽量下载最新版本。

准备GitHub
--
首先你肯定得有一个GitHub账号了，然后建立一个名字为yourname.github.io的repository，其中yourname就是你GitHub的账户名字啦。
安装刚下载好的GitHub windows客户端，安装好后打开GitShell输入：*ssh-keygen  -t rsa*，一路回车，创建好公钥和私钥。然后到” c:\Users\用户名\.ssh\ “  目录找到   “id_rsa.pub”用记事本打开复制全部内容。然后到GitHub网站，进入设置页面（点击网站右上角的那个齿轮），然后进入SSH Keys（在左边栏点击即可），然后点击Add SSH Key ，随便起个名字，然后将刚复制的内容粘贴到里边保存即可。

安装Ruby
--

首先安装RubyInstaller，安装的时候一定要勾选“Add Ruby executables to your PATH”。然后解压缩DevKit，路径中别包好中文。然后打开“Start Command Prompt with Ruby”，，cd到DevKit刚解压到的目录，依次输入如下命令

    ruby dk.rb init
    ruby dk.rb install
    gem install rdiscount --platform=ruby
执行这些命令的时候可能会出现错误，不要慌张，多试几次就好了，可能是要下载的网站被墙掉了。

安装Octopress
-------
打开GitShell，输入

    git clone git://github.com/imathis/octopress.git octopress
然后依次输入以下命令

    cd octopress
    gem install bundler
    bundle install 
这个时候就可以在本地预览搭建好的博客了输入

    rake generate
    rake preview
然后在浏览器输入 127.0.0.1:4000 即可看到搭建好的博客啦。当然可以做一个个性化的配置，则修改_config.yml中url、title、subtitle、author等等。

发布到GitHub
-------
配置octopress和你的github的绑定，打开GitShll输入

    rake setup_github_pages
按照提示输入github项目的网址，比如我的 `git@github.com:ivxworks/ivxworks.github.io.git`
然后在shell中输入

    rake deploy
至此，博客已经搭建好，等上10几分钟，在浏览器中输入你的地址即可访问啦。
我们执行rake deploy的时候只是将_deploy目录下的内容推到了github的master分支。为了安全期间，我们要将博客的全部内容推到source分支，这样当博客出现问题的时候可以用source分支来恢复博客，具体操作如下，cd到octopress根目录，在shell中输入

    git add .
    git commit -m 'your message'
    git push origin source

写博客
-------
写博客前最好先同步一下本地和github

    cd octopress
    git pull origin source
    cd ./_deploy
    git pull origin master
开始写博客

    rake new_post["New Post"]
    rake generate
    git add .
    git commit -am "Some comment here." 
    git push origin source
    rake deploy
    rake preview

至此一个博客已经搭建好了，当然这只是刚刚开始，后边的优化还多这呢~~

参考：
http://oec2003.github.io/blog/2013/06/26/octopress-blog-setting/
http://wangzz.github.io/blog/2014/04/28/custom-your-octopress-blog/
