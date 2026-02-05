

# L2 MAC Flooding & ARP Spoofing

Learn how to use MAC Flooding to sniff traffic and ARP Cache Poisoning to manipulate network traffic as a MITM.

# Task 1 Getting Started

While it's not required, ideally, you should have a general understanding of OSI Model [Layer 2](https://en.wikipedia.org/wiki/Data_link_layer) (L2) [network switches](https://en.wikipedia.org/wiki/Network_switch) work, what a [MAC table](https://en.wikipedia.org/wiki/MAC_table) is, what the Address Resolution Protocol ([ARP](https://en.wikipedia.org/wiki/Address_Resolution_Protocol)) does, and how to use Wireshark at a basic level. If you're not comfortable with these topics, please check out the [Network](https://tryhackme.com/module/network-fundamentals) and [Linux](https://tryhackme.com/module/linux-fundamentals) Fundamentals modules and [Wireshark](https://tryhackme.com/room/wireshark) room.

Now that we've covered the prerequisites go ahead and start the machine and let's get started!

_Please, allow a minimum of **5 minutes** for the machine(s) to get the services fully up and running, before connecting via SSH._

Answer the questions below

I understand and have started the machine by pressing the Start Machine button.

# Task 2 Initial Access

_For the sake of this room, let's assume the following:_

While conducting a pentest, you have gained initial access to a network and escalated privileges to root on a Linux machine. During your routine OS enumeration, you realize it's a [dual-homed](https://en.wikipedia.org/wiki/Dual-homed) host, meaning it is connected to two (or more) networks. Being the curious hacker you are, you decided to explore this network to see if you can move laterally.

After having established **persistence**, you can access the compromised host via **SSH**:

|   |   |   |   |
|---|---|---|---|
|**User**|**Password**|**IP**|**Port**|
|admin|Layer2|MACHINE_IP|22|

_Please, allow a minimum of **5 minutes** for the machine to get the services fully up and running, **then** try connecting with SSH (if you login, and the command line isn't showing up yet, **don't hit Ctrl+C!** Just be patient…):_

`ssh -o StrictHostKeyChecking=accept-new admin@MACHINE_IP`

Note: The **admin** user is in the **sudo** group. I suggest using the **root** user to complete this room: `sudo su -`

Answer the questions below

Now, can you (re)gain access? (Yay/Nay)


