---
layout : post
title : Ubuntu Server上的文件管理
category : Web技术
tagline : "学习与实践"
tags : [Ubuntu]
---
{% include JB/setup %}

应用部署到Ubuntu Server上之后，需要对服务器上的文件进行管理，这里我使用SFTP方式进行连接，客户端软件使用Mac下的Transmit。

由于我的AWS服务已经配置使用Key登录，因此使用Transmit建立连接非常简单，设置IP,选择Key证书后连接就可以了。当然如何在服务器上创建其他用户并限制目录访问权限，需要以后有时间再行测试了。



如果使用用户名口令方式来登录，可以参考以下文章进行设置：
-----------

在Ubuntu中配置sftp服务,并创建用户同时分配权限

	1、首先修改sshd的配置文件： 
        $ sudo nano /etc/ssh/sshd_config 

    2、将该文件的末尾修改如下：
            #Subsystem sftp /usr/lib/openssh/sftp-server   #该行注释掉
            Subsystem sftp internal-sftp 
            #UsePAM yes    #该行同样注释掉，或者移到Subsystem sftp internal-sftp的上面
            Match Group sftp-users   #匹配sftp组，如为单个用户可用：Match User test;  
                     ChrootDirectory /home/joomlaadmin
                     X11Forwarding no
                     AllowTcpForwarding no
                     ForceCommand internal-sftp
					#ChrootDirectory：指定用户被锁定到的目录，为了能够chroot成功，该目录必须属主是root，并且其他用户或组不能写
	3、
		sudo addgroup sftp-users
		sudo adduser joomlaadmin
		sudo usermod -G sftp-users -s /bin/false joomlaadmin

	4、
		sudo chown root /home/joomlaadmin
		sudo chmod 755 /home/joomlaadmin/
		sudo /etc/init.d/ssh reload
	5、
		sudo mkdir uploads
		sudo chown joomlaadmin:sftp-users /home/joomlaadmin/uploads
		sudo chown joomlaadmin:sftp-users /home/joomlaadmin  #执行此行后，joomlaadmin目录由不可写变为可写




* http://blog.csdn.net/marujunyy/article/details/8502289
* http://yhf8377.blog.163.com/blog/static/176860177201210217219800/
* http://it.livekn.com/2013/04/chrooted-sftp.html

