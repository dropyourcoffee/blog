---
layout: post
title:  "Install Zeppelin on AWS EC2"
date:   2017-11-17 11:43:53 +0900
tags: Zeppelin
categories: Web
---
Prerequisite :
 - Java7
 - Scala
 - Spark

### Getting Started
[Zeppelin Getting started Documentation](https://zeppelin.apache.org/docs/0.6.0/install/install.html#downloading-binary-package)

Two Options to install Zeppelin :
 - Pre-built binary Package
 - Download Source and build through maven

<br>
I prefer downloading pre-build binary package from [archive](http://www.apache.org/dyn/closer.cgi/zeppelin/zeppelin-0.7.3/zeppelin-0.7.3-bin-all.tgz)
downloaded .tar.gz is around 800MB, unzipped binary package is around 1.1GB.

{% highlight sh %}
wget http://apache.mirror.cdnetworks.com/zeppelin/zeppelin-0.7.3/zeppelin-0.7.3-bin-all.tgz
{% endhighlight %}


### Configurations

Clone .template files without ".template" suffix extension.
 - \<zeppelin_home_dir>/conf/zeppelin-env.sh
 - \<zeppelin_home_dir>/conf/zeppeling-site.xml



### Starting Zeppelin

Linux
{% highlight sh %}
bin/zeppelin-daemon.sh start
{% endhighlight %}

Windows
{% highlight cmd %}
bin\zeppelin.cmd
{% endhighlight %}



### Interpreters

#### jdbc

Set default settings
 - default.driver :: com.mysql.jdbc.Driver
 - default.password	:: \<password>
 - default.url :: jdbc:mysql://\<domain \| ip>:3306/<db name>?characterEncoding=utf8&autoReconnect=true
 - default.user :: \<username>

Other config :
 - configA.driver	com.mysql.jdbc.Driver
 - configA.password	<password>
 - configA.url	jdbc:mysql://\<domain \| ip>:3306/<db name>?characterEncoding=utf8&autoReconnect=true
 - configA.user	\<username>

%jdbc - default interpreter<br>
%jdbc(settingA) - other config

**Also, Add dependancy :**<br>
artifact :: mysql:mysql-connector-java:5.1.38
<br>
<br>
#### elastic search
 - elasticsearch.cluster.name :: elasticsearch
 - elasticsearch.host :: <domain>
 - elasticsearch.result.size :: 1000
 - http.port :: \<port>
 - transport.tcp.port :: \<port>
 - zeppelin.interpreter.localRepo	/root/zeppelin/local-repo/2C5TFTYJ7<br>
