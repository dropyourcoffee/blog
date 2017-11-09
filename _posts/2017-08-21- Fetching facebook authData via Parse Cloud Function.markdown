---
layout: post
title:  "Fetching Facebook authdata via Parse Cloud Function"
date:   2017-08-21 12:43:53 +0900
categories: Web Parse-Server
---

Fetching To access Facebook authdata from parse-server Cloud Function.<br>
useMasterKey option must be true.


### NodeJS Server querying Parse server

{% highlight javascript %}

var Parse = require('parse/node').Parse;
Parse.initialize("abcdefghijklmnopqrstuvwxyz","aaaabbbbccccddddeeeeffff","ababababababababababab");
Parse.Cloud.useMasterKey();
Parse.serverURL = "https://parse.url.com/parse";

const userLog = Parse.Object.extend('User');

const SearchUser=(parseId,callback) => {
  var userQuery = new Parse.Query(userLog);
  var date;
  userQuery.equalTo("objectId",parseId);
  userQuery.find( {
      success: results => {

        if(results.length == 1) {
          var ret = {};
          ret.parseId = parseId;
          ...
          ret.authData = results[0].get("authData");
          ...

          if(ret.authData==undefined)
            ret.authData = "";

          }else {
            ...
          }

          callback(ret);
        }
        else
          callback({"fail":"parse_FindError"});
      },
      error: err => {
        console.log("err : "+err.message);
        callback(err.message);
      }
  });
};

{% endhighlight %}

### Result
![facebook authData appended]({{site.baseurl}}/img/2017-08-21-img1.png)