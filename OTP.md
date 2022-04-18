# OTP

One-time pad cipher is a type of Vignere cipher which includes the following features −

-   It is an unbreakable cipher.
    
-   The key is exactly same as the length of message which is encrypted.
    
-   The key is made up of random symbols.
    
-   As the name suggests, key is used one time only and never used again for any other message to be encrypted.
    

Due to this, encrypted message will be vulnerable to attack for a cryptanalyst. The key used for a one-time pad cipher is called **pad**, as it is printed on pads of paper.

## Why is it Unbreakable?

The key is unbreakable owing to the following features −

-   The key is as long as the given message.
    
-   The key is truly random and specially auto-generated.
    
-   Key and plain text calculated as modulo 10/26/2.
    
-   Each key should be used once and destroyed by both sender and receiver.
    
-   There should be two copies of key: one with the sender and other with the receiver.
    

## Encryption

To encrypt a letter, a user needs to write a key underneath the plaintext. The plaintext letter is placed on the top and the key letter on the left. The cross section achieved between two letters is the plain text. It is described in the example below −

![OTP](https://www.tutorialspoint.com/cryptography_with_python/images/otp.jpg)

## Decryption

To decrypt a letter, user takes the key letter on the left and finds cipher text letter in that row. The plain text letter is placed at the top of the column where the user can find the cipher text letter.