title: ' Linux使用ssh的简单记录'
author: Walker
tags:
  - Linux
  - SSH
categories:
  - csdn
date: 2017-08-09 00:24:00
---
最近在看unp，当然也写代码。为了方便，直接让一台linux通过ssh控制另外一台linux，包括传送文件，所以这里记录下ssh登录和传送文件的命令。目前linux都是默认安装sshd的了，一般都可以直接使用下面的命令。
对于服务器端，只需要使用以下命令开启ssh服务：
```
service sshd restart
```
对于客户端，可以通过以下命令连接服务器：
```
ssh ipaddr -l username
```
其中ipaddr是服务器的地址，username是登录的用户名，按下Enter键后会提示输入密码。
通过下面的命令向服务器发送文件：
```
scp filename username@ipaddr:remotedir
scp -r dirname username@ipaddr:remotedir
```
第一个命令是发送文件，第二个命令是发送整个目录，username和ipaddr含义同上。remotedir是服务器端存放传送数据的目录，默认以对应用户的home目录为根目录，注意不能以“/”开头。发送文件也是需要输入密码的。此外，不能给username不能是root，只能是普通用户，即在/home目录下存在相应的用户文件夹。
只是简单的记录，所以内容比较简单。

来自我的csdn博客:[http://blog.csdn.net/u014209688/article/details/72355174](http://blog.csdn.net/u014209688/article/details/72355174)