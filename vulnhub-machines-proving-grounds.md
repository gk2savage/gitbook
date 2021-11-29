---
description: Quick Writeups for Vulnhub/ PG Machines
---

# Vulnhub Machines / Proving Grounds

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







