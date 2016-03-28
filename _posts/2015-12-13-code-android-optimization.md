---
layout: post
title: Android Optimization
description: "优化相关."
modified: 2015-12-13
tags: [android-optimization , post]
image:
  feature: abstract-11.jpg
---

1. 使用手机自带 （开发人员选项->调试GPU 过度绘制）界面过度绘制 （优化layout排列&层级）

2. 使用Android Device Monitor -> Hierarchy View （优化layout 层级）

3. lint：（优化app 无用资源 & android 官方提供意见）

{% highlight html %}
    run:
        gradle project -> tasks -> verification -> lint
{% endhighlight %}

#### 配置：

{% highlight html %}
    apply plugin: 'com.droidtitan.lintcleaner'
    lintOptions{
        abortOnError false
    }
{% endhighlight %}

{% highlight html %}
    lintCleaner {
     // Exclude specific files
      exclude = ['com_crashlytics_export_strings.xml','config.xml']

     // Ability to ignore all resource files. False by default.
       ignoreResFiles = true

     // Default path is build/outputs/lint-results.xml
       lintXmlFilePath = 'path/to/lint-results.xml'
    }
{% endhighlight %}

#### 使用浏览器查看

{% highlight html %}
    build/outputs/lint-results.html
{% endhighlight %}


