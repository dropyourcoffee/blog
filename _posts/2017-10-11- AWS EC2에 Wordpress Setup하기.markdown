---
layout: post
title:  "Wordpress Quick Setup on AWS"
date:   2017-10-11 12:43:53 +0900
tags: Wordpress AWS
categories: Linux/bash
---

Setting up Wordpress on AWS Linux with localhost mysql.

#### Config
 - Amazon AWS Linux
 - local Mysql
<br>
<br>

#### 1. Create a free-tier EC2 instance on AWS.

Setup authentication public key(.pem). (optional)<br>
Setup security group, enable inBound port 80 and 3306 for web and sql access.

<br>

#### 2. Install APM(Apache, PHP MySQL) for Wordpress.

Login to EC2 using SSH.

{% highlight sh %}
sudo -i
yum install php
yum install mysql-server mysql
yum install -y php php-mysql
yum install httpd
{% endhighlight %}

<br>

#### 3. MySQL Setup

Start up MySQL daemon and run sql client.
{% highlight sh %}
/etc/init.d/mysqld start
mysql
{% endhighlight %}

In MySQL, create a wordpress database and setup admin db admin user.
{% highlight sql %}
create database wordpress;
grant all on wordpress.* to wordpressU@'localhost' identified by 'wordpressP';
flush privileges;
exit
{% endhighlight %}

#### 4.

{% highlight sh %}
service httpd start
wget https://wordpress.org/latest.tar.gz
cd /var/www/html
tar xzf latest.tar.gz
chown -R apache.apache wordpress #Check User and Group is set same - apache
service httpd restart
{% endhighlight %}