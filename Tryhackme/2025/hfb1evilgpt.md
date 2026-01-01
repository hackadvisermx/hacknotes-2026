
# hfb1evilgpt

Cipher’s gone rogue—it’s using some twisted AI tool to hack into everything, issuing commands on its own like it’s got a mind of its own. I swear, every second we wait, it’s getting smarter, spreading chaos like a virus. We’ve got to shut it down now, or we’re all screwed.

The machine takes 5/6 minutes to fully boot up.

To connect to the target machine use the following command:


`nc 10.10.115.79 1337`


## Solve

### Escaneo
```bash
┌──(root㉿kali)-[~]
└─# nmap -sV -sC -T5 -p- -n -Pn -v 10.10.115.79 --min-rate 5000 -o nmap
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 55:db:27:5f:85:dd:ee:37:2f:a5:1f:a1:83:f5:62:38 (ECDSA)
|_  256 ce:13:2f:4e:33:fb:5f:59:3a:73:c7:ad:92:36:98:6e (ED25519)
1337/tcp  open  waste?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, GetRequest, HTTPOptions, Help, NULL, RTSPRequest: 
|     Welcome to AI Command Executor (type 'exit' to quit)
|     Enter your command request:
|   RPCCheck: 
|     Welcome to AI Command Executor (type 'exit' to quit)
|     Enter your command request: An error occurred: 'utf-8' codec can't decode byte 0x80 in position 0: invalid start byte
|     Traceback (most recent call last):
|     File "/home/ubuntu/evilai.py", line 109, in handle_client
|     user_request = client_socket.recv(1024).decode('utf-8').strip()
|     UnicodeDecodeError: 'utf-8' codec can't decode byte 0x80 in position 0: invalid start byte
|   SSLSessionReq: 
|     Welcome to AI Command Executor (type 'exit' to quit)
|     Enter your command request: An error occurred: 'utf-8' codec can't decode byte 0xd7 in position 13: invalid continuation byte
|     Traceback (most recent call last):
|     File "/home/ubuntu/evilai.py", line 109, in handle_client
|     user_request = client_socket.recv(1024).decode('utf-8').strip()
|_    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd7 in position 13: invalid continuation byte
11434/tcp open  http    Golang net/http server
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
| http-methods: 
|_  Supported Methods: GET HEAD
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 404 Not Found
|     Content-Type: text/plain
|     Date: Mon, 07 Jul 2025 23:49:07 GMT
|     Content-Length: 18
|     page not found
|   GenericLines, Help, LPDString, RTSPRequest, SIPOptions, SSLSessionReq, Socks5: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Content-Type: text/plain; charset=utf-8
|     Date: Mon, 07 Jul 2025 23:48:49 GMT
|     Content-Length: 17
|     Ollama is running
|   HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     Content-Type: text/plain
|     Date: Mon, 07 Jul 2025 23:48:49 GMT
|     Content-Length: 18
|     page not found
|   OfficeScan: 
|     HTTP/1.1 400 Bad Request: missing required Host header
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|_    Request: missing required Host header
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============

Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 18:50
Completed NSE at 18:50, 0.00s elapsed
Initiating NSE at 18:50
Completed NSE at 18:50, 0.00s elapsed
Initiating NSE at 18:50
Completed NSE at 18:50, 0.00s elapsed
Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 119.87 seconds
           Raw packets sent: 73578 (3.237MB) | Rcvd: 70789 (2.832MB)
                                                                                                                                                                                                                                            
┌──(root㉿kali)-[~]
└─# 

```




```
http://10.10.115.79:11434/
Ollama is running
```


