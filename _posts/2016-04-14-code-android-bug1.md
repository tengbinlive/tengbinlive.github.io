---
layout: post
title: Android Bug 1
description: "bug 记录 1."
modified: 2016-04-14
tags: [android-bug , post]
image:
  feature: abstract-4.jpg
---

### .png或.9.png 文件问题 ，可能.9.png放置位置不对(比如放在了mipmap中)，或是PNG文件保存时格式错误(直接将.jpg改后缀为.png有时也会出问题)等

{% highlight html %}
1. AAPT err(Facade for 558739077): libpng error: Not a PNG file

2. Error:Execution failed for task ':app:mergeDebugResources'.
   > Crunching Cruncher top_bg.9.png failed, see logs
   
3. Error: Invalid file name: must contain only lowercase letters and digits ([a-z0-9_.])
{% endhighlight %}

{% highlight html %}
//关闭Android Studio的PNG合法性检查的
 defaultConfig {
        aaptOptions.cruncherEnabled = false
        aaptOptions.useNewCruncher = false
  }
{% endhighlight %}

### 使用 Glide 加载Transformation处理图片时 ，ImageView 图片效果不能被铺满

### 描述
布局
{% highlight html %}
     <ImageView
            android:id="@+id/head_icon"
            android:scaleType="centerCrop"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>
{% endhighlight %}

Glide
{% highlight html %}
      Glide.with(mContext.getApplicationContext()).load(iconUrl).asBitmap()
                       .transform(blurTransformation)
                       .diskCacheStrategy(DiskCacheStrategy.ALL)
                       .placeholder(R.drawable.default_bg).into(head_icon);
{% endhighlight %}

### 处理 使用SimpleTarget，并通过setImageDrawable来设置图片

Glide
{% highlight html %}
        Glide.with(mContext.getApplicationContext()).load(iconUrl).asBitmap()
                         .transform(blurTransformation)
                         .diskCacheStrategy(DiskCacheStrategy.ALL)
                         .placeholder(R.drawable.default_bg).into(new SimpleTarget<Bitmap>() {
                              @Override
                              public void onResourceReady(Bitmap bitmap, GlideAnimation glideAnimation) {
                                 BitmapDrawable bd =  new BitmapDrawable(getResources(),bitmap);
                                 head_icon.setImageDrawable(bd);
                          }
                 });
{% endhighlight %}