---
layout: post
title:  Source Tree Pull 密码错误
description: "Source Tree Pull 密码错误 ."
modified: 2016-05-09
tags: [android-other , post]
image:
  feature: abstract-7.jpg
---


## 在设置了正确账号密码时,出现pull一直提示密码错误,可能是URL是错误

### 可尝试在项目路径中添加账号信息

路径在该项目信息设置中

#### 直接从github copy 的 path
{% highlight html %}
https://github.com/tengbinlive/aibao_demo.git
{% endhighlight %}

#### 修改为
{% highlight html %}
https://tengbinlive@github.com/tengbinlive/aibao_demo.git
{% endhighlight %}



