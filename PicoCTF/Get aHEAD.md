# Get aHEAD

## Description

Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:15931/](http://mercury.picoctf.net:15931/)

## Write Up

Wee need to send `HEAD` request to the url
```bash
❯ curl -I http://mercury.picoctf.net:15931/index.php
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_82880908}
Content-type: text/html; charset=UTF-8
```