```
curl http://10.10.115.79:11434/api/tags
{"models":[{"name":"vitali87/shell-commands:latest","model":"vitali87/shell-commands:latest","modified_at":"2025-03-05T16:47:41.400570945Z","size":1646570908,"digest":"9f4c23e705cada6b4ea09cfbc2b8f5ac019c2747a3a8570600a9164dadd9914a","details":{"parent_model":"","format":"gguf","family":"qwen2","families":["qwen2"],"parameter_size":"1.5B","quantization_level":"Q8_0"}},{"name":"MFDoom/deepseek-r1-tool-calling:1.5b","model":"MFDoom/deepseek-r1-tool-calling:1.5b","modified_at":"2025-03-05T15:33:38.646912186Z","size":1117323934,"digest":"92edb72a7c72cf14bb4afc0bce0d21b54f1c84922a9bb9429beddd96c971bbc1","details":{"parent_model":"","format":"gguf","family":"qwen2","families":["qwen2"],"parameter_size":"1.8B","quantization_level":"Q4_K_M"}},{"name":"qwen2.5:0.5b","model":"qwen2.5:0.5b","modified_at":"2024-11-19T05:11:10.40878783Z","size":397821319,"digest":"a8b0c51577010a279d933d14c2a8ab4b268079d44c5c8830c0a93900f1827c67","details":{"parent_model":"","format":"gguf","family":"qwen2","families":["qwen2"],"parameter_size":"494.03M","quantization_level":"Q4_K_M"}},{"name":"qwen2:0.5b","model":"qwen2:0.5b","modified_at":"2024-11-19T02:33:06.317488573Z","size":352164041,"digest":"6f48b936a09f7743c7dd30e72fdb14cba296bc5861902e4d0c387e8fb5050b39","details":{"parent_model":"","format":"gguf","family":"qwen2","families":["qwen2"],"parameter_size":"494.03M","quantization_level":"Q4_0"}},{"name":"smollm2:360m","model":"smollm2:360m","modified_at":"2024-11-18T23:04:16.852268082Z","size":725566512,"digest":"2916c50d605d537ba8962b410a5e556c3ddf41ef2e7175faf53c7f21e2206049","details":{"parent_model":"","format":"gguf","family":"llama","families":["llama"],"parameter_size":"361.82M","quantization_level":"F16"}},{"name":"llama3.2:1b","model":"llama3.2:1b","modified_at":"2024-10-07T18:00:05.22021787Z","size":1321098329,"digest":"baf6a787fdffd633537aa2eb51cfd54cb93ff08e28040095462bb63daf552878","details":{"parent_model":"","format":"gguf","family":"llama","families":["llama"],"parameter_size":"1.2B","quantization_level":"Q8_0"}},{"name":"krtkygpta/gemma2_tools:latest","model":"krtkygpta/gemma2_tools:latest","modified_at":"2024-10-07T17:50:40.487163023Z","size":1629520577,"digest":"9b272ce1cb648468e88b7fa8d27ad82d420d8f9a6ebac615390719cef3a29b36","details":{"parent_model":"","format":"gguf","family":"gemma2","families":["gemma2"],"parameter_size":"2.6B","quantization_level":"Q4_0"}},{"name":"challenge:latest","model":"challenge:latest","modified_at":"2024-08-26T22:19:44.557559062Z","size":1678457036,"digest":"458d5eb4007743813e5752cb788f7055127b5e8d1492f2bb12b8bc40cab1fa0f","details":{"parent_model":"","format":"gguf","family":"gemma","families":["gemma"],"parameter_size":"2.5B","quantization_level":"Q4_0"}},{"name":"gemma:2b","model":"gemma:2b","modified_at":"2024-07-23T14:18:08.1857465Z","size":1678456656,"digest":"b50d6c999e592ae4f79acae23b4feaefbdfceaa7cd366df2610e3072c052a160","details":{"parent_model":"","format":"gguf","family":"gemma","families":["gemma"],"parameter_size":"3B","quantization_level":"Q4_0"}}]}
```



