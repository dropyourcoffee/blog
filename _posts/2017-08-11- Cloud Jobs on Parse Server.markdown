---
layout: post
title:  "Cloud Jobs on Parse Server"
date:   2017-08-11 12:43:53 +0900
tags: Parse-Server
categories: Web
---
<!--script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script-->

As Parse.com has been retired from its service, Zikto migrated from Parse.com to our [Parse Server](https://github.com/parse-community/parse-server) in Jan 2017.

We initially followed the [parse-server-example guide](http://docs.parseplatform.org/parse-server/guide/) and at the stage we needed to deploy a new firmware update to our end-users after couple of months, My boss asked me to migrate our Cloud Code (pushing a new version of firmware) to our parse server.

At then, I have struggled hours to add the cloud code and found out that there is no background jobs functionality in parse server, ending up with manually writing mongodb script to manually to deploy the firmware update :

![Jobs uploaded but never completes]({{site.baseurl}}/img/2017-08-11-img1.png)
Jobs would upload, never completing the scheduled jobs. Later I found found a [elegant solution](https://gist.github.com/gimdongwoo/326133fc6a471740a5ee73a3565e1b42) from a JS developer forum.

Simiply put the 3 pieces of JS scripts(CloudCode.js, Cron.js, Job.js) and append the following code :


{% highlight javascript %}
if (process.env.NODE_ENV == "production") {
  var Parse = require('parse/node').Parse;
  Parse.initialize(process.env.APP_ID || 'myAppId', null, process.env.MASTER_KEY || '');
  Parse.serverURL = process.env.SERVER_URL || 'http://localhost:1337/parse';

  var CloudCode = require('./src/CloudCode');
  var cloud = new CloudCode(Parse, 'Asia/Seoul');
  cloud.putJob("backgroundJob", null);  // parse cloud function name & param
  cloud.addCron("backgroundJob", "0 */15 * * * *"); // per 15 minutes
  cloud.start();
}
{% endhighlight %}

and add 'cron' to package.json as dependencies.

{% highlight json %}
{
  "dependencies": {
    ...
    "cron": "1.1.0"
  }
}
{% endhighlight %}