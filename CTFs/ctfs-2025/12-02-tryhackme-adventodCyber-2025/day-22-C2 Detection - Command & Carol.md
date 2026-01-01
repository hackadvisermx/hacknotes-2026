
# C2 Detection - Command & Carol



Explore how to analyze a large PCAP and extract valuable information.

The TBFC is very wary since the last series of attacks by the underlings of King Malhare. They are on full alert for anything happening. But they are getting restless; it is too quiet. Sir Elfo of the TBFC takes the initiative and proposes to hunt for Command and Control traffic using the meticulously collected network traffic. A majority of the TBFC elves object, we don't have the time to go through so much network traffic! Sir Elfo chuckles, don't fret, for I have a powerful tool to assist us! I present to you RITA, Real Intelligence Threat Analytics. We just need to convert our PCAP file to Zeek logs, and RITA will do the rest! Anyone can do it, just follow today's tasks.

## Learning Objectives

- Convert a PCAP to Zeek logs
- Use RITA to analyze Zeek logs
- Analyze the output of RITA

# Task 2 - Detecting C2 with RITA

## The Magic of RITA

Real Intelligence Threat Analytics (RITA) is an open-source framework created by Active Countermeasures. Its core functionality is to detect command and control (C2) communication by analyzing network traffic captures and logs. Its primary features are:

- C2 beacon detection
- DNS tunneling detection
- Long connection detection
- Data exfiltration detection
- Checking threat intel feeds
- Score connections by severity
- Show the number of hosts communicating with a specific external IP
- Shows the datetime when the external host was first seen on the network

The magic behind RITA is its analytics. It correlates several captured fields, including IP addresses, ports, timestamps, and connection durations, among others. Based on the normalized and correlated dataset, RITA runs several analysis modules collecting information like:

- Periodic connection intervals
- Excessive number of DNS queries
- Long FQDN
- Random subdomains
- Volume of data over time over HTTPS, DNS, or non-standard ports
- Self-signed or short-lived certificates
- Known malicious IPs by cross-referencing with public threat intel feeds or blocklists

RITA only accepts network traffic input as **Zeek** logs. **Zeek** is an open-source **network security monitoring (NSM)** tool. Zeek is not a firewall or IPS/IDS; it does not use signatures or specific rules to take an action. It simply observes network traffic via configured SPAN ports (used to copy traffic from one port to another for monitoring), physical network taps, or imported packet captures in the PCAP format. Zeek then analyzes and converts this input into a structured, enriched output. This output can be used in incident detection and response, as well as threat hunting. Out of the box, Zeek covers two of the four types of NSM data: transaction data (summarized records of application-layer transactions) and extracted content data (files or artifacts extracted, such as executables).

## PCAP, I Convert Ye to Zeek logs

Let's get started! A neat feature of Zeek is that it can convert packet captures (PCAPs) into structured logs. If you haven't yet done so, open the VM and start a terminal. Navigate to the home directory of the logged-in user and list its contents. As shown in the terminal below, we can see two directories named `pcaps` and `zeek_logs`.

RITA walkthrough

```shell-session
ubuntu@tryhackme$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos  pcaps  zeek_logs
```

The `pcaps` directory contains example PCAPs of real-life incidents collected from Bradly Duncan's [blog](https://malware-traffic-analysis.net/). He has a wonderful collection of malware-related PCAPs that cover real-world threats.

The `zeek_logs` directory contains Zeek logs. These were created by parsing a PCAP file. Let's parse a PCAP ourselves and look at the output Zeek logs. We will use the `zeek readpcap <pcapfile> <outputdirectory>` command.

RITA walkthrough

```shell-session
ubuntu@tryhackme$ zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat
Starting the Zeek docker container
Zeek logs will be saved to /home/ubuntu/zeek_logs/asyncrat
```

Let's examine the logs created. Navigate to `/home/ubuntu/zeek_logs/asyncrat` and list its contents. The output should be similar to the one shown on the terminal below.

RITA walkthrough

```shell-session
ubuntu@tryhackme$ cd /home/ubuntu/zeek_logs/asyncrat/ && ls
capture_loss.log  dns.log    http.log         known_services.log  notice.log  packet_filter.log  software.log  stats.log  x509.log
conn.log          files.log  known_hosts.log  loaded_scripts.log  ocsp.log    reporter.log       ssl.log       weird.log
```

In the terminal above, we can see the different Zeek logs that were generated. For using RITA, we don't really need to know what is in these logs (although the names are quite self-descriptive); however, if you are interested, you can use `cat` to examine their contents. You can find more info at https://docs.zeek.org/en/master/logs/index.html if you want a detailed description.

## Now, Analyze This RITA

Now that we have prepared the Zeek logs, we can import them into RITA and unleash its analytics.  
Enter the command below to import the Zeek logs and let RITA do its work. Once you enter the command, RITA will parse and analyze the imported logs. As seen in the terminal, a lot of output is produced. The terminal output was redacted in the example below to keep it tidy.

RITA walkthrough

