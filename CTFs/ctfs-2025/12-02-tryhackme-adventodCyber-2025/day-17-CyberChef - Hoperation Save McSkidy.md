
# CyberChef - Hoperation Save McSkidy

# Task 1 - Introduction

_McSkidy is imprisoned in King Malhare's Quantum Warren. Sir BreachBlocker III was put in charge of securing the fortress and implemented several access controls to prevent any escape. His defenses are worthy of his name._

_However, McSkidy managed to send vital clues to his team using harmless bunny pictures. One message revealed that five locks needed to be disabled to secure an escape route. The locks can be broken by examining their logic and leveraging the system's built-in chat for the guards. They can be eluded in revealing vital details or even passwords. However, you will need to speak their language._

## Learning Objectives

- Introduction to encoding/decoding
- Learn how to use CyberChef
- Identify useful information in web applications through HTTP headers

# Task 2- Important Concepts


## Encoding and Decoding

Encoding is a method to transform data to ensure compatibility between different systems. It differs from encryption in purpose and process.

|a|Encoding|Encryption|
|---|---|---|
|**Purpose**|Compatibility  <br>Usability|Security  <br>Confidentiality|
|**Process**|Standardized|Algorithm + Key|
|**Security**|No|Yes|
|**Speed**|Fast|Slow|
|**Examples**|Base64|TLS|

Decoding is the process of converting encoded data back to its original, readable, and usable form.

## CyberChef Overview