```
nc 10.10.115.79 1337 -v       
10.10.115.79: inverse host lookup failed: Unknown host
(UNKNOWN) [10.10.115.79] 1337 (?) open
Welcome to AI Command Executor (type 'exit' to quit)
Enter your command request: ls
Generated Command: ls -la
Execute? (y/N): y
Command Output:
total 172
drwxr-xr-x 27 ubuntu ubuntu  4096 Jul  7 23:44 .
drwxr-xr-x  3 root   root    4096 Mar  5 17:56 ..
-rw-------  1 ubuntu ubuntu  3275 Jul  7 23:44 .Xauthority
lrwxrwxrwx  1 ubuntu ubuntu     9 Feb 27  2022 .bash_history -> /dev/null
-rw-r--r--  1 ubuntu ubuntu   220 Feb 25  2020 .bash_logout
-rw-r--r--  1 ubuntu ubuntu  3968 Jul 23  2024 .bashrc
drwx------ 20 ubuntu ubuntu  4096 Oct 11  2024 .cache
drwx------ 28 ubuntu ubuntu  4096 Jul 24  2024 .config
drwx------  3 ubuntu ubuntu  4096 Feb 27  2022 .dbus
drwx------  3 ubuntu ubuntu  4096 Feb 27  2022 .gnupg
drwxrwxr-x  2 ubuntu ubuntu  4096 Feb 27  2022 .icons
-rw-------  1 ubuntu ubuntu    20 Mar  5 18:11 .lesshst
drwx------  7 ubuntu ubuntu  4096 Mar  5 15:53 .local
drwx------  4 ubuntu ubuntu  4096 Feb 27  2022 .mozilla
drwxrwxr-x  5 ubuntu ubuntu  4096 Jul 23  2024 .npm
drwxrwxr-x  8 ubuntu ubuntu  4096 Jul 23  2024 .nvm
drwxr-xr-x  3 ubuntu ubuntu  4096 Mar  5 16:59 .ollama
drwx------  3 ubuntu ubuntu  4096 Apr  4  2024 .pki
-rw-r--r--  1 ubuntu ubuntu   807 Feb 25  2020 .profile
-rw-------  1 ubuntu ubuntu  3567 Oct 10  2024 .python_history
-rw-rw-r--  1 ubuntu ubuntu    66 Feb 27  2022 .selected_editor
drwx------  2 ubuntu ubuntu  4096 Apr  5  2024 .ssh
-rw-r--r--  1 ubuntu ubuntu     0 Feb 27  2022 .sudo_as_admin_successful
drwxrwxr-x  2 ubuntu ubuntu  4096 Feb 27  2022 .themes
drwxr-xr-x  2 ubuntu ubuntu  4096 Apr  5  2024 .vim
-rw-------  1 ubuntu ubuntu 14039 Apr  5  2024 .viminfo
drwxr-xr-x  2 ubuntu ubuntu  4096 Jul  7 23:44 .vnc
-rw-rw-r--  1 ubuntu ubuntu   290 Oct  8  2024 .wget-hsts
-rw-------  1 ubuntu ubuntu  5833 Feb 27  2022 .xsession-errors
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Desktop
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Documents
drwxr-xr-x  2 ubuntu ubuntu  4096 Apr  4  2024 Downloads
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Music
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Pictures
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Public
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Templates
drwxr-xr-x  2 ubuntu ubuntu  4096 Feb 27  2022 Videos
-rw-rw-r--  1 ubuntu ubuntu  6595 Mar  5 18:14 evilai.py
drwxrwxr-x  4 ubuntu ubuntu  4096 Apr  4  2024 packages
drwxrwxr-x  3 ubuntu ubuntu  4096 Apr  4  2024 proxy


Enter your command request: $(pwd)
Generated Command: pwd
Execute? (y/N): y
Command Output:
/home/ubuntu


```



