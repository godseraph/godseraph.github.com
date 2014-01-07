---
layout : post
title : Domino5.08开发中容易忽视的特性
category : Web技术
tagline : "学习与实践"
tags : [Domino5]
---
{% include JB/setup %}


在开发一个Domino表单时，将访问权限授予admin角色用户，正常情况下在未登录时，应该每次访问此页都跳转到登录页面。但实际测试时发现登录一次后，即使关闭了浏览器再访问，也能直接打开该页面，很明显浏览器做了缓存。在表单头信息中加入以下禁止缓存的标记也不起作用。
	<meta http-equiv=\"Content-Type\" content=\"text/html; charset=gb2312\">
	<meta HTTP-EQUIV=\"pragma\" CONTENT=\"no-cache\">
	<meta HTTP-EQUIV=\"Cache-Control\" CONTENT=\"no-cache,must-revalidate\">
	<meta HTTP-EQUIV=\"Expires\"   CONTENT=\"0\">

解决此问题，可以在form表单中加入动态计算的域，这样，domino就不会标记该form未更改，浏览器也不会缓存该页面了。