# Write up

## Info

When you try to log with random credentiel => message: login failed
When you try to SQLI => nothing happend => potential SQLI

## Exploit
On burpsuit wee intercept the request wee see two param => `password=<password>` and `debug=0` 

Turn `debug` to `1` and wee can see the SQL request

Try with basic SQLI like `1'or'1'='1` => the request is `SQL query: SELECT * FROM admin where password = '1'be'1'='1'`

Change the SQLI to `1'be'1'='1` and you get the flag