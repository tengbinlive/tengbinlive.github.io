---
layout: post
title: Android Bug 2
description: "bug 记录 2."
modified: 2016-04-14
tags: [android-bug , post]
image:
  feature: abstract-4.jpg
---

### RecyclerView item 高大于当前屏幕时

#### e.g.

在使用RecyclerView的过程中,RecyclerView -> android:layout_height="match_parent"
,其中有子项item高度超过了,当前RecyclerView设置的match_parent(屏幕显示高度).

#### bug

超过高度的item显示不完全,只显示出了屏幕高度内容. 其他内容被直接裁剪未显示.

#### fix

修改RecyclerView -> android:layout_height="match_wrap_content".
