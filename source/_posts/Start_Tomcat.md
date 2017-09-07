---
layout: post
title:  Mac下启动Tomcat
date:   2017-01-23 15:11:08
comments: true
tags: 
	- Tomcat
---


#### 一、安装Java
官网下载jdk安装
地址：[http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

#### 二、下载启动Tomcat
1.下载Tomcat，地址：[http://tomcat.apache.org/download-80.cgi](http://tomcat.apache.org/download-80.cgi)
mac下载zip和tar.gz都行，我下载的是zip
![](/assets/blogImg/tomcat_download.png)
<!--more-->

2.解压缩之后直接拷贝到资源库中，为方便管理解压后文件夹名称为Tomcat，具体位置如下:
![](/assets/blogImg/tomcat_instail.png)

打开终端，输入以下命令
```bash
$ sudo sh /Library/Tomcat/bin/startup.sh
```
浏览器中输入localhost:8080，就可以看到一下效果:
![](/assets/blogImg/tomcat_start.png)

#### 三、安装过程中遇到的问题
> 1.执行启动命令时提示No such file or directory错误

需要执行以下命令赋予权限：
```bash
$ sudo chmod 755 /Library/Tomcat/bin/*.sh
```
> 2.执行启动命令时提示JAVA_HOME或JRE_HOME错误

修改用户全局变量：
打开用户根目录下的.bash_profile文件
![](/assets/blogImg/tomcar_user.png)
添加如下两行，如图
```bash
export JAVA_HOME=`/usr/libexec/java_home`
export JRE_HOME=$JAVA_HOME/jre
```
![](/assets/blogImg/tomcat_edit_bash_profile.png)
更新配置的环境变量：
```bash
$ source .bash_profile
```

也可以修改Tomcat/bin/setclasspath.sh环境变量 
![](/assets/blogImg/tomcat_setclasspath.png)















