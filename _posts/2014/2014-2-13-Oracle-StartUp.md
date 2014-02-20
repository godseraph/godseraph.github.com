---
layout : post
title : Oracle 10G实践
category : Web技术
tagline : "学习与实践"
tags : [Oracle]
---
{% include JB/setup %}


1.安装32位Windows2003虚拟机
2.下载32位Oracle10G安装包和10.2.0.5补丁包
3.使用默认设置运行安装包和补丁包
4.补丁包安装后需要运行升级程序，否则数据库实例无法运行。


  C:\>set ORACLE_HOME=c:\oracle\product\10.2.0\db_1
  C:\>set ORACLE_SID=sbzxgz
  C:\>sqlplus / as sysdba
  SQL> startup upgrade
  SQL> SPOOL patch.log
  SQL> @?/rdbms/admin/catupgrd.sql
  SQL> SPOOL OFF
  SQL> shutdown immediate
  SQL> startup

5.使用PL/SQL远程连接oracle数据库出现oracle ORA-12526: TNS: 监听程序: 所有适用例程都处于受限模式。

  (查了下原来之前改字符集时执行了：ALTER SYSTEM ENABLE RESTRICTED SESSION；)

解决办法：使用系统管理员身份运行以下一段代码

  SQL> ALTER SYSTEM DISABLE RESTRICTED SESSION;


6.创建用户表空间、创建用户、分配权限
7.创建表、填充测试数据
8.在应用服务器上安装Oracle Data Access Components 10.2.0.2.21
