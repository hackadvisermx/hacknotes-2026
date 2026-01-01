
# Passwords - A Cracking Christmas

# Task 1 Introduction

With time between Easter and Christmas being destabilised, the once-quiet systems of _The Best Festival Company_ began showing traces of encrypted data buried deep within their servers. Sir Carrotbane, stumbled upon a series of locked PDF and ZIP files labelled _“North Pole Asset List.”_ Rumours spread that these could contain fragments of **Santa’s master gift registry**, critical information that could help Malhare control the festive balance between both worlds.

Sir Carrotbane sets out to crack the encryption, learning how weak passwords can expose even the most guarded secrets. Can the Elves adapt fast and prevent their secrets from being discovered?

## Learning Objectives

- How password-based encryption protects files such as PDFs and ZIP archives.
- Why weak passwords make encrypted files vulnerable.
- How attackers use dictionary and brute-force attacks to recover passwords.
- A hands-on exercise: cracking the password of an encrypted file to reveal its contents.
- The importance of using strong, complex passwords to defend against these attacks.

A few simple points to remember:

- The **strength of protection** depends almost entirely on the password. Short or common passwords can be guessed; long, random passwords are far harder to break.
- Different file formats use different algorithms and key derivation methods. For example, PDF encryption and ZIP encryption differ in details (how the key is derived, salt use, number of hash iterations). That affects how easy or hard cracking is.
- Many consumer tools still support legacy or weak modes (particularly older ZIP encryption). That makes some encrypted archives much easier to attack than modern, well-implemented schemes.
- Encryption protects data confidentiality only. It does not prevent someone with access to the encrypted file from trying to guess the password offline.

To make it simple, encryption makes the contents unreadable unless the correct password is known. If the password is weak, an attacker can simply try likely passwords until one works.

# Task 2 - Attacks Against Encrypted Files
## How Attackers Recover Weak Passwords

Attackers don't usually try to "break" the encryption itself because that would take far too long with modern cryptography. Instead, they focus on guessing the password that protects the file. The two most common ways of doing this are dictionary attacks and brute-force (or mask) attacks.

**Dictionary Attacks**

In a dictionary attack, the attacker uses a predefined list of potential passwords, known as a wordlist, and tests each one until the correct password is found. These wordlists often contain leaked passwords from previous breaches, common substitutions like **password123**, predictable combinations of names and dates, and other patterns that people frequently use. Because many users choose weak or common passwords, dictionary attacks are usually fast and highly effective.

**Mask Attacks**

Brute-force and mask attacks go one step further. A brute-force attack systematically tries every possible combination of characters until it finds the right one. While this guarantees success eventually, the time it takes grows exponentially with the length and complexity of the password.

Mask attacks aim to reduce that time by limiting guesses to a specific format. For example, trying all combinations of three lowercase letters followed by two digits.

By narrowing the search space, mask attacks strike a balance between speed and thoroughness, especially when the attacker has some idea of how the password might be structured.

Practical tips attackers use (and defenders should know about):

- Start with a wordlist (fast wins). Common lists: `rockyou.txt`, `common-passwords.txt`.
- If the wordlist fails, move to targeted wordlists (company names, project names, or data from the target).
- If that fails, try mask or incremental attacks on short passwords (e.g. `?l?l?l?d?d` = three lowercase letters + two digits, which is used as a password mask format by password cracking tools).
- Use GPU-accelerated cracking when possible; it dramatically speeds up attacks for some algorithms.
- Keep an eye on resource use: cracking is CPU/GPU intensive. That behaviour can be detected on a monitored endpoint.

## Exercise

You will find the files for this section in the `Desktop` directory of the machine. Switch to it by running `cd Desktop` in your terminal.

**1. Confirm the File Type**

Use the `file` command or open the file with a hex viewer. This helps pick the right tool.

```
ubuntu@tryhackme:~$ cd Desktop/
ubuntu@tryhackme:~/Desktop$ ls
flag.pdf  flag.zip  john  mate-terminal.desktop
ubuntu@tryhackme:~/Desktop$ file flag.pdf 
flag.pdf: PDF document, version 1.7, 1 page(s)
ubuntu@tryhackme:~/Desktop$ file flag.zip 
flag.zip: Zip archive data, at least v2.0 to extract, compression method=AES Encrypted
ubuntu@tryhackme:~/Desktop$ 
```

If it's a PDF, proceed with PDF tools. If it's a ZIP, proceed with ZIP tools.

