# dont-use-client-side

## Description

Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/29835/` ([link](https://jupiter.challenges.picoctf.org/problem/29835/)) or http://jupiter.challenges.picoctf.org:29835

## Info 
### Code source Page
```javascript
function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == '723c') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_7') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == 'e}') {
                  alert("Password Verified")
                  }
                }
              }
      
            }
          }
        }
      }
    }
    else {
      alert("Incorrect password");
    }
    
  }

```

#### Substring
La méthode **`substring()`** retourne une sous-chaîne de la chaîne courante, entre un indice de début et un indice de fin.

```javascript
const str = 'Mozilla';

console.log(str.substring(1, 3));
// expected output: "oz"

console.log(str.substring(2));
// expected output: "zilla"
```



## Flag

0 => 4: `pico`
4 => 8: `CTF{`
8 => 12: `no_c`
12 => 16: `lien`
16 => 20: `ts_p`
20 => 24: `lz_7`
24 => 28: `723c`
28 => 32: `e}`

Flag: `picoCTF{no_clients_plz_7723ce}`