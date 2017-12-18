---
title: 用Docker快速搭建Mysql多实例服务，并进行数据卷分离
permalink: 'docker-quickly-build-mysql-multi-instance-service,-and-data-volume-separation'
tags:
  - Docker
date: 2017-10-27 12:34:17
---

> 在centos 里面编译安装MySQL多实例，编译时间太长，配置多实例也费尽，如果不是专门学习MySQL，而只是使用MySQL服务，使用docker 一条命令瞬间完成一个多实例，方便快捷，而且数据卷分离可以在docker容器外保存数据。
运行：
docker run -d --name myMysql2 -v ~/data/mysql2:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3308:3306 mysql
你就可以本机ip+3308端口访问MySQL，数据把存在本机指定的目录，本例为 ~/data/mysql2，root密码为123456

<!--more-->

## 1  安装[docker](https://www.docker.com/)
**mac 和 win**

去 安装[docker官网](https://www.docker.com/) 下载对应安装包安装

**Ubuntu**
```
$sudo wget -qO- https://get/docker.com/ | sh
$sudo usermod -aG docker current_username
```
>#current_username是你当前的用户名，这样以后就可以免sudo  运行docker 命令了

或者参考这里[Docker入门](http://www.imooc.com/learn/867)

## 2  获取mysql镜像

从docker hub的仓库中拉取mysql镜像

`docker pull mysql`

查看镜像

```
docker images

mysql latest 18f13d72f7f0 2 weeks ago 383.4 MB
```

## 3  运行mysql容器

** 3.1 运行第一个mysql实例的命令如下：**


`docker run -d --name myMysql -v ~/data/mysql1:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3307:3306 mysql`


> -d : --detach，后台运行。
--name : 为你的镜像创建一个别名，该别名用于更好操作。
-p : 映射端口，一般我们会将默认端口进行更改，避免与本机的mysql端口冲突，如果你宿主机有mysql，请更改端口，如 -p 3307:3306。  3307代表本地端口  3306为容器端口这是固定的（固定在MySQL官方镜像里），
-e : 环境变量。为mysql的root用户设置密码为123456。
-v : 指定数据卷，意思就是将mysql容器中的/var/lib/mysql（这个是数据库所有数据信息文件）映射到宿主机~/data/mysql里面。



** 3.2 运行第二个mysql实例的命令如下：**

*只需要与第一个容器的的 --name 以及 本机数据目录, 映射的本机端口这3者不同即可*

`docker run -d --name myMysql2 -v ~/data/mysql2:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3308:3306 mysql`


**在本机登陆到第一个实例**

```
mysql -h 127.0.0.1 -P 3307 -u root -p

or

mysql -h 192.168.0.116 -P 3307 -u root -p
```

**在本机登陆到第二个实例**

```
mysql -h 127.0.0.1 -P 3308 -u root -p

or

mysql -h 192.168.0.116 -P 3308 -u root -p
```

**一定要指定 `ip` 参数，不可以省略 否则报错，连接失败**

```
mysql -uroot -p -P3307
Enter password:
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```

**删除容器，看数据卷是否还在**

```
docker stop myMysql
docker rm myMysql

docker stop myMysql2
docker rm myMysql2`
```

依然还在，这说明如果我们创建新的mysql容器，那么只需要指定数据卷就可以了。


**进入到myMysql容器中**

`docker exec -t -i myMysql /bin/bash`

###登录到myMysql容器中， 在容器内登录到mysql服务器中

`mysql -uroot -p`

>由于MySQL 5.7版本以后的mysql数据库下已经没有password这个字段了，password字段改成了authentication_string，查询时使用authentication_string字段即可

增加用户，授予权限
`grant all on *.* to 'test'@'%' identified by '1234';`

>这时一条授予权限命令，当用户不存在时，则会自动创建。
. 前一个*星号代表所有数据库，后一个星号代表所有数据表
'test"@'% : test是用户名，%为所有IP。
identified by '1234' : 密码设置为1234。



参考：
 - [使用Docker快速搭建Mysql，并进行数据卷分离](http://www.jianshu.com/p/57420240e877)
 - [使用docker运行mysql实例](http://www.jianshu.com/p/c24e3e5f5b58)
 - [MySQL 5.7.19 编译安装与配置](http://www.jianshu.com/p/4416792750c7)