**2. Tools to Use (pick one based on file type)**

- PDF: `pdfcrack`, `john` (via `pdf2john`)
- ZIP: `fcrackzip`, `john` (via `zip2john`)
- General: `john` (very flexible) and `hashcat` (GPU acceleration, more advanced)

**3. Try a Dictionary Attack First (fast, often successful)**

Example: PDF with `pdfcrack` and `rockyou.txt`:

```
pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt 
PDF version 1.7
Security Handler: Standard
V: 2
R: 3
P: -1060
Length: 128
Encrypted Metadata: True
FileID: 3792b9a3671ef54bbfef57c6fe61ce5d
U: c46529c06b0ee2bab7338e9448d37c3200000000000000000000000000000000
O: 95d0ad7c11b1e7b3804b18a082dda96b4670584d0044ded849950243a8a367ff
	found user-password: 'naughtylist'
```

Example: using `john` 

- Create a hash that John can understand: `zip2john flag.zip > ziphash.txt`

```
buntu@tryhackme:~/Desktop$ zip2john flag.zip > ziphash.txt > ziphash.txt

```

- John will report the recovered password if it finds one.
-
```
ubuntu@tryhackme:~/Desktop$ john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
Cost 1 (HMAC size [KiB]) is 1 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
winter4ever      (flag.zip/flag.txt)     
1g 0:00:00:00 DONE (2025-12-09 18:47) 1.923g/s 7876p/s 7876c/s 7876C/s friend..sahara
Use the "--show" option to display all of the cracked passwords reliably
Session completed

z x flag.zip 

7-Zip 23.01 (x64) : Copyright (c) 1999-2023 Igor Pavlov : 2023-06-20
 64-bit locale=C.UTF-8 Threads:2 OPEN_MAX:1024

Scanning the drive for archives:
1 file, 245 bytes (1 KiB)

Extracting archive: flag.zip
--
Path = flag.zip
Type = zip
Physical Size = 245

    
Enter password (will not be echoed):
Everything is Ok

Size:       29
Compressed: 245
ubuntu@tryhackme:~/Desktop$ cat flag.
cat: flag.: No such file or directory
ubuntu@tryhackme:~/Desktop$ cat flag.txt 
THM{Cr4ck1n6_z1p$_1s_34$yyyy}
```

## Detection of Indicators and Telemetry

Offline cracking does not hit login services, so lockouts and failed logon dashboards stay quiet. We can detect the work where it runs, on endpoints and jump boxes. The important signals to monitor include:

**Process creation:** Password cracking has a small set of well-known binaries and command patterns that we can look out for. A mix of process events, file activity, GPU signals, and network touches tied to tooling and wordlists. Our goal is to make the activity obvious without drowning in noise.

- Binaries and aliases: `john`, `hashcat`, `fcrackzip`, `pdfcrack`, `zip2john`, `pdf2john.pl`, `7z`, `qpdf`, `unzip`, `7za`, `perl` invoking `pdf2john.pl`.
- Command‑line traits: `--wordlist`, `-w`, `--rules`, `--mask`, `-a 3`, `-m` in Hashcat, references to `rockyou.txt`, `SecLists`, `zip2john`, `pdf2john`.
- Potfiles and state: `~/.john/john.pot`, `.hashcat/hashcat.potfile`, `john.rec`.

It's worth noting that on Windows systems, Sysmon Event ID 1 captures process creation with full command line properties, while on Linux, `auditd`, `execve`, or EDR sensors capture binaries and arguments.

**GPU and Resource Artefacts**

GPU cracking is loud. Sudden high utilisation on hosts can be picked up and would need to be investigated.

- `nvidia-smi` shows long‑running processes named `hashcat` or `john`.
- High, steady GPU utilisation and power draw while the fan curve spikes.
- Libraries loaded: `nvcuda.dll`, `OpenCL.dll`, `libcuda.so`, `amdocl64.dll`.

**Network Hints, Light but Useful**

Offline cracking does not need the network once wordlists are present. Yet most operators fetch lists and tools first.

- Downloads of large text files named `rockyou.txt`, or Git clones of popular wordlist repos.
- Package installs, for example `apt install john hashcat`, detected by EDR package telemetry.
- Tool updates and driver fetches for GPU runtimes.

**Unusual File Reads**

Repeated reads of files such as wordlists or encrypted files would need analysis.

**Detections**

Below are some examples of detection rules and hunting queries we can put to use across various environments.

_Sysmon_:

