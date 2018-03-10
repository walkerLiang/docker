title: Linux下hexo的搭建
tags:
  - hexo
categories: []
author: Walker
date: 2017-08-06 15:52:00
---
hexo的搭建还是比较简单的，主要是安装git、node.js、hexo就行了，后面再介绍下主题的修改和编辑器的添加。
#### 基本
Linux下一般都是自带git，所以这里不再介绍git的安装。
对于node.js，貌似是不支持直接使用命令行安装的，只能下载安装包再解压安装。如果你能够用浏览器访问的话，可以上官网[https://nodejs.org/en/download/](https://nodejs.org/en/download/)下载，像我实在服务器上搭建的话，就只能用命令下载了:
```
wget https://nodejs.org/dist/v6.11.2/node-v6.11.2-linux-x64.tar.xz --no-check-certificate
```
使用上面的命令就可以下载版本6.11.2的安装包，注意dist/后面的一串数字也是和版本相关的。下载完成后解压缩文件到某个目录例如src_dir，然后使用下面的命令设置软链接。
```
ln -s src_dir/bin/npm /usr/local/bin
ln -s src_dir/bin/node /usr/local/bin
```
这样子就可以直接使用npm命令安装hexo了，使用命令如下：
```
npm install -g hexo-cli
ln -s src_dir/bin/hexo /usr/local/bin
```
第二个命令也是用来设置hexo的软链接的，npm命令似乎是会自动定位到node.js的安装目录，并将hexo安装到同一目录下。至此，我们的hexo算是安装完成了，但也只是命令的使用而已，接下来我们将介绍如何搭建自己的个人博客。
#### 博客搭建
首先我们进入到任意目录下，依次执行下面的命令：
```
hexo init blog
cd blog/
hexo server 
```
第一个命令会创建一个blog的目录并存放需要的文件，如配置文件、主题文件、markdown文件等，目前对于整个目录结构还不熟，所以这里不介绍了。
而第三个命令则是运行我们的服务器了，运行该命令后，便可以通过网页访问我们的博客了，根据命令输出的链接访问即可，访问链接类似 x.x.x.x:4000，其中x.x.x.x为IP地址，如果是本地的话也可以替换为localhost。可以看到博客的页面类似如下：
![myblog](http://oudii2u1j.bkt.clouddn.com/blog.png)

默认会有一片介绍hexo使用的简单文档，创建新博客也是很简单，只要使用下面的命令：
```
hexo new myblog
```
可以看到blog目录下的source/_posts目录下多出了一个myblog.md文件，这便是保存新博客内容的markdown文件，似乎hexo是默认用markdown来保存博客的。我们可以直接用相应的软件比如马克飞象来编辑文件后保存在_posts目录下然后刷新页面就可以看到效果了。

此外，需要注意的是hexo似乎是默认没有编辑功能的，查找了一番之后找到了hexo-admin插件，似乎就可以实现博客编辑和同步查看效果功能，接下来简单介绍下这个插件的使用。

#### hexo-admin插件
给hexo安装插件也是非常简单的：
```
npm instal -save hexo-admin
```
就算是安装完成了，只要通过x.x.x.x:4000/admin就可以访问编辑页面，页面大概如下：
![](http://oudii2u1j.bkt.clouddn.com/blog/hexo-admin.png)
提供编辑和新建操作，没有提供删除操作。默认情况下这个页面是不需要权限的，设置权限可以按照页面上Settings部分的操作将设置后得到的内容保存在blog目录下的_config.yml文件中在重启服务器即可，此后进入该页面就需要输入用户名和密码了。

至此，我们的博客就算搭建完成了，但对于博客的在线编辑体验还是没有那么好，后期打算自己调整hexo-admin看下能否直接嵌入到博客页面中。