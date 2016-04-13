---
layout: post
title: Android Compatible
description: "兼容问题."
modified: 2016-03-28
tags: [android-compatible , post]
image:
  feature: abstract-10.jpg
---

### 描述 

#### 机型：三星 SM-9200

在SM-9200 中，如果是RelativeLayout布局中嵌套 自定义MGridView（显示全部item），
{% highlight java %}
@Override
public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {

   int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2,
                MeasureSpec.AT_MOST);
   super.onMeasure(widthMeasureSpec, expandSpec);
   
}
{% endhighlight %}

MGridView 需至于某布局下面时（layout_below），

在初始MGridView时会导致高度计算，当前布局中可能出现布局错乱.

### 解决

使用LinearLayout 代替 RelativeLayout

