---
layout: post
title: Android Bug
description: "bug 记录."
modified: 2015-03-28
tags: [android-bug , post]
image:
  feature: abstract-4.jpg
---

### ShareSDK分享
 
#### Wechat
 
1. 如果分享类型跟数据填充不匹配，将无法调启微信客服端，如（url ="",分享类型为 = SHARE_WEBPAGE,会无法调启客服端）
  
2. 超出限制也将无法调启客服端 比如(urlImage 大小，title 大小，content 大小)
  
### 混淆打包失败

1. 混淆打包失败 除去app太大原因外，一般都是混淆配置文件少写造成的，警告可以使用-dontwarn 过滤

2. 确实依赖jar , 可能是在studio中删除过该jar ,然后使用快捷键回撤该jar (回撤后jar会无内容).

### webView.loadData 乱码解决
{% highlight html %}
webView.getSettings().setDefaultTextEncodingName("UTF -8");//设置默认为utf-8  

webView.loadData(htmlData, "text/html", "UTF -8");//API提供的标准用法，无法解决乱码问题  

webView.loadData(htmlData, "text/html; charset=UTF-8", null);//这种写法可以正确解码
{% endhighlight %}

### 获取设备信息异常

buildToolsVersion 版本 >= 23时 ,权限会默认关闭，需要提醒用户设置，如：
{% highlight html %}
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
{% endhighlight %}

未处理抛出权限异常

### FragmentAdapter-notifyDataSetChanged()回调无效，需要重写以下方法：
{% highlight html %}
@Override
public Fragment getItem(int position) {
    return TestFragment.newInstance(getIntro(position));
}

@Override
public Object instantiateItem(ViewGroup container, int position) {
    TestFragment f = (TestFragment) super.instantiateItem(container,position);
    return f;
}

@Override
public int getItemPosition(Object object) {
    return PagerAdapter.POSITION_NONE;
}
{% endhighlight %}