```shell-session
ubuntu@tryhackme$ rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat
[REDACTED]
2025-10-23T10:56:58Z INF Initiating new import... dataset=asyncrat directory=/tmp/zeek_logs rebuild=false rolling=false started_at="2025-10-23 10:56:58.079568235 +0000 UTC m=+0.013974881"
2025-10-23T10:56:58Z INF [THREAT INTEL] Updating online feed... feed_url=https://feodotracker.abuse.ch/downloads/ipblocklist.txt
[-] Parsing:  /tmp/zeek_logs/conn.log
[-] Parsing:  /tmp/zeek_logs/http.log
[-] Parsing:  /tmp/zeek_logs/ssl.log
[-] Parsing:  /tmp/zeek_logs/dns.log
Log Parsing ? ??????????????????????????????????????????????????????????? 4 / 4
[REDACTED]
```

Now that RITA has parsed and analyzed our data, we can view the results by entering the command `rita view <database-name>`. Now enter the command below. Note: It is important to consider the dataset's size. Larger datasets will provide more insights than smaller ones. Smaller datasets are also more prone to false positive entries. The one we are using is rather small, but it contains sufficient data for an initial usable result.

RITA walkthrough

```shell-session
ubuntu@tryhackme$ rita view asyncrat
```

After entering the command, we can see a structured terminal window with the results, as shown in the image below.

The terminal window shows three elements: the search bar, the results pane, and a details pane.

**Search bar**  
To search, we need to enter a forward slash (/). We can then enter our search term and narrow down the results. The search utility supports the use of search fields. When we enter `?` while in search mode, we can see an overview of the search fields, alongside some examples. The image below shows the help for the search utility. To exit the help page, enter `?` again. Enter the escape key ("esc") to exit the search functionality.

**Results pane**  
The results pane includes information for each entry that can quickly help us recognize potential threats. The following columns are included:

- **Severity**: A score calculated based on the results of threat modifiers (discussed below)
- **Source and destination** IP/FQDN
- **Beacon** likelihood
- **Duration** of the connection: Long connections can be indicators of compromise. Most application layer protocols are stateless and close the connection quickly after exchanging data (exceptions are SSH, RDP, and VNC).
- **Subdomains**: Connections to subdomains with the same domain name. If there are many subdomains, it could indicate the use of a C2 beacon or other techniques for data exfiltration.
- **Threat intel**: lists any matches on threat intel feeds

We can see two interesting findings: an FQDN pointing to `sunshine-bizrate-inc-software[.]trycloudflare[.]com` and an IP `91[.]134[.]150[.]150`. Move the keyboard arrows to select the first entry. You should then see detailed information in the right pane.


```
zeek readpcap pcaps/rita_challenge.pcap zeek_logs/challenge
Starting the Zeek docker container
Zeek logs will be saved to /home/ubuntu/zeek_logs/challenge


 ✔ Container rita-syslog-ng  Running                                                                                                                                         0.0s 
 ✔ Container rita-clickhouse Running                                                                                                                                         0.0s 
Container rita-clickhouse Waiting 
Container rita-clickhouse Healthy 
Container rita-rita-run-b5f3d505b434 Creating 
Container rita-rita-run-b5f3d505b434 Created 
2025-12-22T17:28:09Z INF Initiating new import... dataset=challenge directory=/tmp/zeek_logs rebuild=false rolling=false started_at="2025-12-22 17:28:09.259651126 +0000 UTC m=+0.015101733"
[-] Parsing:  /tmp/zeek_logs/conn.log
[-] Parsing:  /tmp/zeek_logs/http.log
[-] Parsing:  /tmp/zeek_logs/dns.log
Log Parsing 🎉 ╢▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌▌╟ 3 / 3
2025-12-22T17:28:10Z INF Finished Parsing Logs! 🎉 elapsed_time=218.991448ms parsing_began=1766424490 parsing_finished=1766424490

🧂 Seasoning SSL connections  🎉  ███████████████████████████████████████████████████████████████████████████ 100%


🧂 Seasoning HTTP connections 🎉  ███████████████████████████████████████████████████████████████████████████ 100%


✅ Sifting IP connections...

2025-12-22T17:28:11Z INF Finished Seasoning Logs! 🎉 elapsed_time=400.599002ms seasoning_began=1766424490 seasoning_finished=1766424491

SNI Connection Analysis 🎉  ███████████████████████████████████████████████████████████████████████████ 100%


IP Connection Analysis  🎉  ███████████████████████████████████████████████████████████████████████████ 100%


DNS Analysis            🎉  ███████████████████████████████████████████████████████████████████████████ 100%

2025-12-22T17:28:12Z INF Finished Analysis! 🎉 analysis_began=1766424491 analysis_finished=1766424492 elapsed_time=1.772004676s
2025-12-22T17:28:12Z INF Finished Modification! 🎉 elapsed_time=36.645381ms modification_began=1766424492 modification_finished=1766424492
2025-12-22T17:28:13Z INF Finished Importing Hour Chunk day=0 elapsed_time=2.608406132s hour=0
2025-12-22T17:28:13Z INF 🎊✨ Finished Import! ✨🎊 elapsed_time=3.8s
 
 
```

```
rita view challenge


```

## Answer the questions below

### How many hosts are communicating with **malhare.net**?

6

### Which Threat Modifier tells us the number of hosts communicating to a certain destination?

prevalence

### What is the highest number of connections to **rabbithole.malhare.net**?

 40

### Which search filter would you use to search for all entries that communicate to **rabbithole.malhare.net** with a **beacon score** greater than 70% and sorted by **connection duration (descending)**?

dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc


### Which port did the host 10.0.0.13 use to connect to **rabbithole.malhare.net**?

80