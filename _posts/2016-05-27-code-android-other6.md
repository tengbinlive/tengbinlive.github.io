---
layout: post
title:  代码重构
description: "代码重构 代码的坏味道 ."
modified: 2016-05-27
tags: [android-other , post]
image:
  feature: abstract-2.jpg
---



### 是的，你要为你的代码负责，你要为你的接口负责，让用户只能正确地使用，难以误用。作为程序员，我们应该不断写出合格的，优秀的代码，而不是为这个本就糟糕透顶的世界添加更多的数字垃圾。

-------   Scott Meyers

### 重复的代码
{% highlight html %}
设法将它们合而为一，程序会变得更好。

同一个class内的两个函数中含有重复的代码段

两个兄弟class的成员函数中含有重复的代码段

两个毫不相关的class内出现重复的代码段
{% endhighlight %}

### 过长函数
{% highlight html %}
需要以注释来说明点什么的时候，就把需要说明的东西写进一个独立函数中

，并以其用途（而非实现手法）命名。

可以对一组或甚至一行代码做这件事。

哪怕替换后的函数调用动作比函数自身还长，只要函数名称能够解释其用途就可以。

关键不在于函数的长度，而在于函数「做什么」和「如何做」之间的语义距离。
{% endhighlight %}

### 过大类
{% highlight html %}
如果想利用单一类做太多事情，其内往往就会出现太多的成员变量。

提取完成同一任务的相关变量到一个新的类

干太多事情的类，可以考虑把责任委托给其他类
{% endhighlight %}

### 过长参数列
{% highlight html %}
太长的参数列表难以理解，太多参数会造成前后不一致、不易使用，

而且你需要更多数据时，就不得不修改它。
{% endhighlight %}

### 发散式变化
{% highlight html %}
一个类受多种变化的影响

数据库新加一个字段，同时修改三个函数：Load、Insert、Update
{% endhighlight %}

### 散弹式修改
{% highlight html %}
一种变化引起多个类相应的修改
{% endhighlight %}

### 依恋情结
{% highlight html %}
一个类里的某个函数所有使用的数据和逻辑绝大部分来源其他类，需要对这个函数进
{% endhighlight %}

### 数据泥团
{% highlight html %}
总是出现在一起的数据应该有属于他们自己的对象

有些数据项，喜欢成群结队地待在一块。

那就把它们绑起来放在一个新的类里面。
{% endhighlight %}

### 基本型别偏执
{% highlight html %}
使用小对象替换基本类型
{% endhighlight %}

### switch惊悚现身
{% highlight html %}
少用switch语句。从本质上说，switch语句的问题在于重复。

减少使用 switch 使用统一的结构进行替代，

看到switch你就应该考虑使用多态来替换它

多态取代条件表达式
{% endhighlight %}

### 平行继承体系
{% highlight html %}
每当你为某个 class 增加一个 subclass，

必须也为另一个class相应增加一个subclass 是坏味道
{% endhighlight %}

### 冗赘类
{% highlight html %}
你所创建的每一个类，都得有人去理解它、维护它 ,

如果一个类的所得不值其身价，它就应该消失。
{% endhighlight %}

### 夸夸其谈未来性
{% highlight html %}
不要为未来考虑太多
{% endhighlight %}

### 令人迷惑的暂时值域
{% highlight html %}
instance 的变量仅为某种特定情势而设，

需要为这些和这个临时变量相关的代码放到一个新的地方
{% endhighlight %}

### 过度耦合的消息链
{% highlight html %}
有时你会看到两个类过于亲密，花费太多时间去探究彼此的private成分。

过分狎昵的类必须拆散 .
{% endhighlight %}

### 中间转手人
{% highlight html %}
某个class接口有一半的函数都委托给其他class 是坏味道

Inappropriate Intimacy（狎昵关系）

两个 class 联系过于紧密，可以将他们拆散，

或者提取共有部分放到新的 class
{% endhighlight %}

### 异曲同工的类
{% highlight html %}
如果两个函数做同一件事情，却有着不同的签名式 ,

删除一个，保留一个 .
{% endhighlight %}

### 不完美的程序库类
{% highlight html %}
复用可能导致过去设计 ,

库的设计有时会不够好，不那么容易使用，可能还会有那么一点小缺陷。
{% endhighlight %}

### 纯数据类
{% highlight html %}
只拥有一些值域（fields），以及用于访问（读写〕这些值域的函数是坏味道
{% endhighlight %}

### 被拒绝的遗贈
{% highlight html %}
Subclasses 应该继承superclasses的函数和数据
{% endhighlight %}

### 过多的注释
{% highlight html %}
当你感觉需要撰写注释，请先尝试重构，试着让所有注释都变得多余
{% endhighlight %}

