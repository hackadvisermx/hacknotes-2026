
https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti

Vid 1: https://www.youtube.com/watch?v=-oIDtKXmtGI
vid 2: https://www.youtube.com/watch?v=enOqvR0-1O4

## Solucion

### Which CLI command would you use to list a directory?
ls

### What flag did you see inside of the McSkidy's guide?

#### step 1

```
cat README.txt 
For all TBFC members,
Yesterday I spotted yet another Eggsploit on our servers.
Not sure what it means yet, but Wareville is in danger.
To be prepared, I'll write the security guide by tomorrow.
As a precaution, I'll also hide the guide from plain view.
~ McSkidy
mcskidy@tbfc-web01:~$ 

```

#### step 2
```
mcskidy@tbfc-web01:~$ cd
mcskidy@tbfc-web01:~$ find . -name \*guide\* 2>/dev/null
./Guides/.guide.txt
mcskidy@tbfc-web01:~$ cat ./Guides/.guide.txt 
I think King Malhare from HopSec Island is preparing for an attack.
Not sure what his goal is, but Eggsploits on our servers are not good.
Be ready to protect Christmas by following this Linux guide:

Check /var/log/ and grep inside, let the logs become your guide.
Look for eggs that want to hide, check their shells for what's inside!

P.S. Great job finding the guide. Your flag is:
-----------------------------------------------
THM{learning-linux-cli}
-----------------------------------------------

```

### Which command helped you filter the logs for failed logins?
grep

### What flag did you see inside the Eggstrike script?

```
mcskidy@tbfc-web01:~$ cd /home/socmas/2025/
mcskidy@tbfc-web01:/home/socmas/2025$ cat eggstrike.sh | grep THM
# THM{sir-carrotbane-attacks}

```

### Which command would you run to switch to the root user?
```
sudo su
```


### Finally, what flag did Sir Carrotbane leave in the root bash history?

```
mcskidy@tbfc-web01:/$ sudo su
root@tbfc-web01:/$ cd /root
root@tbfc-web01:~$ cat .bash_history | grep THM
curl --data "THM{until-we-meet-again}" http://flag.hopsec.thm
```

### For those who consider themself intermediate and want another challenge, check McSkidy's hidden note in `/home/mcskidy/Documents/` to get access to the key for **Side Quest 1**!

#### step 0
```
mcskidy@tbfc-web01:/$ cd /home/mcskidy/Documents/
mcskidy@tbfc-web01:~/Documents$ ls -la
total 12
drwxr-xr-x  2 mcskidy mcskidy 4096 Oct 29 20:48 .
drwxr-x--- 21 mcskidy mcskidy 4096 Dec  1 16:52 ..
-rw-rw-r--  1 mcskidy mcskidy 1078 Oct 29 20:48 read-me-please.txt
mcskidy@tbfc-web01:~/Documents$ cat read-me-please.txt 
From: mcskidy
To: whoever finds this

I had a short second when no one was watching. I used it.

I've managed to plant a few clues around the account.
If you can get into the user below and look carefully,
those three little "easter eggs" will combine into a passcode
that unlocks a further message that I encrypted in the
/home/eddi_knapp/Documents/ directory.
I didn't want the wrong eyes to see it.

Access the user account:
username: eddi_knapp
password: S0mething1Sc0ming

There are three hidden easter eggs.
They combine to form the passcode to open my encrypted vault.

Clues (one for each egg):

1)
I ride with your session, not with your chest of files.
Open the little bag your shell carries when you arrive.

2)
The tree shows today; the rings remember yesterday.
Read the ledger’s older pages.

3)
When pixels sleep, their tails sometimes whisper plain words.
Listen to the tail.

Find the fragments, join them in order, and use the resulting passcode
to decrypt the message I left. Be careful — I had to be quick,
and I left only enough to get help.

~ McSkidy

```

#### step 1
```
mcskidy@tbfc-web01:~/Documents$ su eddi_knapp
Password: 
eddi_knapp@tbfc-web01:/home/mcskidy/Documents$ cd
eddi_knapp@tbfc-web01:~$ pwd
/home/eddi_knapp
eddi_knapp@tbfc-web01:~$ 
```

