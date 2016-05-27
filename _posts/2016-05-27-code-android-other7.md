---
layout: post
title:  深度拷贝
description: "java 深度拷贝 ."
modified: 2016-05-27
tags: [android-other , post]
image:
  feature: abstract-7.jpg
---



#### 深度拷贝
{% highlight html %}
/**
 * 深度拷贝
 * 拷贝对象 需要 序列号
 * implements Serializable
 *
 * @param src
 * @return
 * @throws IOException
 * @throws ClassNotFoundException
 */
 public List deepCopy(List src) throws IOException, ClassNotFoundException {
        ByteArrayOutputStream byteOut = new ByteArrayOutputStream();
        ObjectOutputStream out = new ObjectOutputStream(byteOut);
        out.writeObject(src);

        ByteArrayInputStream byteIn = new ByteArrayInputStream(byteOut.toByteArray());
        ObjectInputStream in = new ObjectInputStream(byteIn);
        return (List) in.readObject();
    }
{% endhighlight %}




