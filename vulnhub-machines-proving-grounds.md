---
description: Quick Writeups for Vulnhub/ PG Machines
---

# Vulnhub Machines / Proving Grounds

## Infosec Prep

USER  
User : OSCP  
User-Agent: \* Disallow: /secret.txt  
In robots.txt, we get base64 encoded Private SSH Key.  
`ssh oscp@IP_ADDRESS -i id_rsa` 

ROOT  
SUID bash binary  
`/bin/bash -p`  
Unintended Methods:  
[https://falconspy.medium.com/infosec-prep-oscp-vulnhubwalkthrough-a09519236025](https://falconspy.medium.com/infosec-prep-oscp-vulnhubwalkthrough-a09519236025)



