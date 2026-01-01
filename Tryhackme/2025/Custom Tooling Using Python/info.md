
# # Custom Tooling Using Python
Creating custom tooling for application testing using Python.


https://tryhackme.com/room/customtoolingpython

# Task 1 Introduction

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

## Task 2 - Using a Coding Language for Custom Tooling

### Why Create Your Own Tools?

When you go up against a web application during a red team, relying solely on existing tools may not always be sufficient. While there are many open-source and commercial options available, they may not fully align with the specific needs of your engagement. Furthermore, most of these tools have already been signed, meaning the likelihood of detection is quite high. Creating custom tooling allows you to:

- Tailor functionality to your specific needs
- Automate exploit and create automated workflows to perform repetitive tasks
- Bypass detection mechanisms
- Modify existing exploits and tools to suit your exact needs

Coding is the ultimate form of this. It allows you to either create something entirely from scratch or build a new tool from existing parts.

### To Script or Not to Script

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

### Choosing the Right Language

Different coding languages have unique strengths and weaknesses when creating custom tooling and exploits. Let's take a look at a comparison:

|   |   |   |   |   |
|---|---|---|---|---|
|**Language**|**Type**|**Key Features**|**Advantages**|**Disadvantages**|
|**Python**|Scripting|Extensive libraries and dynamic typing|Easy to learn and allows for fast prototyping|Slower execution and often easily detected by AVs or EDRs|
|**JavaScript**|Scripting|Browser-based and easy-to-perform threading|Useful for web-based exploits and widely supported in web applications|It is not suitable for low-level system tasks and has a high detection rate|
|**Go (Golang)**|Compiled|Statically types and provides efficient concurrency support|Fast executing and easy cross-compilation|Created larger binary sizes and has fewer security-specific libraries currently|
|**.NET (C#)**|Compiled|Windows-focused and integrates well with system APIs|Good for Windows exploitation and has easy obfuscation techniques|Limited cross-platform compatibility and requires the .NET runtime|
|**C++**|Compiled|High performance and allows for direct memory manipulation|Very fast execution and grants low-level system access, which is great for creating stealthy tools|Complex syntax and is harder to debug|

### Popular Python

Among these options, Python remains one of the most widely used languages for building custom security tools and exploits. Some of the main reasons for its popularity are:

- It allows for fast prototyping and development.
- Python has an extensive library list for things like networking, web interaction, and automation.
- Python's simple syntax makes it easy to develop and modify tools quickly.
- Python scripts can run on any operating system with the Python interpreter installed. Using libraries such as py2exe, you could even create a compiled binary of your Python code to execute on Windows systems that do not have the Python interpreter.
- Given Python's popularity, there is large community support for it, making it easy to modify it using existing tools.

Choosing the right coding language depends on the specific requirements of your custom tooling. While Python offers rapid development and strong community support, compiled languages like Go and .NET can provide better stealth and performance. By understanding these trade-offs, you can select the best language for the task at hand and develop highly effective custom tools for web application red teaming. In this room, we will show how Python can be used. However, you should be able to perform all the tasks in this room using any coding language of your choice.


#### Does a scripting language perform better than a compiled language? (Yea/Nay)

 NAy

#### Which compiled language is easy to cross-compile?

 go
#### Which scripting language is best suited for web-based exploits?

javascript
## Task 3 Developing a Brute-Forcing Tool

Now that we have understood the importance of Python for custom tooling, let’s explore how we can develop a brute-forcing tool to bypass authentication. Brute-force attacks involve trying multiple username-password combinations until the correct credentials are found. While these attacks are commonly mitigated by rate limiting and account lockout mechanisms, they still remain an easy-to-do job for hackers.

## Essential Commands

Before we start coding, let's go over some essential functions and techniques used in brute-forcing:

- **Requests library**: A Python library that facilitates sending HTTP requests and receiving responses from web apps. It has built-in functions to send custom headers like user-agent, HTTP method, and more. 
- **Handling responses**: Identifying successful logins based on HTTP status codes, redirects, or content patterns, which further helps to identify valid credentials.
- **String library**: Built-in functions from the String module make it easy to generate letter sequences, perform text formatting and manipulation, and more.

## Practical

In order to understand the essence of custom tooling using Python, consider a web application hosted at `http://python.thm/labs/lab1`. Visit the application, and you will see the following login panel.

