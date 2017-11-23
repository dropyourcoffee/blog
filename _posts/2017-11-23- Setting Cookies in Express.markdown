---
layout: post
title:  "Setting Cookies in NodeJS Express"
date:   2017-11-23 10:41:53 +0900
tags: NodeJS
categories: Web
---


An example source extracted from [Stackoverflow](https://stackoverflow.com/questions/16209145/how-to-set-cookie-in-node-js-using-express-framework)


{% highlight js %}
// need cookieParser middleware before we can do anything with cookies
app.use(express.cookieParser());

// set a cookie
app.use(function (req, res, next) {
  // check if client sent cookie
  var cookie = req.cookies.cookieName;
  if (cookie === undefined)
  {
    // no: set a new cookie
    var randomNumber=Math.random().toString();
    randomNumber=randomNumber.substring(2,randomNumber.length);
    res.cookie('cookieName',randomNumber, { maxAge: 900000, httpOnly: true });
    console.log('cookie created successfully');
  }
  else
  {
    // yes, cookie was already present
    console.log('cookie exists', cookie);
  }
  next(); // <-- important!
});

// let static middleware do its job
app.use(express.static(__dirname + '/public'));
{% endhighlight %}

This temporary verification for a user can be used as long as identical session is maintained.


