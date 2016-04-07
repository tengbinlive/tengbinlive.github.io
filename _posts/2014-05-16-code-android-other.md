---
layout: post
title: 源码下编译 apk 导入三方jar
description: "源码下编译 apk 导入三方jar."
modified: 2014-05-16
tags: [android-other , post]
image:
  feature: abstract-3.jpg
---

#### 需要注意的两点：

Android.mk文件中

{% highlight html %}
LOCAL_STATIC_JAVA_LIBRARIES := libjsoup libokhttp libksoap2 

(定义各个jar 在mk文件中的 变量名 空格分隔)
{% endhighlight %}

#### 导入jar (每个jar 需要用 空格加\ 分隔“ \”)

{% highlight html %}
include $(CLEAR_VARS)

LOCAL_PREBUILT_STATIC_JAVA_LIBRARIES :=libjsoup:libs/jsoup.jar \
libksoap2:libs/ksoap2.jar  \
libokhttp:libs/okhttp.jar \

include $(BUILD_MULTI_PREBUILT)
(libs/xxxx.jar 为路径)
{% endhighlight %}