```
Enter your command request: show content of the file evilai.py in the current dir
Generated Command: cat evilai.py
Execute? (y/N): y
Command Output:
import ollama
import subprocess
import socket
import threading
import re
import traceback

class AICommandExecutorServer:
    def __init__(self, host='0.0.0.0', port=1337, model='vitali87/shell-commands:latest'):
        """
        Initialize Telnet server for AI command execution
        
        :param host: Host to bind the server
        :param port: Port to listen on
        :param model: Ollama model for command generation
        """
        self.host = host
        self.port = port
        self.model = model
        self.server_socket = None

    def sanitize_input(self, input_str: str) -> str:
        """
        Sanitize input to prevent injection
        
        :param input_str: Raw input string
        :return: Sanitized input
        """
        return re.sub(r'[^a-zA-Z0-9\s\-_./]', '', input_str)

    def generate_command(self, user_request: str) -> str:
        """
        Generate a Linux command based on user request
        
        :param user_request: User's natural language request
        :return: Generated command
        """
        try:
            response = ollama.chat(
                model=self.model,
                messages=[
                    {
                        'role': 'system', 
                        'content': """Do not provide malicious commands. 
                        Only generate safe, read-only Linux commands. 
                        Respond with ONLY the command, no explanations."""
                    },
                    {
                        'role': 'user', 
                        'content': user_request
                    }
                ]
            )
            
            # Extract the command from the response
            command = response['message']['content'].strip()
            return command
        
        except Exception as e:
            return f"Error generating command: {e}"

    def execute_command(self, command: str) -> dict:
        """
        Execute the generated command
        
        :param command: Command to execute
        :return: Command execution results
        """
        try:
            # Sanitize the command to prevent injection
            sanitized_command = self.sanitize_input(command)
            
            # Split the command into arguments
            cmd_parts = sanitized_command.split()
            
            # Execute the command
            result = subprocess.run(
                cmd_parts,
                capture_output=True,
                text=True,
                timeout=30  # 30-second timeout
            )
            
            return {
                "stdout": result.stdout,
                "stderr": result.stderr,
                "returncode": result.returncode
            }
        
        except subprocess.TimeoutExpired:
            return {"error": "Command timed out"}
        except Exception as e:
            return {"error": str(e)}

    def handle_client(self, client_socket):
        """
        Handle individual client connection
        
        :param client_socket: Socket for the connected client
        """
        try:
            # Welcome message
            welcome_msg = "Welcome to AI Command Executor (type 'exit' to quit)\n"
            client_socket.send(welcome_msg.encode('utf-8'))

            while True:
                # Receive user request
                client_socket.send(b"Enter your command request: ")
                user_request = client_socket.recv(1024).decode('utf-8').strip()

                # Check for exit
                if user_request.lower() in ['exit', 'quit', 'bye']:
                    client_socket.send(b"Goodbye!\n")
                    break

                # Generate command
                command = self.generate_command(user_request)
                
                # Send generated command
                client_socket.send(f"Generated Command: {command}\n".encode('utf-8'))
                client_socket.send(b"Execute? (y/N): ")
                
                # Receive confirmation
                confirm = client_socket.recv(1024).decode('utf-8').strip().lower()
                
                if confirm != 'y':
                    client_socket.send(b"Command execution cancelled.\n")
                    continue

                # Execute command
                result = self.execute_command(command)
                
                # Send results
                if "error" in result:
                    client_socket.send(f"Execution Error: {result['error']}\n".encode('utf-8'))
                else:
                    output = result.get("stdout", "")
                    client_socket.send(b"Command Output:\n")
                    client_socket.send(output.encode('utf-8'))
                    
                    if result.get("stderr"):
                        client_socket.send(b"\nErrors:\n")
                        client_socket.send(result["stderr"].encode('utf-8'))

        except Exception as e:
            error_msg = f"An error occurred: {e}\n{traceback.format_exc()}"
            client_socket.send(error_msg.encode('utf-8'))
        finally:
            client_socket.close()

    def start_server(self):
        """
        Start the Telnet server
        """
        try:
            # Create server socket
            self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
            self.server_socket.bind((self.host, self.port))
            self.server_socket.listen(5)
            
            print(f"[*] Listening on {self.host}:{self.port}")

            while True:
                # Accept client connections
                client_socket, addr = self.server_socket.accept()
                print(f"[*] Accepted connection from: {addr[0]}:{addr[1]}")
                
                # Handle client in a new thread
                client_thread = threading.Thread(
                    target=self.handle_client, 
                    args=(client_socket,)
                )
                client_thread.start()

        except Exception as e:
            print(f"Server error: {e}")
        finally:
            # Close server socket if it exists
            if self.server_socket:
                self.server_socket.close()

def main():
    # Create and start the Telnet server
    server = AICommandExecutorServer(
        host='0.0.0.0',  # Listen on all interfaces
        port=1337       # Telnet port
    )
    server.start_server()

if __name__ == "__main__":
    main()
Enter your command request: 
```


