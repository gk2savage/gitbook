---
description: Quick Writeups for Vulnhub/ PG Machines/ THM/ HTB
---

# Vulnhub/ PG/ THM/ HTB

## Infosec Prep

USER\
User : OSCP\
User-Agent: \* Disallow: /secret.txt\
In robots.txt, we get base64 encoded Private SSH Key.\
`ssh oscp@IP_ADDRESS -i id_rsa`&#x20;

ROOT\
SUID bash binary\
`/bin/bash -p`\
Unintended Methods:\
[https://falconspy.medium.com/infosec-prep-oscp-vulnhubwalkthrough-a09519236025](https://falconspy.medium.com/infosec-prep-oscp-vulnhubwalkthrough-a09519236025)

## FunBoxEasy

USER : Dirbuster ->  [http://192.168.74.111/store/admin.php](http://192.168.74.111/store/admin.php)\
Login with admin:admin, edit image and upload PHP reverse shell.\
SSH with password.txt \
ROOT : sudo time /bin/bash



## Dawn

USER : smbclient //192.168.178.11/ITDEPT\
Management.log in :80/logs shows web-control running as root.\
uploaded python shell in smb ITDEPT share with name 'web-control'\
Got reverse shell with cron.\
ROOT : checking for SUID BITS, found `/usr/bin/zsh -> euid=0`



### **Machine Categories**

#### **SSTI**

HTB - Late (Image to Text Application built with Flask)

### Important Machines Writeups

{% embed url="https://n1ck3nd.gitbook.io/ctf-write-ups/vulnnet#receiving-a-shell" %}

Execute sandboxed Lua scripts through the “EVAL” command using _dofile(), Capturing_ NTLM hash via responder by connecting with //tun0-ip//share, Powerview and sharpHound, BloodHound for enumeration and Abusing GPO Permission via SharpGPOAbuse.exe