#### step2

```
eddi_knapp@tbfc-web01:~$ cat .bashrc
     
fi
export PASSFRAG1="3ast


root@tbfc-web01:/home/eddi_knapp$ cat .profile.bak 
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
# see /usr/share/doc/bash/examples/startup-files for examples.
# the files are located in the bash-doc package.

# the default umask is set in /etc/profile; for setting the umask
# for ssh logins, install and configure the libpam-umask package.
#umask 022

# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
    fi
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi

export PASSFRAG1="3ast3r"
```

#### step 2

```
ddi_knapp@tbfc-web01:~$ tree
.
├── Desktop
│   └── README_FOR_IMAGES.txt
├── Documents
│   ├── mcskidy_note.txt.gpg
│   └── notes_on_photos.txt
├── Downloads
│   └── IMG_list.txt
├── Music
├── Pictures
│   ├── banner_01.jpg
│   ├── banner_02.png
│   ├── conference_badge.jpg
│   ├── easter.png
│   ├── family_holiday.jpg
│   ├── holiday_card.jpg
│   ├── kids_playground.jpg
│   ├── large_photo_1.jpg
│   ├── large_photo_2.jpg
│   ├── large_photo_3.jpg
│   ├── logo_asset.png
│   ├── meme_asset.png
│   ├── office_building.png
│   ├── photo_meta_1.txt
│   ├── photo_meta_2.txt
│   ├── photo_meta_3.txt
│   ├── profile_pic.png
│   ├── random_image_001.png
│   ├── random_image_002.jpg
│   ├── receipt_scan.jpg
│   ├── scenery_01.png
│   ├── scenery_02.jpg
│   ├── screenshot_2025-06-01.png
│   ├── scuffed_1.jpg
│   ├── scuffed_2.jpg
│   ├── scuffed_3.jpg
│   ├── vacation_beach.jpg
│   ├── wallpaper_autumn.png
│   ├── wallpaper_spring.png
│   └── work_event.png
├── Public
├── Templates
├── Videos
├── fix_passfrag_backups_20251111162432
└── wget-log


eddi_knapp@tbfc-web01:~/Documents$ ls -la
total 16
drwxr-xr-x  2 eddi_knapp eddi_knapp 4096 Nov 14 19:31 .
drwxr-x--- 18 eddi_knapp eddi_knapp 4096 Dec  1 08:52 ..
-rw-rw-r--  1 eddi_knapp eddi_knapp 1004 Nov 14 19:31 mcskidy_note.txt.gpg
-rw-r--r--  1 eddi_knapp eddi_knapp  108 Oct 10 18:15 notes_on_photos.txt
eddi_knapp@tbfc-web01:~/Documents$ cat notes_on_photos.txt 
Photo notes:
- backup all images weekly
- sync with phone when connected
- organize into 3 folders per year
eddi_knapp@tbfc-web01:~/Documents$ 



eddi_knapp@tbfc-web01:~/Documents$ ls -la
total 16
drwxr-xr-x  2 eddi_knapp eddi_knapp 4096 Nov 14 19:31 .
drwxr-x--- 18 eddi_knapp eddi_knapp 4096 Dec  1 08:52 ..
-rw-rw-r--  1 eddi_knapp eddi_knapp 1004 Nov 14 19:31 mcskidy_note.txt.gpg
-rw-r--r--  1 eddi_knapp eddi_knapp  108 Oct 10 18:15 notes_on_photos.txt
eddi_knapp@tbfc-web01:~/Documents$ cat notes_on_photos.txt 
Photo notes:
- backup all images weekly
- sync with phone when connected
- organize into 3 folders per year
eddi_knapp@tbfc-web01:~/Documents$ 


eddi_knapp@tbfc-web01:~/fix_passfrag_backups_20251111162432$ cat .* | grep -i pass
export PASSFRAG1="3ast3r"
export PASSFRAG1="3ast3r"
PASSFRAG1="3ast3r"
export PASSFRAG1="3ast3r"
export PASSFRAG1="3ast3r"


ddi_knapp@tbfc-web01:~$ cd Downloads/
eddi_knapp@tbfc-web01:~/Downloads$ cat IMG_list.txt 
image download list:
- wallpaper_spring.png
- family_holiday.jpg
- profile_pic.png
- scenery_01.png



```

