
# Custom Tooling using Burp

Creating custom tooling for application testing using Burp Plugins.

https://tryhackme.com/room/customtoolingviaburp


# Task 1 - Introduction

The ability to create your own custom tooling is critically important for web application red teaming. Rarely will you be able to find a tool or plugin that will do exactly what you need. This then calls for you to develop custom tooling! This custom tooling module will showcase different ways you can approach this problem. Each option is unique and has its benefits and drawbacks.

In this room, we will focus on using **Burp plugins** to create tools and exploit them. Burp acts as an intercepting proxy, allowing you to view and modify requests and responses as the web application interfaces with it. Burp has several features, such as repeating requests or performing automated brute forcing of specific requests and payloads. This makes plugins a unique option when you need additional versatility in your tooling to be used in an automated and manual fashion. While we will showcase using Burp plugins in this room, the principles can be applied to any intercepting proxy you choose. Let's dive in and use Burp plugins to create our very own custom tools and exploits!

## Prerequisites

- [Burp Suite Module](https://tryhackme.com/module/learn-burp-suite)
- [Custom Tooling using Python](https://tryhackme.com/room/customtoolingpython)
## Learning Objectives

- Understand how Burp plugins work and can be used to create custom tools and exploits
- Learn how to create a custom intruder plugin
- Learn how to create a custom proxy plugin
- Learn how to craft plugins for custom cryptography, which will allow you to test it seamlessly even after it is implemented

## Starting the Machine

Deploy the target VM attached to this task by pressing the green **Start Machine** button. After obtaining the machine's generated IP address, you can either use the AttackBox or your own VM connected to TryHackMe's  VPN.

**Note:** This room requires you to start two VMs simultaneously. If you're not using your own machine, be sure to extend the time of the current VM in this room.

You can find and start the second VM from [this room](https://tryhackme.com/jr/customtoolingviaburp2). We will use the IP address of the second VM as `SECOND_VM_IP` in this room.

## Answer the questions below

I am ready to learn about creating custom Burp plugins!

# Task 2 - Using a Proxy for Custom Tooling

## Why Create Your Own Tools?

When you go up against a web application during a red team, relying solely on existing tools may not always be sufficient. While many open-source and commercial options are available, they may not fully align with the specific needs of your engagement. Furthermore, most of these tools have already been signatured, meaning the likelihood of detection is quite high. Creating custom tooling allows you to:

- Tailor functionality to your specific needs
- Automate exploit and create automated workflows to perform repetitive tasks
- Bypass detection mechanisms
- Modify existing exploits and tools to suit your exact needs

In the previous room, we showcased how coding could be used for this task. In this room, our focus shifts to using an intercepting proxy with a custom plugin.

## Custom Crypto Cryptonite

Custom plugins play a large role in mobile application testing due to custom cryptography. Mobile applications are a tad bit special as they are full applications that execute in an untrusted environment. Nothing stops a threat actor from downloading a mobile application from the Play Store and pulling it apart to find potential weaknesses and vulnerabilities. Furthermore, mobile applications can be instrumented using tools such as [Frida](https://frida.re/), allowing threat actors and pentesters to alter the behaviour of the application and attempt to directly interface with the API server backing the application. The issue stems from the fact that a threat actor has full control of the mobile phone, which means it is an untrusted environment.

In an attempt to protect mobile applications and their backing APIs, developers will often take two approaches:

- Mobile binary protections such as source code obfuscation, root detection, and hook detection will be introduced.
- Custom cryptography will be implemented in the requests and responses made to the backing API.

The latter creates an interesting problem both for pentesting and red teaming. If we can't alter the parameters or payloads in the requests being made, we can't really attack the API. Therefore, we need to reverse engineer the custom cryptography to allow ourselves to reproduce the steps in order to alter the parameters. Sometimes, even the response has custom cryptography, meaning we can't even read the output from the server without taking some steps. Usually, the custom cryptography steps will remain static for all requests, meaning that once we have reverse-engineered it once, we can apply the same steps for all subsequent requests.

This places us in a unique position; the custom tooling we need isn't really for an exact exploitation goal, such as creating a brute force or vulnerability scanner. Rather, we need custom tooling to perform the repetitive cryptography steps, allowing us to gain access to the raw requests and responses and then use our main tooling for testing or red teaming. As such, the ideal position for this tooling is within an intercepting proxy, which will perform these steps for each request that is made.

## Interesting Intercepting Proxies and Where to Find Them

Several different options are available for our intercepting proxy. Let's examine some of the most popular ones and compare them.

|   |   |   |   |   |
|---|---|---|---|---|
|**Decision Factor**|**Burp Suite**|**Fiddler**|**OWASP ZAP**|**Caido**|
|**Platform Support**|Windows, macOS, Linux|Windows|Windows, macOS, Linux|Windows, macOS, Linux|
|**Plugin Support**|Extensions in Java, Python, and Ruby|.NET scripting|Add-Ons in Java or JavaScript|JavaScript/TypeScript scripting|
|**Ease of Plugin Development**|High (Burp Extender API and community examples)|Medium (required .NET knowledge)|Medium (ZAP scripting interface and good documentation)|High (Modern, dev-friendly scripting APIs)|
|**Community & Ecosystem**|Large - Extensive library and strong support|Medium - Less security-focused community|Large - Active open-source security community|Growing - A newer tool but with strong momentum|
|**License**|Commercial (Free tier with limitations)|Free|Free and open-source|Free (Open-core with paid support model)|
|**Performance with Large Volumes of Requests**|High - Optimised for intensive workflows|Medium - Can lag under load|Medium - Memory intensive at times|High - Designed for modern performance needs|

## Beautiful Burp

Mobile applications often introduce custom cryptographic layers to protect requests and responses. Our goal is not to break the cryptography itself but to understand and replicate the steps so we can decrypt, inspect, and modify API communication. To do this efficiently, we need tooling that can hook into every request and response, apply repeatable logic, and provide a smooth developer experience for custom plugins. Burp excels in this space. Some of the main reasons for its popularity are:

- Burp offers a robust Extender API, which allows for the development of plugins in Java, Python (via Jython), or Ruby. 
- Plugins can hook into every part of the request/response lifecycle, giving you precise control
- A large and active community means there are plenty of reference plugins and support forums from which to learn. If you are trying to reverse engineer a custom crypto function, chances are someone has done something similar with Burp.
- Burp lets you intercept traffic at any point and modify it manually or automatically. When paired with custom plugins, this makes it possible to decrypt the parameters, re-encrypt the modified ones before sending, and present cleartext responses to you, the tester.

For this task, we will be using Burp Suite as our intercepting proxy of choice. While several tools offer powerful interception and scripting capabilities, Burp Suite stands out due to its maturity, extensibility, and widespread use in mobile application security testing.

While other tools like Fiddler, ZAP, and Caido have their merits, Burp’s balance of power, flexibility, and community support makes it the clear winner for this task—especially when dealing with custom crypto in mobile apps.

In the next section, we’ll begin building our custom Burp plugin, stepping through how to hook into the request/response cycle and implement the cryptographic transformations we need.


# Task 3 Using Extensions in Burp

In this task, we will explore Burp extensions and how they ease a pentester’s job by automating routine tasks. Burp offers built-in extensions that enhance basic security testing capabilities, such as logging, request/response modification, and simple automation. Some of the extensions are available for free, while a few require Burp Professional.

## Playing with Extensions

In the attached VM, click on the `Burp` icon on the left pane to open the Burp Sutie Community Edition. Once Burp is open, click on the `Extension` tab and then click on the `BApp Store` to view multiple extensions offered by Burp and uploaded by community users worldwide.

In this task, we will install the famous extension **Decoder Improved**, which allows for the encoding and decoding of URLs and HTML, and hashing of input. This extension comes in handy when you are dealing with a complex web application that has incorporated multiple encoding mechanisms; therefore, instead of using any other application or custom script, you can simply use this extension to perform decoding. 

In the list of available extensions, find **Decoder Improved** and you will find the **Install** button on the right side to install it (Do not click the button yet), as shown below:

**Note**: Since the attached VM is not connected to the internet, we will install the extension in offline mode. However, on an internet-connected machine, you can simply click the Install button to install the extension directly.

On the same screen, click the `Manual Install` button as shown below, and select the `Decoder-Improved.bapp` file from `/home/ubuntu/lib`, as shown below:

