---
layout: post
title: Android Bug
description: "bug 记录 - 1."
modified: 2016-04-14
tags: [android-bug , post]
image:
  feature: abstract-4.jpg
---

### .png或.9.png 文件问题 ，可能.9.png放置位置不对(比如放在了mipmap中)，或是PNG文件保存时格式错误(直接将.jpg改后缀为.png有时也会出问题)等
{% highlight html %}
1. AAPT err(Facade for 558739077): libpng error: Not a PNG file

2. Error:Execution failed for task ':app:mergeDebugResources'.
   > Crunching Cruncher top_bg.9.png failed, see logs
   
3. Error: Invalid file name: must contain only lowercase letters and digits ([a-z0-9_.])
{% endhighlight %}

{% highlight html %}
//关闭Android Studio的PNG合法性检查的
 defaultConfig {
        aaptOptions.cruncherEnabled = false
        aaptOptions.useNewCruncher = false
  }
{% endhighlight %}
