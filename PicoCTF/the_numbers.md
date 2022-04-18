# Write up

Open the image extract the numbers and flag it with

```python 
import string

flag_encrypt = "16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }".split(' ')
alphabet = list(string.ascii_letters)

FLAG = ""

for num in flag_encrypt:

    if (num != "{" and  num != "}"):
        FLAG += alphabet[int(num) - 1]
    else:
        FLAG += num

    print(FLAG)



```