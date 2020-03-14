---
title: Mac OS X 终端切换root用户
tags:
  - 工具
  - 技术
date: 2018-03-18 08:16:00
categories: 教程
---

mac 打开终端默认是当前登录用户，若要切换到 root 用户，使用命令：

第一种：(1)输入  sudo -i 或者 su - 或着 su - root  然后回车

(2)输入密码，就可以进入 root 用户（因为我之前设置过一次 root，所以这里到底是输入当前登录用户的密码还是 root 用户的密码我也不是很清楚，看其他网友的博客不太一样，反正我输了一次当前用户密码就切换成功了，欢迎大家指正）。

(3)这种方法的终端显示形式为：usernamedeMacBook-Pro:~ root#

第二种：(1)输入 sudo su 然后回车

(2)输入密码，就可以进入 root 用户

(3)终端显示形式：sh-3.2#

⚠️：这里两种方法进入 root 用户的终端显示不同，我并不知道有什么区别，欢迎大家告知

从 root 用户进入你想登陆的普通用户的方法，这里普通用户名用 username 来举例

(1)输入  su - username  然后回车

(2)就可以进入 username 用户

(3)这种方法的终端显示形式为：usernamedeMacBook-Pro:~ username\$
