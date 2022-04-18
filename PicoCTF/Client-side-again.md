# Client-side-again

## Description

Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/6353/` ([link](https://jupiter.challenges.picoctf.org/problem/6353/)) or http://jupiter.challenges.picoctf.org:6353


## Info

```javascript

function verify() {
    checkpass = document.getElementById('pass').value;
    split = 0x4;
    if (checkpass.substring(0x0, split * 0x2) == 'picoCTF{') {
        if (checkpass.substring(0x7, 0x9) == '{n') {
            if (checkpass.substring(split * 0x2, split * 0x2 * 0x2) == 'not_this') {
                if (checkpass.substring(0x3, 0x6) == 'oCT') {
                    if (checkpass.substring(split * 0x3 * 0x2, split * 0x4 * 0x2) == '0a029}') {
                        if (checkpass.substring(0x6, 0xb) == 'F{not') {
                            if (checkpass.substring(split * 0x2 * 0x2, split * 0x3 * 0x2) == '_again_5') {
                                if (checkpass.substring(0xc, 0x10) == 'this') {
                                    alert('Password Verified');
                                }
                            }
                        }
                    }
                }
            }
        }
    } else {
        alert('Incorrect password');
    }
}

```

## Flag

0 => 8:  `picoCTF{`
7 => 9: `picoCTF{n`
8 => 16: `picoCTF{not_this`
3 => 6: `picoCTF{not_this`
24 => 32: `0a029}`
16 => 24: `_again_5`
12 => 16: `this`

Flag: `picoCTF{not_this_again_50a029}`

## Links
- [[WebApp]]
- [[JsObfuscate]]