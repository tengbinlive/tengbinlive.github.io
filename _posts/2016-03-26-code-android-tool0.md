---
layout: post
title: find bugs 静态检查工具
description: "FindBugs 是一个静态分析工具."
modified: 2016-03-26
tags: [android-tool , post]
image:
  feature: abstract-8.jpg
---

## [find bugs 静态检查工具](http://baike.baidu.com/view/2367937.htm)

FindBugs 是一个静态分析工具，它检查类或者 JAR 文件，

将字节码与一组缺陷模式进行对比以发现可能的问题。

有了静态分析工具，就可以在不实际运行程序的情况对软件进行分析.


### 静态代码分析工具的优势

0. 帮助程序开发人员自动执行静态代码分析，快速定位代码隐藏错误和缺陷。

1. 帮助代码设计人员更专注于分析和解决代码设计缺陷。

2. 显著减少在代码逐行检查上花费的时间，提高软件可靠性并节省软件开发和测试成本。


### Bug分类

0. Bad practice 坏的实践

1. Correctness 一般的正确性问题

2. Internationalization 国际化

3. Malicious code vulnerability 可能受到的恶意攻击

4. Multithreaded correctness 多线程的正确性

5. Performance 性能问题

6. Dodgy 危险的 


#### 可能导致错误的代码：

NP： 空指针被引用；在方法的异常路径里，空指针被引用；方法没有检查参数是否null；null值产生并被引用；null值产生并在方法的异常路径被引用；传给方法一个声明为@NonNull的null参数；方法的返回值声明为@NonNull实际是null。

Nm： 类定义了hashcode()方法，但实际上并未覆盖父类Object的hashCode()；类定义了tostring()方法，但实际上并未覆盖父类Object的toString()；很明显的方法和构造器混淆；方法名容易混淆。

SQL：方法尝试访问一个Prepared Statement的0索引；方法尝试访问一个ResultSet的0索引。

UwF：所有的write都把属性置成null，这样所有的读取都是null，这样这个属性是否有必要存在；或属性从没有被write。


#### Internationalization 国际化

当对字符串使用upper或lowercase方法，如果是国际的字符串，可能会不恰当的转换。

Malicious code vulnerability 可能受到的恶意攻击


#### 如果代码公开，可能受到恶意攻击的代码：

FI： 一个类的finalize()应该是protected，而不是public的。

MS：属性是可变的数组；属性是可变的Hashtable；属性应该是package protected的。

Multithreaded correctness 多线程的正确性


#### 多线程编程时，可能导致错误的代码：

ESync：空的同步块，很难被正确使用。

MWN：错误使用notify()，可能导致IllegalMonitorStateException异常；或错误的使用wait()。

No： 使用notify()而不是notifyAll()，只是唤醒一个线程而不是所有等待的线程。

SC： 构造器调用了Thread.start()，当该类被继承可能会导致错误。


#### Performance 性能问题 可能导致性能不佳的代码：

DM：方法调用了低效的Boolean的构造器，而应该用Boolean.valueOf(…)；用类似

Integer.toString(1) 代替new Integer(1).toString()；方法调用了低效的float的构造器，应该用静态的valueOf方法。

SIC：如果一个内部类想在更广泛的地方被引用，它应该声明为static。

SS： 如果一个实例属性不被读取，考虑声明为static。

UrF：如果一个属性从没有被read，考虑从类中去掉。

UuF：如果一个属性从没有被使用，考虑从类中去掉。


#### Dodgy 危险的 具有潜在危险的代码，可能运行期产生错误：

CI： 类声明为final但声明了protected的属性。

DLS：对一个本地变量赋值，但却没有读取该本地变量；本地变量赋值成null，却没有读取该本地变量。

ICAST： 整型数字相乘结果转化为长整型数字，应该将整型先转化为长整型数字再相乘。

INT：没必要的整型数字比较，如X <= Integer.MAX_VALUE。

NP： 对readline()的直接引用，而没有判断是否null；对方法调用的直接引用，而方法可能返回null。

REC：直接捕获Exception，而实际上可能是RuntimeException。

ST： 从实例方法里直接修改类变量，即static属性。


### 总结

Bad practice 坏的实践：常见代码错误，用于静态代码检查时进行缺陷模式匹配

Correctness 可能导致错误的代码，如空指针引用等

国际化相关问题：如错误的字符串转换

可能受到的恶意攻击，如访问权限修饰符的定义等

多线程的正确性：如多线程编程时常见的同步，线程调度问题。

运行时性能问题：如由变量定义，方法调用导致的代码低效问题。




