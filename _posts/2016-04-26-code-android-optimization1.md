---
layout: post
title: XWalkView 替代 WebView
description: "XWalkView 替代 WebView ."
modified: 2016-04-26
tags: [android-optimization , post]
image:
  feature: abstract-11.jpg
---

## [Crosswalk](https://crosswalk-project.org/)

## [APIs](https://crosswalk-project.org/documentation/apis/embedding_api.html)

### 配置：

{% highlight html %}
allprojects {
    repositories {
        maven { url 'https://download.01.org/crosswalk/releases/crosswalk/android/maven2'}
    }
}
{% endhighlight %}

{% highlight html %}
dependencies {
    compile 'org.xwalk:xwalk_core_library:10.39.235.15'
}
{% endhighlight %}


### 使用

#### 权限
{% highlight html %}
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
{% endhighlight %}

#### 添加布局
{% highlight html %}
<org.xwalk.core.XWalkView
     android:id="@+id/xwalk_view"
     android:layout_width="match_parent"
     android:layout_height="match_parent"
     android:background="@color/theme_bg_layout" />
{% endhighlight %}

#### 获取id XWalkView xWalkView = (XWalkView) findViewById(R.id.xwalk_view);

#### 常用设置
{% highlight html %}
0. debug调试
  XWalkPreferences.setValue(XWalkPreferences.REMOTE_DEBUGGING, true);
  
1. 执行js
  xWalkView.load("javascript:document.body.contentEditable=true;", null);
  
2. JavaScript回调Java
  XWalkSettings webSettings = xWalkView.getSettings();
  //Tells the WebView to enable JavaScript execution. 
  webSettings.setJavaScriptEnabled(true);
  //绑定
  xWalkView.addJavascriptInterface(new JsInterface(), "NativeInterface");

3. WebViewClient对应监听（或setResourceClient）
  private void xWalkViewSetInit(String url) {
        xWalkView.setUIClient(new XWalkUIClient(xWalkView) {
            @Override
            public void onPageLoadStarted(XWalkView view, String url) {
                super.onPageLoadStarted(view, url);
                progress.setVisibility(View.VISIBLE);//进度条 开始
            }

            @Override
            public void onPageLoadStopped(XWalkView view, String url, LoadStatus status) {
                super.onPageLoadStopped(view, url, status);
                progress.setVisibility(View.GONE);//进度条 结束
            }
        });
        xWalkView.load(url, null);
  }
{% endhighlight %}

#### 生命周期（避免内存问题）
{% highlight html %}
    @Override
    protected void onActivityResult(int requestCode, int resultCode,
                                    Intent intent) {
        if (xWalkView != null) {
            xWalkView.onActivityResult(requestCode, resultCode, intent);
        }
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        if (xWalkView != null) {
            xWalkView.onDestroy();
        }
    }

    @Override
    public void onPause() {
        super.onPause();
        if (xWalkView != null) {
            xWalkView.pauseTimers();
            xWalkView.onHide();
        }
    }

    @Override
    public void onResume() {
        super.onResume();
        if (xWalkView != null) {
            xWalkView.resumeTimers();
            xWalkView.onShow();
        }
    }

    @Override
    public void onBackPressed() {
        // Go backward
        if (xWalkView != null && xWalkView.getNavigationHistory().canGoBack()) {
            xWalkView.getNavigationHistory().navigate(
                    XWalkNavigationHistory.Direction.BACKWARD, 1);
        } else {
            super.onBackPressed();
        }
    }

    @Override
    public void onNewIntent(Intent intent) {
        if (xWalkView != null) {
            xWalkView.onNewIntent(intent);
        }
    }
{% endhighlight %}

#### 动画开启

默认XWalkView不能使用动画，甚至setVisibility也不行
{% highlight html %}
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        // ANIMATABLE_XWALK_VIEW preference key MUST be set before XWalkView creation.
        XWalkPreferences.setValue(XWalkPreferences.ANIMATABLE_XWALK_VIEW, true);
        super.onCreate(savedInstanceState);
    }
    
@Override
    public void onDestroy() {
        super.onDestroy();
        if (xWalkView != null) {
              xWalkView.onDestroy();
        }
        // Reset the preference for animatable XWalkView.
        XWalkPreferences.setValue(XWalkPreferences.ANIMATABLE_XWALK_VIEW, false);
    }
{% endhighlight %}