```EventID=1
(ProcessName="C:\Program Files\john\john.exe" OR
 ProcessName="C:\Tools\hashcat\hashcat.exe" OR
 CommandLine="*pdf2john.pl*" OR
 CommandLine="*zip2john*")
```

_Linux audit rules, temporary for an investigation:_

```bash
auditctl -w /usr/share/wordlists/rockyou.txt -p r -k wordlists_read
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/john -k crack_exec
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/hashcat -k crack_exec
```

_Sigma style rule, Windows process create for cracking tools:_

```yaml
title: Password Cracking Tools Execution
id: 9f2f4d3e-4c16-4b0a-bb3a-7b1c6c001234
status: experimental
logsource:
  product: windows
  category: process_creation
detection:
  selection_name:
    Image|endswith:
      - '\john.exe'
      - '\hashcat.exe'
      - '\fcrackzip.exe'
      - '\pdfcrack.exe'
      - '\7z.exe'
      - '\qpdf.exe'
  selection_cmd:
    CommandLine|contains:
      - '--wordlist'
      - 'rockyou.txt'
      - 'zip2john'
      - 'pdf2john'
      - '--mask'
      - ' -a 3'
  condition: selection_name or selection_cmd
level: medium
```

**Response Playbook**

As security analysts in Wareville, it is important to have a playbook to follow when such incidents occur. The immediate actions to take are:

1. Isolate the host if malicious activity is detected. If it is a lab, tag and suppress.
2. Capture triage artefacts such as process list, process memory dump, `nvidia-smi` sample output, open files, and the encrypted file.
3. Preserve the working directory, wordlists, hash files, and shell history.
4. Review which files were decrypted. Search for follow‑on access, lateral movement or exfiltration.
5. Identify the origin and intent of the activity. Was this authorised? If not, escalate to the IR team.
6. Remediate the activity, rotate affected keys and passwords, and enforce MFA for accounts.
7. Close with education and correct placement of tools into approved sandboxes.



## Answer the questions below

### What is the flag inside the encrypted PDF?

THM{Cr4ck1ng_PDFs_1s_34$y}

### What is the flag inside the encrypted zip file?

THM{Cr4ck1n6_z1p$_1s_34$yyyy}

### For those who want another challenge, have a look around the VM to get access to the key for **Side Quest 2**! Accessible through our [Side Quest Hub](https://tryhackme.com/adventofcyber25/sidequest)!



```
/snap/john-the-ripper/694/bin/keepass2john .Passwords.kdbx > kepass.hash
ubuntu@tryhackme:~$ john --wordlist=/usr/share/wordlists/rockyou.txt --format=kepass kepass.hash 
Error: No format matched requested name 'kepass'
ubuntu@tryhackme:~$ john --wordlist=/usr/share/wordlists/rockyou.txt --format=keepass kepass.hash 
Using default input encoding: UTF-8
Loaded 1 password hash (KeePass [AES/Argon2 256/256 AVX2])
Cost 1 (t (rounds)) is 20 for all loaded hashes
Cost 2 (m) is 65536 for all loaded hashes
Cost 3 (p) is 2 for all loaded hashes
Cost 4 (KDF [0=Argon2d 2=Argon2id 3=AES]) is 0 for all loaded hashes
Will run 2 OpenMP threads
Note: Passwords longer than 41 [worst case UTF-8] to 124 [ASCII] rejected
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
Failed to use huge pages (not pre-allocated via sysctl? that's fine)
0g 0:00:00:57 0.00% (ETA: 2026-04-27 09:27) 0g/s 1.455p/s 1.455c/s 1.455C/s benfica..love123
0g 0:00:00:59 0.00% (ETA: 2026-04-29 07:17) 0g/s 1.454p/s 1.454c/s 1.454C/s 696969..asdfgh
harrypotter      (.Passwords)     
1g 0:00:01:06 DONE (2025-12-09 19:03) 0.01510g/s 1.449p/s 1.449c/s 1.449C/s harrypotter..ihateyou
Use the "--show" option to display all of the cracked passwords reliably
Session completed

harrypotter 
```

```
keepassxc-cli show /home/ubuntu/.Passwords.kdbx Key
Enter password to unlock /home/ubuntu/.Passwords.kdbx: 
Title: Key
UserName: 
Password: PROTECTED
URL: 
Notes: 
Uuid: {368ed39e-b162-44cd-b8aa-13093233202a}
Tags: 

keepassxc
Abrir con cliente grafico y ver el attach: tit_for_tat
```