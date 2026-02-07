
# Lateral Movement and Pivoting

Learn about common techniques used to move laterally across a Windows network.

https://tryhackme.com/room/lateralmovementandpivoting

# Task 1 Introduction

In this room, we will look at lateral movement, a group of techniques used by attackers to move around the network while creating as few alerts as possible. We'll learn about several common techniques used in the wild for this end and the tools involved.

It is recommended to go through the [Breaching AD](https://tryhackme.com/room/breachingad) and [Enumerating AD](https://tryhackme.com/room/adenumeration) rooms before this one.

## Learning Objectives

- Familiarise yourself with the lateral movement techniques used by attackers.
- Learn how to use alternative authentication material to move laterally.
- Learn different methods to use compromised hosts as pivots.

## Connecting to the Network

**AttackBox**  

If you are using the Web-based AttackBox, you will be connected to the network automatically if you start the AttackBox from the room's page. You can verify this by running the ping command against the IP of the THMDC.za.tryhackme.com host. We do still need to configure DNS, however. Windows Networks use the Domain Name Service (DNS) to resolve hostnames to IPs. Throughout this network, DNS will be used for the tasks. You will have to configure DNS on the host on which you are running the VPN connection. In order to configure our DNS, run the following command:

Terminal

```shell-session
[thm@thm]$ sed -i '1s|^|nameserver $THMDCIP\n|' /etc/resolv-dnsmasq
```

Remember to replace $THMDCIP with the IP of THMDC in your network diagram.

You can test that DNS is working by running:

`nslookup thmdc.za.tryhackme.com`

This should resolve to the IP of your DC.

**Note: DNS may be reset on the AttackBox roughly every 3 hours. If this occurs, you will have to redo the command above. If your AttackBox terminates and you continue with the room at a later stage, you will have to redo all the DNS steps.**  

You should also take the time to make note of your VPN IP. Using `ifconfig` or `ip a`, make note of the IP of the **lateralmovement** network adapter. This is your IP and the associated interface that you should use when performing the attacks in the tasks.

**Other Hosts**  

If you are going to use your own attack machine, an OpenVPN configuration file will have been generated for you once you join the room. Go to your [access](https://tryhackme.com/access) page. Select `Lateralmovementandpivoting` from the VPN servers (under the network tab) and download your configuration file.

Use an OpenVPN client to connect. This example is shown on a Linux machine; similar guides to connect using Windows or macOS can be found at your [access](https://tryhackme.com/r/access) page.

Terminal

```shell-session
[thm@thm]$ sudo openvpn user-lateralmovementandpivoting.ovpn
Fri Mar 11 15:06:20 2022 OpenVPN 2.4.9 x86_64-redhat-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Apr 19 2020
Fri Mar 11 15:06:20 2022 library versions: OpenSSL 1.1.1g FIPS  21 Apr 2020, LZO 2.08
[....]
Fri Mar 11 15:06:22 2022 /sbin/ip link set dev lateralmovement up mtu 1500
Fri Mar 11 15:06:22 2022 /sbin/ip addr add dev lateralmovement 10.50.2.3/24 broadcast 10.50.2.255
Fri Mar 11 15:06:22 2022 /sbin/ip route add 10.200.4.0/24 metric 1000 via 10.50.2.1
Fri Mar 11 15:06:22 2022 WARNING: this configuration may cache passwords in memory -- use the auth-nocache option to prevent this
Fri Mar 11 15:06:22 2022 Initialization Sequence Completed
```

The message "Initialization Sequence Completed" tells you that you are now connected to the network. Return to your access page. You can verify you are connected by looking on your access page. Refresh the page, and you should see a green tick next to Connected. It will also show you your internal IP address.

**Note:** You still have to configure DNS similar to what was shown above. It is important to note that although not used, the DC does log DNS requests. If you are using your machine, these logs may include the hostname of your device.

**Kali**

If you are using a Kali VM, Network Manager is most likely used as DNS manager. You can use GUI Menu to configure DNS:

- Network Manager -> Advanced Network Configuration -> Your Connection -> IPv4 Settings
- Set your DNS IP here to the IP for THMDC in the network diagram above  
    
- Add another DNS such as 1.1.1.1 or similar to ensure you still have internet access
- Run `sudo systemctl restart NetworkManager` and test your DNS similar to the steps above.

**Note:** When configuring your DNS in this way, the `nslookup` command won't work as expected. To test if you configured your DNS correctly, just navigate to [http://distributor.za.tryhackme.com/creds](http://distributor.za.tryhackme.com/creds). If you see the website, you are set up for the rest of the room.

  

## Requesting Your Credentials

To simulate an AD breach, you will be provided with your first set of AD credentials. Once your networking setup has been completed, on your Attack Box, navigate to [http://distributor.za.tryhackme.com/creds](http://distributor.za.tryhackme.com/creds) to request your credential pair. Click the "Get Credentials" button to receive your credential pair that can be used for initial access.

This credential pair will provide you SSH access to THMJMP2.za.tryhackme.com. THMJMP2 can be seen as a jump host into this environment, simulating a foothold that you have achieved. 

For SSH access, you can use the following command:

`ssh za\\<AD Username>@thmjmp2.za.tryhackme.com`


## A Note on Reverse Shells

If you are using the AttackBox and have joined other network rooms before, be sure to select the IP address assigned to the tunnel interface facing the `lateralmovementandpivoting` network as your ATTACKER_IP, or else your reverse shells/connections won't work properly. For your convenience, the interface attached to this network is called `lateralmovement`, so you should be able to get the right IP address by running `ip add show lateralmovement`:

This will be helpful whenever needing to do a reverse connection back to your attacker machine throughout the room.


