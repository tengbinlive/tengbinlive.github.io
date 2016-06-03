---
layout: post
title:  OnGestureListener
description: "OnGestureListener ."
modified: 2016-06-03
tags: [android-other , post]
image:
  feature: abstract-7.jpg
---



####  public boolean onDown(MotionEvent arg0)
// 用户轻触触摸屏，由1个MotionEvent ACTION_DOWN触发


####  public void onShowPress(MotionEvent e)
// 用户轻触触摸屏，尚未松开或拖动，由一个1个MotionEvent ACTION_DOWN触发, 注意和onDown()的区别，强调的是没有松开或者拖动的状态


####  boolean  onSingleTapUp(MotionEvent e)
// 用户（轻触触摸屏后）松开，由一个1个MotionEvent ACTION_UP触发


####  public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY)
// 用户按下触摸屏、快速移动后松开，由1个MotionEvent ACTION_DOWN, 多个ACTION_MOVE, 1个ACTION_UP触发


####  public boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX, float distanceY)
// 用户按下触摸屏，并拖动，由1个MotionEvent ACTION_DOWN, 多个ACTION_MOVE触发


####  void  onLongPress(MotionEvent e)
// 用户长按触摸屏，由多个MotionEvent ACTION_DOWN触发


<figure>
<a href="/images/OnGestureListener.jpg"><img src="/images/OnGestureListener.jpg" alt=""></a>
</figure>