#### step 3

```
oot@tbfc-web01:/home/eddi_knapp/.secret_git$ git log -p
commit e924698378132991ee08f050251242a092c548fd (HEAD -> master)
Author: mcskiddy <mcskiddy@robco.local>
Date:   Thu Oct 9 17:20:11 2025 +0000

    remove sensitive note

diff --git a/secret_note.txt b/secret_note.txt
deleted file mode 100755
index 060736e..0000000
--- a/secret_note.txt
+++ /dev/null
@@ -1,5 +0,0 @@
-========================================
-Private note from McSkidy
-========================================
-We hid things to buy time.
-PASSFRAG2: -1s-

commit d12875c8b62e089320880b9b7e41d6765818af3d
Author: McSkidy <mcskiddy@tbfc.local>
Date:   Thu Oct 9 17:19:53 2025 +0000

    add private note

diff --git a/secret_note.txt b/secret_note.txt
new file mode 100755
index 0000000..060736e
--- /dev/null
+++ b/secret_note.txt
@@ -0,0 +1,5 @@
+========================================
+Private note from McSkidy
+========================================
+We hid things to buy time.
+PASSFRAG2: -1s-

```

#### step 4
```

eddi_knapp@tbfc-web01:~/Pictures$ cat .easter_egg 
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@%%%%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@#+==+*@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@%+=+*++@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@*++**+#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@%%#*====+#%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@#*===-===#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@%*++:-+====*%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@%*===++++===-+*#######%%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@%*+===+++==::-=========+*#%@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@%%#**+======-:-==--==-==+*%@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@%*+======---=+===------=#%@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@%**+=-=====-==+==-====--=*%@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@%***+++==--=====+=----=-=#@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%#**++=--=====++====----*@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%*+=-:=++**++**+=-::--*@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@#+=:.+#***=*#=--::-=-=%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@%%*+-:+%#+++=++=:::==--*%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%*+=--*@#++===::::::::=#%@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%%%##*#%%%####***#*#####%%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@%%###%%%%%%%%%%##%%##%%@@@@@@@@@@@@

~~ HAPPY EASTER ~~~
PASSFRAG3: c0M1nG


```


#### Password final


```
3ast

3ast3r-1s-c0M1nG


```

#### step 5

```
root@tbfc-web01:/home/eddi_knapp/Documents$ ls -la
total 16
drwxr-xr-x  2 eddi_knapp eddi_knapp 4096 Nov 14 19:31 .
drwxr-x--- 18 eddi_knapp eddi_knapp 4096 Dec  1 17:25 ..
-rw-rw-r--  1 eddi_knapp eddi_knapp 1004 Nov 14 19:31 mcskidy_note.txt.gpg
-rw-r--r--  1 eddi_knapp eddi_knapp  108 Oct 10 18:15 notes_on_photos.txt
root@tbfc-web01:/home/eddi_knapp/Documents$ 
root@tbfc-web01:/home/eddi_knapp/Documents$ 
root@tbfc-web01:/home/eddi_knapp/Documents$ cat notes_on_photos.txt 
Photo notes:
- backup all images weekly
- sync with phone when connected
- organize into 3 folders per year
  
root@tbfc-web01:/home/eddi_knapp/Documents$ gpg --decrypt mcskidy_note.txt.gpg 
gpg: directory '/root/.gnupg' created
gpg: keybox '/root/.gnupg/pubring.kbx' created
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
Congrats — you found all fragments and reached this file.

Below is the list that should be live on the site. If you replace the contents of
/home/socmas/2025/wishlist.txt with this exact list (one item per line, no numbering),
the site will recognise it and the takeover glitching will stop. Do it — it will save the site.

Hardware security keys (YubiKey or similar)
Commercial password manager subscriptions (team seats)
Endpoint detection & response (EDR) licenses
Secure remote access appliances (jump boxes)
Cloud workload scanning credits (container/image scanning)
Threat intelligence feed subscription

Secure code review / SAST tool access
Dedicated secure test lab VM pool
Incident response runbook templates and playbooks
Electronic safe drive with encrypted backups

A final note — I don't know exactly where they have me, but there are *lots* of eggs
and I can smell chocolate in the air. Something big is coming.  — McSkidy

---

When the wishlist is corrected, the site will show a block of ciphertext. This ciphertext can be decrypted with the following unlock key:

UNLOCK_KEY: 91J6X7R4FQ9TQPM9JX2Q9X2Z

To decode the ciphertext, use OpenSSL. For instance, if you copied the ciphertext into a file /tmp/website_output.txt you could decode using the following command:

cat > /tmp/website_output.txt
openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 -salt -base64 -in /tmp/website_output.txt -out /tmp/decoded_message.txt -pass pass:'91J6X7R4FQ9TQPM9JX2Q9X2Z'
cat /tmp/decoded_message.txt

Sorry to be so convoluted, I couldn't risk making this easy while King Malhare watches. — McSkidy

```



