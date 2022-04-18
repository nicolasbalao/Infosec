# Write up

### Note: [[Tryhackme/Ignite/help]]


## Keys words:
- `Remote file injection`
- `CVE-2018-16763`
- `reverse shell`

## links
- [[Pentesting]]
- [[WebApp]]

## Info
### Home pag
#### That's it!

To access the FUEL admin, go to:  
[http://ignite.th/fuel](http://ignite.th/fuel)  
User name: **admin**  
Password: **admin** (you can and should change this password and admin user information after logging in)

 #### Install the database
    
Install the FUEL CMS database by first creating the database in MySQL and then importing the fuel/install/fuel_schema.sql file. After creating the database, change the database configuration found in `fuel/application/config/database.php` to include your hostname (e.g. localhost), `username, password` and the database to match the new database you created.

    


## Process

### Enumeration
#### Nmap: 
`nmap -A ignite.th`

Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-11 15:59 CEST
Nmap scan report for ignite.th (10.10.35.158)
Host is up (0.055s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS




### Exploit
- Search exploit for Fuel wee find: -   [https://www.exploit-db.com/exploits/50477](https://www.exploit-db.com/exploits/50477) 

- Donwloads a reverse shell php => get reverse shell

### Privilege escaltion
Look at the file database.php and wee find root password

