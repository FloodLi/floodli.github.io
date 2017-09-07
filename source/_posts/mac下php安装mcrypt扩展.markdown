---
layout: post
title:  mac下php安装mcrypt扩展
date:   2016-11-25 09:45:11
comments: true
tags: 
	- PHP
---

# MCrypt是一个功能强大的加密算法扩展库，它包括有22种算法。

##### 1：下载并解压mcrypt-2.6.8.tar.bz2。（2.6.8为版本号，可以自行选择，但是注意后边步骤要与下载的版本号一致。）

##### 2：在终端执行命令（注意如下命令需要安装xcode支持）：

```
cd ~/Downloads/mcrypt-2.5.8
./configure --disable-posix-threads --enable-static
make
sudo make install
```

或者使用homebrew安装

```
brew install mcrypt
```

<!--more-->

##### 3：下载并解压php源码，根据自己情况选择对应版本。(注意以下命令中php的版本)
在终端执行命令：（如果出错请看后边）

```
cd ~/Downloads/php-5.5.14/ext/mcrypt
phpize
./configure
make
cd modules
sudo cp mcrypt.so /usr/lib/php/extensions/no-debug-non-zts-20121212/
```
（cd modules后当出现
```
Build complete.
Don't forget to run 'make test'.
```
表示安装成功。）

##### 4：打开php.ini

```
sudo vi /etc/php.ini
```
添加如下代码：（注意no-debug-non-zts-20121212版本号，如果不清楚可以前往/usr/lib/php/extensions/查看）

```
extension=/usr/lib/php/extensions/no-debug-non-zts-20121212/mcrypt.so
```
\*如果phpize出现如下错误：

```
grep: /usr/include/php/main/php.h: No such file or directory
grep: /usr/include/php/Zend/zend_modules.h: No such file or directory
grep: /usr/include/php/Zend/zend_extensions.h: No such file or directory
Configuring for:
PHP Api Version:
Zend Module Api No:
Zend Extension Api No:
Cannot find autoconf. Please check your autoconf installation and the
$PHP_AUTOCONF environment variable. Then, rerun this script.
```

##### 表示需要安装autoconf

\*如果make出现如下错误：

```
/ext/mcrypt/mcrypt.c:25:10: fatal error: 'php.h' file not found
```
执行如下命令即可：

```
sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include /usr/include
```

##### \*注意MacOSX10.10.sdk修改为自己系统的版本号