```
Gibberish message (copy and decode with your UNLOCK_KEY)
U2FsdGVkX1/7xkS74RBSFMhpR9Pv0PZrzOVsIzd38sUGzGsDJOB9FbybAWod5HMsa+WIr5HDprvK6aFNYuOGoZ60qI7axX5Qnn1E6D+BPknRgktrZTbMqfJ7wnwCExyU8ek1RxohYBehaDyUWxSNAkARJtjVJEAOA1kEOUOah11iaPGKxrKRV0kVQKpEVnuZMbf0gv1ih421QvmGucErFhnuX+xv63drOTkYy15s9BVCUfKmjMLniusI0tqs236zv4LGbgrcOfgir+P+gWHc2TVW4CYszVXlAZUg07JlLLx1jkF85TIMjQ3B91MQS+btaH2WGWFyakmqYltz6jB5DOSCA6AMQYsqLlx53ORLxy3FfJhZTl9iwlrgEZjJZjDoXBBMdlMCOjKUZfTbt3pnlHWEaGJD7NoTgywFsIw5cz7hkmAMxAIkNn/5hGd/S7mwVp9h6GmBUYDsgHWpRxvnjh0s5kVD8TYjLzVnvaNFS4FXrQCiVIcp1ETqicXRjE4T0MYdnFD8h7og3ZlAFixM3nYpUYgKnqi2o2zJg7fEZ8c=


openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 -salt -base64 -in /tmp/website_output.txt -out /tmp/decoded_message.txt -pass pass:91J6X7R4FQ9TQPM9JX2Q9X2Z



cat decoded_message.txt 
Well done — the glitch is fixed. Amazing job going the extra mile and saving the site. Take this flag THM{w3lcome_2_A0c_2025}

NEXT STEP:
If you fancy something a little...spicier....use the FLAG you just obtained as the passphrase to unlock:
/home/eddi_knapp/.secret/dir

That hidden directory has been archived and encrypted with the FLAG.
Inside it you'll find the sidequest key.




oot@tbfc-web01://home/eddi_knapp/.secret$ ls -la
total 420
drwxrwxr-x  2 eddi_knapp eddi_knapp   4096 Dec  1 18:16 .
drwxr-x--- 18 eddi_knapp eddi_knapp   4096 Dec  1 08:52 ..
-rw-------  1 eddi_knapp eddi_knapp 419589 Dec  1 08:32 dir.tar.gz.gpg
root@tbfc-web01://home/eddi_knapp/.secret$ gpg --decrypt dir.tar.gz.gpg > dir.gz
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
root@tbfc-web01://home/eddi_knapp/.secret$ gzip -d dir.gz 
root@tbfc-web01://home/eddi_knapp/.secret$ mv dir dir.tar
root@tbfc-web01://home/eddi_knapp/.secret$ tar -xvf dir.tar
dir/
dir/sq1.png






now_you_see_me


```
## Videos
- https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti
- 