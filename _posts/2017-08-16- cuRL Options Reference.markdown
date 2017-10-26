---
layout: post
title:  "cURL Option Reference"
date:   2017-08-16 12:43:53 +0900
categories: Etc
---

### Request Options

#### -X —request <command>

     Set HTTP Method
     Generally "-X GET" option is set as default

#### -H —header <header>

     Add on Header
     -H ""
     헤더를 보낸다.
     -H 'content-type: application/json'
     Add several -H for more than one header.

#### -d, —data <name=content>

     Send data as query string.
     -d is by default '-data-ascii'
     For binary data, '-data-binary' for url-encoded '-data-encode'

     contentType of request header must be:
     -H 'content-type: application/x-www-form-urlencoded'

#### -f, —form <name=content>

     Upload binary file.

     contentType of request header must be:
     -H 'content-type: multipart/form-data'

     For file path prepend @ in front of the path.
     -f 'file=@/var/log/a.file'

#### -K, —config <config file>

     Send request as with config file.

<br><br>


### Response Options

#### -o, —output <file>

     Similar to redirection('>').
     Write ouput to a file instead of stdout.

#### -w, —write-format <format>

     Format the response.
     eg. %{content_type}, %{http_code}, %{time_toal}


