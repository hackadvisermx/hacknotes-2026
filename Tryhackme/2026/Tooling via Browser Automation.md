#customtooling
# Tooling via Browser Automation

https://tryhackme.com/room/customtoolingviabrowserautomation

# Task 1 Introduction

The ability to create your own custom tooling is critically important for web application red teaming. Rarely will you be able to find a tool or plugin that will do exactly what you need. This then calls for you to develop custom tooling! This custom tooling module will showcase different ways you can approach this problem. Each option is unique and has its benefits and drawbacks.

In this room, we will focus on using **Browser Automation** to create tools and exploits. Browser automation tools allow you to write software that will interface with your browser as a normal human does. This provides some distinct advantages as the browser will already take care of a significant amount of the processing for you, such as running JavaScript and updating the Document Object Model (DOM) as requests are made, leaving you to focus on the exact actions that you want to automate. While this is a more popular option with unit and quality test cases for developers, threat actors can leverage this same tooling to create exploits. In this room, we will showcase Selenium. However, there are several different types of browser automation tools that you could use! Let's dive in and use Selenium to create our very own custom tools and exploits!

## Prerequisites

- [Custom Tooling using Python](https://tryhackme.com/room/customtoolingpython)
    
## Learning Objectives

- Understand how Selenium works and how it can be used to create custom tools and exploits.
- Learn about the considerations when using browser automation.
- Learn how to create a custom Selenium script to brute force CAPTCHAs.

## Starting the Machine

Deploy the target VM attached to this task by pressing the green **Start Machine** button. After obtaining the machine's generated IP address, you can either use the AttackBox or your own VM connected to TryHackMe's  VPN.

**Note:** This room requires you to start two VMs simultaneously. If you're not using your own machine, be sure to extend the time of the current VM in this room.

You can find and start the second VM from [this room](https://tryhackme.com/jr/customtoolingviabrowserautomation2).

# Task 2 - Using Browser Automation for Custom Tooling

## Why Use Browser Automation for Red Teaming?

In the [previous room](https://tryhackme.com/jr/customtoolingviaburp), we looked at how intercepting proxies and custom plugins could help us process and manipulate communication that made use of custom cryptography. However, this approach requires that we reverse-engineer the crypto and replicate the logic ourselves. Browser automation changes things for us!

When you automate the browser, you no longer have to manually break through the layers of encryption. Instead, you let the browser do the heavy lifting, just as it would for a legitimate user. The JavaScript running in the application performs all its logic client-side, including custom encryption and DOM manipulations.

By using browser automation tools, you interact with the application exactly as a real user would. This means that the browser does all the processing for you. Your automation can simply extract the final payloads or responses once they are rendered or transformed.

This makes browser automation tools incredibly useful for:

- Bypassing CAPTCHAs and client-side restrictions - Since you are simulating real interactions, many bot detection mechanisms become less effective. Certain browser automation tools even allow you to inject your browser context, which means the browser used by the automation software will have established trust to bypass bot detection mechanisms.
- Triggering multi-step workflows—Some exploits require interacting with the application across several screens or user actions. Browser automation allows you to chain these steps together fluidly.
- Lifting rendered or dynamically generated values - Often, the data or tokens you want only appear after JavaScript executes. Browser automation gives you direct access to the live DOM and rendered values.

In short, browser automation tools allow you to embrace the application’s logic rather than fight it. By navigating the app as a user would, you can bypass client-side controls, extract dynamic data, and build more resilient and realistic exploits.



# To do

- https://tryhackme.com/room/customtoolingpython
- https://tryhackme.com/room/customtoolingviaburp
- 