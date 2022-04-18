# JaWT Scratchpad

## Description

Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/58210/` or http://jupiter.challenges.picoctf.org:58210

## Info 
On the home page wee can create a user and write some text. With the JWT token wee can loging and see what wee have writed. Wee need to get the `admin Token`.

## Links
- [[WebApp]]
- [[JWT Token]]

## Exploit

Wee got our JWT token: `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoidGVzdCJ9.IAu_YSHppFe8hXH_BSPb4OLJYGUi8wXqXdS0T33cKbA`

### Go to https://jwt.io
Wee see

#### Payload

Header:
```javascript
{
  "typ": "JWT",
  "alg": "HS256"
}
```

Payload:
```javascript
{
  "user": "test"
}
```

Signature:
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  `secret_key`
)
```

#### Way to exploit
Change the user by `admin` but you can't have valid JWT without the `secret`

#### Crack the signature
Wee can use [[Hashcat]]
`hashcat -m 16500 jwt <path_wordlist>` => ilovepico

## Get Flag
Change the user with `admin` and write `ilovepico` for the keys. Change the JWT in browser, reaload and wee got the flag