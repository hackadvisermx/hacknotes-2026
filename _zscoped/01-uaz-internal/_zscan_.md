

## Conectar a la vpn con el cliente openvpn

```
openvpn --config client.ovpn --data-ciphers AES-256-GCM:AES-128-GCM:CHACHA20-POLY1305:AES-256-CBC
```


```
 nmap -p445 -n -Pn --open --script smb-os-discovery 10.1.1.1/16 -vv -oA xdata
```

```
naabu -host 10.1.0.0/16 -p 445 -c 30 -rate 5000 -nmap-cli 'nmap --script smb-os-discovery' -o uaz1
```