---
layout: post
title:  Android Studio 升级错误
description: "Re-download dependencies and sync project (requires network)"
modified: 2017-10-27
tags: [android-other , post]
image:
  feature: abstract-7.jpg
---



###  android studio 升级后同步时报错
{% highlight html %}
Re-download dependencies and sync project (requires network)
The state of a Gradle build process (daemon) may be corrupt. Stopping all Gradle daemons may solve this problem
{% endhighlight %}

#### 前往gradle系统目标 ".gradle\wrapper\dists" , 删除同步项目中gradle/wrapper/gradle-wrapper.properties对应版本,如:"gradle-4.1-all"

#### 重启android studio 