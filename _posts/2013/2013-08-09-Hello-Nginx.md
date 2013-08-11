---
layout: post
title: 使用Nginx搭建流媒体服务器
category : Web技术
tagline: "学习与实践"
tags : [流媒体, Nginx, Ubuntu, tutorial]
---
{% include JB/setup %}

##使用官方PPA安装 Nginx 最新版本，使用以下命令：

    sudo add-apt-repository ppa:nginx/stable
    sudo apt-get update
    sudo apt-get install nginx

    安装pcre
    sudo apt-get install libpcre3 libpcre3-dev


所有的配置文件都在/etc/nginx下，并且每个虚拟主机已经安排在了×/etc/nginx/sites-available下×,其中的default文件是虚拟主机的配置文件
默认的虚拟主机的目录设置在了×/usr/share/nginx/html×
程序文件在/usr/sbin/nginx 
日志放在了/var/log/nginx中 
并已经在/etc/init.d/下创建了启动脚本nginx 
Nginx相关控制命令：

    启动 Nginx：
        sudo /etc/init.d/nginx start

    浏览器浏览运行情况输入：http://localhost ;如果现实”Welcome to nginx!”，表明你的 Nginx 服务器安装成功！
    关闭 Nginx：sudo /etc/init.d/nginx stop;
    重启 nginx：sudo /etc/init.d/nginx restart;

##Permission denied 问题的解决办法
    修改目录所有者为www-data即可。
    chown -R www-data:www-data proxy_temp




