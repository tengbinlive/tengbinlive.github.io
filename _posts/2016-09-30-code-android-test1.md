---
layout: post
title: Monkey Test
description: "Monkey Test 命令"
modified: 2016-09-30
tags: [android-test , post]
image:
  feature: abstract-11.jpg
---



### monkey test

{% highlight html %}
adb shell monkey -p com.binteng --throttle 200
 --pct-syskeys 2 --ignore-crashes 100000000
{% endhighlight %}

