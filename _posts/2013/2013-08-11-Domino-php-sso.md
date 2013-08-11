---
layout: post
title: Domino与PHP实现SSO的初步研究
category : Web技术
tagline: "学习与实践"
tags : [SSO, Domino, PHP, tutorial]
---
{% include JB/setup %}

##前提条件
Domino服务器与php服务器属于同一个域
例如：oa.abc.com
      mis.abc.com

##服务器端获取已经Domino认证的页面上的Cookie，并设置到php的页面中
    <?php
    setcookie('DomAuthSessId','C08BB3ACD62CCBAE3CDE0D0048E2D21E',0,'');
    ?>

##验证页面中已经设置了正确的Cookie
    <?php
    echo $_COOKIE['DomAuthSessId'];
    ?>
##验证浏览器访问Domino服务器，用户正确验证

    oa.abc.com/oainterface.nsf/test?openagent
