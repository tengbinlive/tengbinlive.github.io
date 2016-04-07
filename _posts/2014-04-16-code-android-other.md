---
layout: post
title: 源码下编译 xhdpi 等文件进apk
description: "源码下编译 xhdpi 等文件进apk."
modified: 2014-04-17
tags: [android-other , post]
image:
  feature: abstract-3.jpg
---

当在源码下编译 生成apk ，
  
在编译正常 运行apk错误时 有可能是 源码下配置生成apk时未讲需要的xhdpi等文件编辑进去
  
#### 需要修改

  1. 进入build 目录 将buildspec.mk.default 文件复制一份到 工程bin目录下
  
  2. 修改其中 
  
  {% highlight html %}
  ifndef CUSTOM_LOCALES
  
  #CUSTOM_LOCALES:=
  
  endif
  {% endhighlight %}
  
  为
  
  {% highlight html %}
  ifndef CUSTOM_LOCALES
  
  CUSTOM_LOCALES:=
  mdpi ldpi hdpi xhdpi
  endif
  {% endhighlight %}

#### CUSTOM_LOCALES:=｛mdpi ldpi hdpi xhdpi｝ ｛｝中为需要编译进apk 的目录





