---
layout: post
title: aws(亚马逊) ubuntu 部署 openfire
description: "aws亚马逊ubuntu服务器，部署openfire."
modified: 2016-04-08
tags: [ubuntu-openfire , post]
image:
  feature: abstract-2.jpg
---

## ubuntu实例启动完成后

### 0.配置实例安全组，可将HTTP,TCP,SMTP,SSH等相关需要的规则添加



### 1.使用putty 登录 ubuntu (在实例操作界面，点击连接有具体步骤)



### 2.先确保你的系统已经更新到最新 , 输入下面的命令更新
{% highlight html %}
sudo apt-get update

sudo apt-get upgrade
{% endhighlight %}
    
    
    
### 3.安装最新版本的Oracle JRE/JDK，使用PPA(personal package archieve)WEBUPD8的方式安装
{% highlight html %}
sudo apt-get install python-software-properties

sudo add-apt-repository ppa:webupd8team/java

sudo apt-get update
{% endhighlight %}

#### 移除OPenJDK避免冲突
{% highlight html %}
sudo apt-get remove --purge openjdk*
{% endhighlight %}

#### 安装Oracle Java 7
{% highlight html %}
sudo apt-get install oracle-java7-installer
{% endhighlight %}



### 4.安装mysql数据库，安装过程中会有提示框输入mysql密码
{% highlight html %}
sudo apt-get install mysql-server
{% endhighlight %}

#### 为openfire创建数据库,需要输入密码
{% highlight html %}
sudo mysql -u root -p
{% endhighlight %}

#### 创建名为dbopenfire的数据库
{% highlight html %}
mysql>

    CREATE DATABASE dbopenfire CHARACTER SET='utf8';
{% endhighlight %}

#### 用户名为openfire ，密码为openfirepwd
{% highlight html %}
    CREATE USER 'openfire'@'localhost' IDENTIFIED BY 'openfirepwd';

    GRANT ALL PRIVILEGES ON dbopenfire.* TO openfire@localhost WITH GRANT OPTION;

    FLUSH PRIVILEGES;

    quit;
{% endhighlight %}



### 5.下载并且安装openfire，相关版本可以在[openfire官网查看](http://www.igniterealtime.org/downloads/index.jsp)
{% highlight html %}
cd /tmp

wget http://download.igniterealtime.org/openfire/openfire_4.0.2_all.deb
{% endhighlight %}

#### dpkg命令安装
{% highlight html %}
sudo dpkg -i openfire_4.0.2_all.deb
{% endhighlight %}

#### 如出现以下:
{% highlight html %}
(Reading database ... 85791 files and directories currently installed.)
Preparing to replace openfire 3.6.4 (using openfire_3.7.1_all.deb) ...
Unpacking replacement openfire ...
Setting up openfire (3.7.1) ...
Installing new version of config file /etc/openfire/security/truststore ...
Installing new version of config file /etc/init.d/openfire ...
Processing triggers for ureadahead ...
ureadahead will be reprofiled on next reboot
{% endhighlight %}

#### 忽略所有对于用户和文件夹权限的安装误差，这可能是因为你的jre/JDK版本导致的，你需要编辑文件/etc/init/d/openfire  的27行.

#### 将java-6-sun用java-6-oracle或者java-7-oracle代替.
{% highlight html %}
sudo apt-get install rpl
sudo rpl '6-sun' '7-oracle' /etc/init.d/openfire
sudo service openfire start
{% endhighlight %}



### 6.配置openfire的相关端口, 你需要安装防火墙并且允许一些openfire的端口通过

#### 如未安装（默认有安装）

##### 安装
{% highlight html %}
sudo apt-get install ufw
{% endhighlight %}

##### 启用
{% highlight html %}
sudo ufw enable

sudo ufw default deny
{% endhighlight %}

##### 使用ufw命令来配置
{% highlight html %}
sudo ufw allow 9090/tcp
sudo ufw allow 9091/tcp
sudo ufw allow 5222/tcp
sudo ufw allow 7777/tcp
sudo ufw allow 7443/tcp
sudo ufw allow 7070/tcp
sudo ufw allow 3478/tcp
sudo ufw allow 3479/tcp
{% endhighlight %}



### 7.使用浏览器登录配置http://localhost:9090/setup/index.jsp

#### localhost需要换成自己服务器公共ip地址

#### 在数据库设置时选择 标准数据库连接，选择mysql类型

#### 连接 URL(dbopenfire为数据库名称):
{% highlight html %}
jdbc:mysql://localhost:3306/dbopenfire?rewriteBatchedStatements=true
{% endhighlight %}

#### 其他跟随openfire配置向导进行操作即可

#### 注意不要修改登录端口9090 - > 80 ，80端口ubuntu下 你是没权限访问的

#### 如需手动重新配置openfire

##### 搜索openfire相关
{% highlight html %}
whereis openfire 
{% endhighlight %}

#### 进入相关目录（etc/openfire/）修改openfire.xml配置文件

##### 打开openfire.xml
{% highlight html %}
vim openfire.xml
{% endhighlight %}

##### 删除下面代码
{% highlight html %}
<setup>true</setup>
{% endhighlight %}

##### 退出vim
{% highlight html %}
1 按esc键

2 shift 加 :(冒号)

3 输入wq!

4 enter键
{% endhighlight %}

#### 帐号无法登录时,使用vim 编辑 openfire.xml 配置文件（使用admin登录） 

##### 添加
{% highlight html %}
<admin>
<authorizedUsernames>amidn</authorizedUsernames>
</admin>
{% endhighlight %}

##### 至
{% highlight html %}
<jive>
   <admin>
     <authorizedUsernames>amidn</authorizedUsernames>
   </admin>
   <adminConsole> 
     <!-- Disable either port by setting the value to -1 -->  
     <port>9090</port>  
     <securePort>9091</securePort> 
   </adminConsole>
{% endhighlight %}








