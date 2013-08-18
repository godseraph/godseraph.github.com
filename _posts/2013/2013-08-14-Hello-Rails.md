---
layout: post
title: Ubuntu 12.04 Server LTS安装部署Nginx+MySQL+Ruby1.9.3+Rails3.2 
category : Web技术
tagline: "学习与实践"
tags : [ROR, Nginx, Ubuntu]
---
{% include JB/setup %}

##1、准备工作:

//更新源

    $sudo apt-get update
    $sudo apt-get upgrade

//矫正时区

    $sudo dpkg-reconfigure tzdata
    选择Asia,然后选择shanghai。

##2、安装所需的linux包:

    $sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev  libxml2-dev libxslt-dev autoconf libc6-dev zlib1g-dev libssl-dev build-essential curl git-core libc6-dev g++ gcc


##3、为Rails添加用户和组:

    $sudo addgroup passenger			
    $sudo adduser godseraph			//已有此用户，则此步省略
    $sudo usermod -G passenger,www-data,sudo godseraph
    $su - godseraph

##4、安装Ruby1.9.3:

    $bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)     //安装rvm控制ruby的版本
    $source .bashrc      //首次需要加载rvm
    $rvm –v             //查看rvm的版本
    $sudo vi ~/.bashrc  //打开bashrc文件，添加以下代码：
        [[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" 
    $source ～/.bashrc  //打开新终端运行bashrc
    $rvm install 1.9.3  //安装ruby,1.9.3为ruby的版本
    $rvm use 1.9.3 default  //设置1.9.3为默认的版本
    $ruby –v                //查看当前ruby的版本

##5、安装rubygems,Rails3.2
//安装libssl支持

    $sudo apt-get install openssl libssl-dev 
    $sudo apt-get install libopenssl-ruby1.9.1 

//安装rubygems

    $rvm rubygems current		//Installing rubygems-2.0.6 for ruby-1.9.3-p448
    $gem install rails   		//安装rails最新版 
    $gem install rails --version 3.2.14	//安装rails 3.2.14版
    $rails -v   			//查看已安装rails版本,我的是rails 3.2.





参考资料：
http://blog.sina.com.cn/s/blog_5d239b7f01019km9.html
http://blog.it580.com/install-ruby-on-rails-on-ubuntu-12-04-1-lts
http://ruby-china.org/wiki/install-rails-on-ubuntu-12-04-server


