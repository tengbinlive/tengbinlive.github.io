---
layout: post
title:  can't bind to local 8600 for debugger
description: "can't bind to local 8600 for debugger"
modified: 2016-06-04
tags: [android-other , post]
image:
  feature: abstract-7.jpg
---



##  尝试以下方式

####  1.fuser -k 8600/tcp

####  2.重启adb
{% highlight html %}
./adb kill-server
./adb start-server
{% endhighlight %}

####  3.android 开发出现无法连接 debugger时
可以尝试在 host 文件中 添加:
{% highlight html %}
127.0.0.1 localhost
{% endhighlight %}

#####  Windows
{% highlight html %}
0. hosts 位于 Windows 系统 %windir%\system32\drivers\etc\hosts（一般情况下：%windir% - > C:\WINDOWS）

1. 以记事本的方式打开hosts，添加以下文档中的地址并保存就可以了，注意hosts文件没有后缀

2. 刷新dns , 开始 -> 运行 -> 输入cmd -> 在CMD窗口输入 ipconfig /flushdns
{% endhighlight %}

#####  linux
{% highlight html %}
0. hosts 位于 linux 系统 /etc/hosts

1. 可用Notepad++ 等编辑器转换文本编码和换行符格式

2. 终端输入 sudo rcnscd restart

   对于systemd发行版，请使用命令 sudo systemctl restart NetworkManager
{% endhighlight %}

#####  Mac
{% highlight html %}
0. 打开文件管理器（也就是Finder）按快捷键组合“Shift+Command+G”三个组合按键查找文件，
   并输入Hosts文件的所在路径：/etc/hosts

1. 可用Notepad++ 等编辑器转换文本编码和换行符格式

2. 终端输入 sudo killall -HUP mDNSResponder
{% endhighlight %}




