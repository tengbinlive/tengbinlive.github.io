---
layout: post
title: Android Compatible
description: "兼容问题."
modified: 2015-12-13
tags: [android-optimization , post]
image:
  feature: abstract-10.jpg
---

### Bug描述 

#### 机型：三星 SM-9200

在SM-9200 中，如果是RelativeLayout布局中嵌套 自定义MGridView（显示全部item），

MGridView 需至于某布局下面时（layout_below），

在初始MGridView时会导致高度计算，当前布局中可能出现布局错乱.

### Bug解决

使用LinearLayout 代替 RelativeLayout

