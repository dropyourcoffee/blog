---
layout: post
title:  "Commonly used OpenSSL commands"
date:   2019-04-15 11:43:53 +0900
tags: Openssl
categories: Linux 
---

While setting up Kubernetes cluster for new DevOps for my team, I find more opportunities tas or set up HTTPS using OpenSSL.

Some common commands I use frequently.

 - Generate new x509 HTTPS Certificate ()
```bash
    openssl genrsa -out server.key 2048
    openssl req -new -key server.key -out server.csr
    openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

 - Encode `<userid>:<password>` in base64 for basic authentication.
```bash
    echo -n "admin:changeme" | openssl enc -base64
    
    ## Alternatively, using htpasswd
    echo -n "admin:changeme" | -cb
```

 - Parse x509 certificate into text
```bash
    openssl x509 -text -noout -in <filename>.crt
    
    ## for DER
    openssl x509 -inform der -text -noout -in <filename>.crt
```

 - Generate key pair
```bash
    openssl genrsa -out server.key 2048
    
    # + Cipher:aes-128 / Passphrase without prompt
    openssl genrsa -aes256 -passout pass:asdfasdf -out aes-pri.key 2048
```
 
 - Extract private key -> public key from key pair
```bash
    openssl rsa -pubout -in server.key
```





