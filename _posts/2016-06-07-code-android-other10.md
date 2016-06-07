---
layout: post
title:  webview 使用 cookie 保存连接
description: "webview 使用 cookie 保存连接"
modified: 2016-06-07
tags: [android-other , post]
image:
  feature: abstract-1.jpg
---



####  获取cookie
{% highlight html %}
http:
Header[] cookies = httpResponse.getHeaders("Set-Cookie");
if(null != cookies && cookies.length > 0){
    String cookieStr = cookies[0].toString();
}

volley:
String cookieStr = networkResponse.headers.get(SET_COOKIE_KEY)
{% endhighlight %}

####  同步cookie
{% highlight html %}
public static boolean syncCookie(String url,String cookie) {
    CookieManager cookieManager = CookieManager.getInstance();
    if (Build.VERSION.SDK_INT < Build.VERSION_CODES.LOLLIPOP) {
        CookieSyncManager.createInstance(context);
        cookieManager.setAcceptCookie(true);
    } else {
        cookieManager.setAcceptThirdPartyCookies(true);
    }
    cookieManager.setCookie(url, cookie);//如果没有特殊需求，这里只需要将session id以"key=value"形式作为cookie即可
    String newCookie = cookieManager.getCookie(url);
    return TextUtils.isEmpty(newCookie)?false:true;
}
{% endhighlight %}

####  其他
{% highlight html %}
通常情况下获取到的cookie类似:
Set-Cookie: JSESSIONID=725B63507EB2989AE6B38DF5698F1B23; Path=/sns/; HttpOnly

如果是以下这种会出现,LOLLIPOP版本下内嵌html无法保存同一用户状态
Set-Cookie: JSESSIONID=725B63507EB2989AE6B38DF5698F1B23
{% endhighlight %}

{% highlight html %}
注：临时cookie(没有expires参数的cookie)不能带有domain选项。
expires=: 设置cookie的有效期，如果cookie超过date所表示的日期时，cookie将失效。
如果没有设置这个选项，那么cookie将在浏览器关闭时失效。
注意：date是格林威治时间(GMT)，使用如下格式表示：
DAY, DD MMM YYYY HH:MM:SS GMT

secure   : 表示cookie只能被发送到http服务器。
httponly : 表示cookie不能被客户端脚本获取到。
{% endhighlight %}



