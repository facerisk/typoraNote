## 1.安装docker

docker官网，docker for mac

## 2.下载oracle镜像

docker pull wnameless/oracle-xe-11g

## 3.启动docker容器

docker run -d -p 9090:8080 -p 1521:1521 --name oracle_11g wnameless/oracle-xe-11g

![image-20201220213805879](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213805879.png)

## 4.进入docker中oracle并设置

```sql
lplmbp@bogon ~ % docker exec -it -u root oracle_11g bash    -- 使用 root 用户连接容器 oracle

root@d83bc093026a:/# sqlplus system/oracle -- 登录oracle



SQL*Plus: Release 11.2.0.2.0 Production on Sat Dec 19 17:02:03 2020



Copyright (c) 1982, 2011, Oracle. All rights reserved.





Connected to:

Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production



SQL> create user wyf identified by password;    -- 创建用户     



User created.



SQL> alter user wyf identified by password 123456;  -- 修改用户密码



User altered.

SQL> select username from dba_users;  -- 查询用户

USERNAME
------------------------------
WYF
SYS
SYSTEM
ANONYMOUS
APEX_PUBLIC_USER
APEX_040000
OUTLN
XS$NULL
FLOWS_FILES
MDSYS
CTXSYS

USERNAME
------------------------------
XDB
HR

13 rows selected.

SQL> grant create session to wyf; -- 登录权限

Grant succeeded.

SQL> grant create table,unlimited tablespace to wyf; -- 建表权限 查看表目录权限

Grant succeeded.

SQL> grant select any table,update any table,delete any table,insert any table,drop any table to wyf; --操作表权限

Grant succeeded.

SQL> grant create sequence to wyf;

Grant succeeded.

SQL> 

SQL> exit -- 退出oracle
Disconnected from Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
root@d83bc093026a:/# exit -- 退出docker
exit
lplmbp@bogon ~ % 
```

## 5.oracle管理工具 —navicat

![image-20201220211037556](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220211037556.png)



## 扩展1:破解navicat premium

### 1.原料 

Navicat premium 15.0.15

navicat-keygen-mac

### 2.破解开始

进入navicat-keygen-mac文件夹cd Downloads/navicat-keygen-mac，打开终端输入：

```
./navicat-patcher /Applications/Navicat\ Premium.app/
```

![image-20201220212900058](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220212900058.png)





1. 生成一份自签名的代码证书，并总是信任该证书。这一步非常重要, 打开 “钥匙串访问”，选择菜单栏的 钥匙串访问->证书助理->创建证书，然后证书类型选择 “代码签名”。

![image-20201220212929426](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220212929426.png)





1. 然后在证书上右键选择“显示简介”，在“使用证书”那里选择始终信任。

![image-20201220213009923](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213009923.png)




![image-20201220213043630](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213043630.png)



1. 用 codesign 对 libcc-premium.dylib （如果有的话） 和 Navicat Premium.app 重签名。

**如果你的Navicat Premium版本号高于15.0.0，你必须先签名 libcc-premium.dylib，再签名 Navicat Premium.app。**

```
codesign -f -s Navicat /Applications/Navicat\ Premium.app/Contents/Frameworks/libcc-premium.dylib
codesign -f -s Navicat /Applications/Navicat\ Premium.app/
```

1. 接下来使用 navicat-keygen 来生成 序列号 和 激活码。

```
./navicat-keygen ./RegPrivateKey.pem
```

1. 依次选择 1 15 之后你会被要求填入请求码。注意 不要关闭注册机。

![image-20201220213112888](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213112888.png)





1. **断开网络** 并打开 Navicat

![image-20201220213139152](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213139152.png)





1. 找到注册窗口，填入注册机给你的序列号。然后点击激活按钮。(一般来说在线激活肯定会失败，这时候Navicat会询问你是否手动激活，直接选吧。)
2. 在手动激活窗口你会得到一个请求码，复制它并把它粘贴到keygen里。最后别忘了连按至少两下回车结束输入。

![image-20201220213210089](/Users/lplmbp/Library/Application Support/typora-user-images/image-20201220213210089.png)





1. 如果不出意外，你会得到一个看似用Base64编码的激活码。

直接复制它，并把它粘贴到Navicat的手动激活窗口，最后点激活按钮。
如果没什么意外的话应该能成功激活。

## 扩展2：orcale授权操作

1) 采用sys or system / manager as sysdba; 连接数据库。



2) 创建普通用户peng: create user peng identified by pwd_oracle;

 删除用户, drop user peng;



3) 授予用户登录数据库的权限： grant create session to peng;



4) 授予用户操作表空间的权限：

grant unlimited tablespace to peng;

grant create tablespace to peng;

grant alter tablespace to peng;

grant drop tablespace to peng;

grant manage tablespace to peng;



5) 授予用户操作表的权限：

grant create table to peng; (包含有create index权限, alter table, drop table权限)



6) 授予用户操作视图的权限:

grant create view to peng; (包含有alter view, drop view权限)



7) 授予用户操作触发器的权限：

grant create trigger to peng; (包含有alter trigger, drop trigger权限)



8) 授予用户操作存储过程的权限：

grant create procedure to peng;(包含有alter procedure, drop procedure 和function 以及 package权限)



9) 授予用户操作序列的权限：

grant create sequence to peng; (包含有创建、修改、删除以及选择序列)



10) 授予用户回退段权限：

grant create rollback segment to peng;

grant alter rollback segment to peng;

grant drop rollback segment to peng;



11) 授予用户同义词权限：

grant create synonym to peng;(包含drop synonym权限)

grant create public synonym to peng;

grant drop public synonym to peng;



12) 授予用户关于用户的权限：

grant create user to peng;

grant alter user to peng;

grant become user to peng;

grant drop user to peng;



13) 授予用户关于角色的权限：

grant create role to peng;



14) 授予用户操作概要文件的权限

grant create profile to peng;

grant alter profile to peng;

grant drop profile to peng;



15) 允许从sys用户所拥有的数据字典表中进行选择

grant select any dictionary to peng;