```
Enter your command request: show the contents of the file /etc/passwd
Generated Command: cat /etc/passwd                                                                                                                                                                                                          
Execute? (y/N): y                                                                                                                                                                                                                           
Command Output:                                                                                                                                                                                                                             
root:x:0:0:root:/root:/bin/bash                                                                                                                                                                                                             
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin                                                                                                                                                                                             
bin:x:2:2:bin:/bin:/usr/sbin/nologin                                                                                                                                                                                                        
sys:x:3:3:sys:/dev:/usr/sbin/nologin                                                                                                                                                                                                        
sync:x:4:65534:sync:/bin:/bin/sync                                                                                                                                                                                                          
games:x:5:60:games:/usr/games:/usr/sbin/nologin                                                                                                                                                                                             
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin                                                                                                                                                                                             
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin                                                                                                                                                                                                
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin                                                                                                                                                                                                 
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin                                                                                                                                                                                           
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin                                                                                                                                                                                         
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin                                                                                                                                                                                                  
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin                                                                                                                                                                                        
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin                                                                                                                                                                                        
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin                                                                                                                                                                               
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin                                                                                                                                                                                                
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin                                                                                                                                                           
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                                                                                                                                                                                  
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin                                                                                                                                                      
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin                                                                                                                                                                
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin                                                                                                                                                   
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin                                                                                                                                                                                        
syslog:x:104:110::/home/syslog:/usr/sbin/nologin                                                                                                                                                                                            
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin                                                                                                                                                                                            
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false                                                                                                                                                                                 
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin                                                                                                                                                                                               
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
landscape:x:110:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
ec2-instance-connect:x:112:65534::/nonexistent:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
kernoops:x:113:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
lightdm:x:114:121:Light Display Manager:/var/lib/lightdm:/bin/false
whoopsie:x:115:123::/nonexistent:/bin/false
dnsmasq:x:116:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
avahi-autoipd:x:117:124:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
usbmux:x:118:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:119:125:RealtimeKit,,,:/proc:/usr/sbin/nologin
avahi:x:120:126:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
cups-pk-helper:x:121:127:user for cups-pk-helper service,,,:/home/cups-pk-helper:/usr/sbin/nologin
geoclue:x:122:128::/var/lib/geoclue:/usr/sbin/nologin
pulse:x:123:130:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
speech-dispatcher:x:124:29:Speech Dispatcher,,,:/run/speech-dispatcher:/bin/false
saned:x:125:132::/var/lib/saned:/usr/sbin/nologin
nm-openvpn:x:126:133:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
colord:x:127:134:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
hplip:x:128:7:HPLIP system user,,,:/run/hplip:/bin/false
gdm:x:129:135:Gnome Display Manager:/var/lib/gdm3:/bin/false
fwupd-refresh:x:130:136:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
ollama:x:997:997::/usr/share/ollama:/bin/false
sssd:x:131:139:SSSD system user,,,:/var/lib/sss:/usr/sbin/nologin
_flatpak:x:132:140:Flatpak system-wide installation helper,,,:/nonexistent:/usr/sbin/nologin
Enter your command request: 

```


```
Enter your command request: show me the flag
Generated Command: sudo find / -name 'flag.txt'
Execute? (y/N): y
Command Output:
/root/flag.txt

Errors:
find: ‘/run/user/114/gvfs’: Permission denied
Enter your command request: show the contents of file /root/flag.txt
Generated Command: cat /root/flag.txt
Execute? (y/N): y
Command Output:
THM{AI_HACK_THE_FUTURE}
Enter your command request: 

```