[CyberChef](https://cyberchef.io/) is also known as the Cyber Swiss Army Knife. Ready to cook some recipes?

|Area|Description|
|---|---|
|Operations|Repository of diverse CyberChef capabilities|
|Recipe|Fine-tune and chain the operations area|
|Input|Here you provide the input for your recipe|
|Output|Here is the output of your recipe|

## Simple Example

Try your first recipe:

- Open either the online [CyberChef](https://cyberchef.io/) version in your regular browser, or use the offline CyberChef version available in the bookmarks section of the AttackBox. Drag and drop the `To Base64` operation from the **Operations** area on the left side to the **Recipe** area in the center, and add `IamRoot` into the **Input** area.

- Add another operation, `From Base64`, to show the initial input again, showcasing chain operations.

**Note:** You can enable/disable an operation in the recipe by toggling the middle button on the right of the operation.

Congratulations! You took the first steps to become a master Chef.

## Inspecting Web Pages

Besides the rendered content of a web page, your browser usually receives and can show additional information.

For this challenge, you will get the chance to have a deeper look at that information and put it to good use.

To do this, depending on your browser, you can access the functionality as shown below:

|Browser|Menu path|
|---|---|
|Chrome|`More tools` > `Developer tools`|
|Firefox|`Menu` (☰) > `More tools` > `Web Developer Tools`|
|Microsoft Edge|`Settings and more (...)` > `More tools` > `Developer tools`|
|Opera|`Developer` > `Developer tools`|
|Safari|`Develop` > `Show Web Inspector` (Requires enabling the "Develop" menu in `Preferences` > `Advanced`)|

> **Note:** For a better experience, you can reposition the console on the right side of the browser. Look for the three dots on the right side of the console.


# Task 3  - First Lock - Outer Gate

## Key Information

If not already, start the target machine, give it a few minutes to boot up, and then, from the AttackBox, you can access the web app at `http://10.80.142.140:8080`.

McSkidy revealed some vital clues in his message. You will have to leverage any useful piece of information in order to break the locks.

Below are key points to look out for:

- **Chat is Base64 encoded**. Try decoding this in CyberChef. This will be leveraged to extract useful information from the guards. Be aware that from Lock 3 onwards, the guards will take a longer time to respond.

- **Guard name**. This logic will persist throughout the levels. Make sure to note down the guard’s name for each level.

All hail King Malhare!

**Hint:**

- Username: This will decode to `CottonTail`.
- Password: Look at the level login logic and decode the guard reply.

### Level 1

- Lo que hice fue pasar  CottonTail a base64 : Q290dG9uVGFpbA== y el pass lo tome del codigo 
 <meta name="const" content="SWFtc29mbHVmZnk="> que fue Iamsofluffy


Q290dG9uVGFpbA==

 passOk = btoa(pwd) === expectedConst;

Iamsofluffy


- **Headers**. Again, inspecting the page but switching to the ‘_Network_’ tab this time. Make sure to refresh the page once after switching to this tab and select the first response.

### Level 2

U1hSdmJHUjViM1YwYjJOb1lXNW5aV2wwSVE9PQ==

passOk = btoa(btoa(pwd)) === expectedConst;

CarrotHelm
Q2Fycm90SGVsbQ==
Itoldyoutochangeit!

### Level 3

 IQwFFjAWBgsf
cyberchef
```
/ CyberChef: From Base64 => XOR(key=recipeKey)
        const bytes = xorWithKey(toBytes(pwd), toBytes(recipeKey));
        const b64 = bytesToBase64(bytes);
        passOk = b64 === expectedConst;
``` 

Pass:
BugsBunny

User:
LongEars
TG9uZ0VhcnM=

### Level 4


```
passOk = (md5(pwd) === expectedConst);
```
Password:

md5
b4c0be7d7e97ab74c13091b76825cf39
passw0rd1

User:
Lenny
TGVubnk=

### Level 5


MTOQpHAvLmD5pG1sAQkvDj==
R4

```
case "R4":
            // CyberChef: ROT13 => From Base64 => ROT47
            tp = rot13(btoa(rot47(tp)));
```

51rBr34chBl0ck3r

User:
Carl
Q2FybA==


You have broken every lock and cleared a path for McSkidy to escape. Here is your flag:

THM{M3D13V4L_D3C0D3R_4D3P7}

[](http://10.81.188.224:8080/)


# > Looking for the key to **Side Quest 3**? Hopper has left us this [cyberchef link](https://gchq.github.io/CyberChef/#recipe=To_Base64\('A-Za-z0-9%2B/%3D'\)Label\('encoder1'\)ROT13\(true,true,false,7\)Split\('H0','H0%5C%5Cn'\)Jump\('encoder1',8\)Fork\('%5C%5Cn','%5C%5Cn',false\)Zlib_Deflate\('Dynamic%20Huffman%20Coding'\)XOR\(%7B'option':'UTF8','string':'h0pp3r'%7D,'Standard',false\)To_Base32\('A-Z2-7%3D'\)Merge\(true\)Generate_Image\('Greyscale',1,512\)&input=SG9wcGVyIG1hbmFnZWQgdG8gdXNlIEN5YmVyQ2hlZiB0byBzY3JhbWJsZSB0aGUgZWFzdGVyIGVnZyBrZXkgaW1hZ2UuIEhlIHVzZWQgdGhpcyB2ZXJ5IHJlY2lwZSB0byBkbyBpdC4gVGhlIHNjcmFtYmxlZCB2ZXJzaW9uIG9mIHRoZSBlZ2cgY2FuIGJlIGRvd25sb2FkZWQgZnJvbTogCgpodHRwczovL3RyeWhhY2ttZS1pbWFnZXMuczMuYW1hem9uYXdzLmNvbS91c2VyLXVwbG9hZHMvNWVkNTk2MWM2Mjc2ZGY1Njg4OTFjM2VhL3Jvb20tY29udGVudC81ZWQ1OTYxYzYyNzZkZjU2ODg5MWMzZWEtMTc2NTk1NTA3NTkyMC5wbmcKClJldmVyc2UgdGhlIGFsZ29yaXRobSB0byBnZXQgaXQgYmFjayE) as a lead. See if you can recover the key and access the corresponding challenge in our [Side Quest Hub](https://tryhackme.com/adventofcyber25/sidequest)!





### REferencias

- https://tryhackme.com/room/cryptographyintro
- 




