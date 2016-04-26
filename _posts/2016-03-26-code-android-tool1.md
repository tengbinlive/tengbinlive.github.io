---
layout: post
title: 使用ProGuard查看混淆后日志
description: "还原混淆后的log方法."
modified: 2016-03-26
tags: [android-tool , post]
image:
  feature: abstract-8.jpg
---

#### sdk/tools/proguard/bin 目录下有个retrace.bat工具可以将混淆后的报错堆栈解码成正常的类名

#### 使用方法如下:

将你的报错堆栈保存到文件中，如obfuscated_trace.txt

拿到版本发布时生成的mapping.txt

执行命令
{% highlight html %}
retrace.bat -verbose mapping.txt obfuscated_trace.txt
{% endhighlight %}

#### ProGuard 提供了命令行和 GUI 工具来还原混淆后的代码。

该工具位于  <android-sdk>/tools/proguard/bin/ 目录下。

里面的 proguardgui.bat 为 GUI 工具，

0. 运行 proguardgui.bat

1. 从左边的菜单选择  “ReTrace”

2. 在上面的 mapping 文件中选择你的 mapping 文件 ，在下面输入框输入要还原的代码

3. 点击 “ReTrace!” 

retrace.bat 为命令行工具， 把 mapping 文件和 要还原的堆栈信息保存在 stacktrace 文件中，

然后把这两个文件复制到 retrace.bat 目录下，运行如下命令即可。
{% highlight html %}
retrace.bat -verbose mapping.txt stacktrace.txt > out.txt
{% endhighlight %}




