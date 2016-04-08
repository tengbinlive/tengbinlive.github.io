---
layout: post
title: Android Compatible
description: "上传服务器 避免String 特殊字符."
modified: 2014-04-20
tags: [android-compatible , post]
image:
  feature: abstract-10.jpg
---

#### 文件转换成base64编码，然后上传.

转换成base64编码后都是一些数字与字母的组合，不会有特殊字符.
{% highlight java %}
    FileInputStream fis = null;
    ByteArrayOutputStream baos = null;
    try {
        fis = new FileInputStream(file);
        baos = new ByteArrayOutputStream();
        byte[] buffer = new byte[1024];
        int count = 0;
        while ((count = fis.read(buffer)) >= 0) {
            baos.write(buffer, 0, count);
        }
        String uploadBuffer = Base64.encode(baos.toByteArray());
        if (uploadBuffer.equals("") || uploadBuffer.length() <= 0) {
            return true;
         }
        ret = uploadResult(uploadBuffer, method, md5, false, fileName);
      } catch (Exception e) {
             // e.printStackTrace();
             ret = false;
      } finally {
            try {
                if (null != fis)
                    fis.close();
                if (null != baos)
                    baos.close();
                } catch (IOException e) {
                    // TODO Auto-generated catch block
                    // e.printStackTrace();
                     ret = false;
                }
       }
      return ret;
{% endhighlight %}






