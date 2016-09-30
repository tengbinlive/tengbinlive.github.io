---
layout: post
title: Jenkins Gradle Build Tag Git Android
description: "jenkins 集成git获取 android项目 使用gradle编译"
modified: 2016-09-07
tags: [android-other , post]
image:
  feature: abstract-11.jpg
---



### 关于Jenkins安装 以及Gradle Git 插件,可google

### 配置gradle编译Android项目,代码重git 最后一个tag获取

#### 配置代码获取

1.选择git

2.Repositories -> Repository URL(http://../xx.git git路径)

3.Repositories -> Credentials git clone 验证账号密码

4.高级 -> Refspec 配置获取tags
{% highlight html %}
+refs/tags/*:refs/remotes/origin/tags/*
{% endhighlight %}

5.Branches to build -> Branch Specifier (blank for 'any') 配置获取最后一个tag
{% highlight html %}
*/tags/*
{% endhighlight %}

<figure>
<a href="/images/jenkins_0.png"><img src="/images/jenkins_0.png" alt=""></a>
</figure>

### 配置构建

#### 添加构建步骤 invoke gradle script

1.勾选 Use Gradle Wrapper

2.勾选 Use Gradle Wrapper -> From Root Build Script Dir

3.添加gradle 命令 Tasks (可在Android Studio 编译运行项目时 messages中查看)
{% highlight html %}
:app:assembleProdDebug
{% endhighlight %}

4.添加 Use Gradle Wrapper -> Root Build script
{% highlight html %}
${workspace}
{% endhighlight %}

<figure>
<a href="/images/jenkins_1.png"><img src="/images/jenkins_1.png" alt=""></a>
</figure>
