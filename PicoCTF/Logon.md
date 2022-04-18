# Logun

## Description

The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at?

## Try

- Loging with username `joe` and password `admin` => message: `Joe's password is very good`

- Login with random credential => get logged but message: `dont flag for you`

- SQLI but nothing happends

- Change username cookies with Joe => nothing happend


## Info
- Joe password is strong => no guessing, brute-force
- Wee can log with any random credentials


## Exploit
Log with random credentials and check, if wee have some cookies and yes 3 interresting cookie

- `admin=Fasle`
- `username=test`
- `password=test`

Change cookies `admin` to `True`and wee got the flag.
