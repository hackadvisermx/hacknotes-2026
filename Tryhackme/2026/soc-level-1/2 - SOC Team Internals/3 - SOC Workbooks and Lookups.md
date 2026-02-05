
# SOC Workbooks and Lookups

Discover useful corporate resources to help you structure and simplify L1 alert triage.

# Task 1 - Introduction

Alert triage is a complex process that often requires analysts to gather additional information about affected employees or servers. This room explores SOC workbooks designed to streamline alert triage and explains various lookup methods to quickly retrieve user and system context.

## Learning Objectives

- Familiarise yourself with SOC investigation workbooks
- Learn where to find and how to use asset inventory in SOC
- Understand the importance of corporate network diagrams
- Practice workflow building inside an interactive interface

## Prerequisites

- Complete the SOC L1 [Alert Triage](https://tryhackme.com/room/socl1alerttriage) and [Alert Reporting](https://tryhackme.com/room/socl1alertreporting) rooms
- Have practice with investigating common attack chains
- Understand the fundamental networking concepts
- Preferably, be familiar with the concept of SOAR playbooks

Answer the questions below

I am ready to start!

# Task 2 Assets & Identities

Imagine having a night shift and looking into an alert saying that G.Baker logged into the HQ-FINFS-02 server. Then, the user downloaded the "Financial Report US 2024.xlsx" file from there and shared it with R.Lund. To correctly triage the alert and understand if the activity is expected, you will have to find answers to many questions:

- Who is G.Baker? What are their working hours and role in the company?
- What is the purpose and location of HQ-FINFS-02? Who can access it?
- Why could R.Lund need access to the corporate financial records?

## Identity Inventory

Identity inventory is a catalogue of corporate employees (user accounts), services (machine accounts), and their details like privileges, contacts, and roles within the company. For the scenario above, identity inventory would help you get context about G.Baker and R.Lund, and make it simpler to decide if the activity was expected or not.

**Example of Identities**

| Full Name     | Username     | Email                 | Role                     | Location   | Access           |
| ------------- | ------------ | --------------------- | ------------------------ | ---------- | ---------------- |
| Gregory Baker | G.Baker      | g.baker@tryhatme.thm  | Chief Financial Officer  | Europe, UK | VPN, HQ, FINANCE |
| Raymond Lund  | R.Lund       | r.lund@tryhatme.thm   | US Financial Adviser     | US, Texas  | VPN, FINANCE     |
| Kate Danner   | K.Danner     | k.danner@tryhatme.thm | Chief Technology Officer | Europe, UK | VPN, DA, HQ, AWS |
| svc-veeam-06  | svc-veeam-06 | N/A                   | Backup Service Account   | N/A        | VEEAM, DMZ, HQ   |
| svc-nginx-pp  | svc-nginx-pp | N/A                   | Web App Service Account  | N/A        | DMZ              |

**Sources of Identities**

|Solution|Examples|Description|
|---|---|---|
|Active Directory|On-prem AD, Entra ID|AD itself is an identity database, and it is commonly used by SOC|
|SSO Providers|Okta, Google Workspace|Cloud alternative for AD, an easy way to manage and search the users|
|HR Systems|BambooHR, SAP, HiBob|Limited to employees only, but usually provides full employee data|
|Custom Solution|CSV or Excel Sheets|It is common for IT or security teams to maintain their own solutions|

## Asset Inventory

Asset inventory, also called asset lookup, is a list of all computing resources within an organisation's IT environment. Note that while "asset" is a vague term and can also refer to software, hardware, or employees, this room emphasises servers and workstations only. For the scenario above, asset inventory would help you get context about the HQ-FINFS-02 server.

**Example of Assets**

| Hostname    | Location      | IP Address   | OS                  | Owner           | Purpose                           |
| ----------- | ------------- | ------------ | ------------------- | --------------- | --------------------------------- |
| HQ-FINFS-02 | UK Datacenter | 172.16.15.89 | Windows Server 2022 | Central IT      | File server for financial records |
| HQ-ADDC-01  | UK Datacenter | 172.16.15.10 | Windows Server 2019 | Central IT      | Primary AD domain controller      |
| PC-891D     | London Office | 192.168.5.13 | Windows 11 Pro      | Tech Support    | Stationary PC for accountants     |
| L007694     | Remote        | N/A          | MacOS 13            | A.Kelly, DevOps | Corporate laptop                  |
| L005325     | Remote        | N/A          | MacOS 13            | J.Eldridge, HR  | Corporate laptop                  |

**Sources of Assets**

|Solution|Examples|Description|
|---|---|---|
|Active Directory|On-prem AD, Entra ID|AD is not only an identity but also a solid asset inventory database|
|SIEM or EDR|Elastic, CrowdStrike|Some SIEM or EDR agents collect information about the monitored hosts|
|MDM Solution|MS Intune, Jamf MDM|A dedicated class of solutions created to list and manage assets|
|Custom Solution|CSV or Excel Sheets|Same as with the identity inventory, custom solutions are common|

Answer the questions below

Looking at the identity inventory, what is the role of R.Lund at the company?

 US Financial Adviser

Checking the asset inventory, what data does the HQ-FINFS-02 server store?

 financial records

Finally, does the file sharing from the scenario look legitimate and expected? (Yea/Nay)

Yea

# Task 3 - Network Diagrams

Continuing identity and asset inventory topics, you might also need to look at the alert from a network point of view, especially in bigger companies. Consider the scenario where you are investigating a chain of related alerts based on firewall logs and want to give some meaning to the IPs you see:

1. **08:00**: An IP **103.61.240.174** is repeatedly connecting to a corporate firewall via port **TCP/10443**
2. **08:23**: Firewall logs show that the IP 103.61.240.174 was translated to an internal **10.10.0.53** IP
3. **08:25**: The IP 10.10.0.53 is scanning the **172.16.15.0/24** network range but does not find open ports
4. **08:32**: The same IP is now scanning the **172.16.23.0/24** network range, and the attack seems to be ongoing

## Network Diagrams

To investigate the case above, you will have to find out what service is running at the 10443 port and why anyone would connect there. Then, identify the subnet the 10.10.0.53 IP belongs to and why it would ever try to connect to other subnets. A **network diagram**, a visual schema presenting existing locations, subnets, and their connections, is an answer to your questions:

Depending on a company's size and structure, you may see more complex diagrams, but their use for SOC analysts remains the same - to help understand suspicious network activity. In our scenario, you can refer to the network diagram and reconstruct the attack path as follows:

1. Threat actor behind the 103.61.240.174 IP performed **VPN brute force**, targeting vpn.tryhatme.thm
2. After a successful brute force and VPN login, the threat actor was assigned an IP from the **VPN Subnet**
3. Then, the adversary tried to scan the **Database Subnet**, but was likely blocked by the firewall rules
4. Seeing no success, the threat actor switches to the **Office Subnet**, looking for their next target

## Answer the questions below

According to the network diagram, which service is exposed on the TCP/10443 port?

 vpn

Now, which subnet would the server behind 172.16.15.99 IP belong to?

 Database subnet

Finally, does the scenario look like a True Positive (TP) or False Positive (FP)?

TP

# Task 4 - Workbooks Theory

With asset inventory and network diagrams, you can get enough context about the user, host, or IP address. Next, your task is to make a verdict on whether the activity you see is safe or not. For some alerts, the analysis is simple, but some may require dozens of essential steps that must be followed to avoid missing vital details and confusing attack evidence. So, how can you ensure all the analysis steps are always followed?

## SOC Workbooks

**SOC workbook**, also called playbook, runbook, or workflow, is a structured document that defines the steps required to investigate and remediate specific threats efficiently and consistently. Since L1 analysts are considered junior specialists and are not expected to triage every possible attack scenario perfectly, senior analysts often prepare workbooks to support their less experienced teammates. L1 analysts are recommended and sometimes even required to triage the alerts precisely according to workbooks to avoid mistakes and streamline the analysis.

## Workbook Example

The diagram above is a typical example of an investigation workbook aimed to help L1 analysts triage alerts about atypical email, web, or corporate VPN login. Most workbook diagrams are supplemented with a detailed textual guide and links to the mentioned resources. Also, note how the workbook is divided into three logical groups. By following the steps in the correct order, you can guarantee high-quality alert triage and eliminate cases where the verdict is made without enough evidence:

1. **Enrichment**: Use Threat Intelligence and identity inventory to get information about the affected user
2. **Investigation**: Using the gathered data and SIEM logs, make your verdict if the login is expected
3. **Escalation**: Escalate the alert to L2 or communicate the login with the user if necessary

## Answer the questions below

Which SOC role would use workbooks the most (e.g. SOC Manager)?

 SOC L1 Analyst

What is the process of gathering user, host, or IP context using TI and lookups?

 Enrichment

Looking at the workbook example, what platform is used as an identity inventory source?

BambooHR


# Task 5 - Workbooks Practice

Different teams have different approaches to workbook building. Some teams may have hundreds of complex workbooks for every possible detection rule, more like a SOAR automation playbook than human guides. Other teams may prepare just a few high-level workbooks for the most common attack vectors and rely more on the experience and decision-making of L1 analysts. In any case, you as an L1 analyst should know how to divide your investigation into modular blocks and build simple workbooks around it.

## Practice

Let's practice building the workbooks! Open the attached site by pressing the **View Site** button above and fill in the missing workbook steps from the options. Drag and drop the options to their respective positions. If the position is correct, the option will stick there. Once you are done, receive the flag and continue to the next section!


## Answer the questions below

What flag did you receive after completing the first workbook?

 THM{the_most_common_soc_workbook}

What flag did you receive after completing the second workbook?

  THM{be_vigilant_with_powershell}

What flag did you receive after completing the third workbook?

 THM{asset_inventory_is_essential}

# Task 6 Conclusion

Nice work on building the workbooks! Remember to use the existing lookups like asset inventory or network map to better understand the alerts, and push your team to implement and maintain workbooks to streamline and simplify SOC operations. Hope you enjoyed the room!

Answer the questions below

I am ready to move on!
