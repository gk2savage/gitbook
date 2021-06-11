# Attack Vectors

{% embed url="https://medium.com/@adam.toscher/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa" %}

### LLMNR Poisoning

![](../.gitbook/assets/image%20%2819%29.png)

{% embed url="https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/" %}

Basically we are mitm and wait for someone in the domain to access non-existing domain which will lead to sending a broadcast request through which we capture the hash and then maybe crack it to get access.

![](../.gitbook/assets/image%20%2821%29.png)

![](../.gitbook/assets/image%20%2825%29.png)

![](../.gitbook/assets/image%20%2826%29.png)

`hashcat -m 5600 ntlmhash wordlist //5600 - NetNTLMv2`

### SMB Relay

![](../.gitbook/assets/image%20%2817%29.png)

We search for devices in domain with smb signing disabled. for example with nse script in nmap for smb  
[https://nmap.org/nsedoc/scripts/smb2-security-mode.html](https://nmap.org/nsedoc/scripts/smb2-security-mode.html)

We change configs in responder.conf, run the responder again with the same command and setup relay with ntlmrelayx.py. Same as LLMNR poisoning but we use the hash to relay it to smb service and get access. In ntmlrelayx.py, we can use -i to get interactive smb shell.

![](../.gitbook/assets/image%20%2816%29.png)

![](../.gitbook/assets/image%20%2820%29.png)

![](../.gitbook/assets/image%20%2824%29.png)

Getting Shell with credentials using psexec  
`psexec.py marvel.local/fcastle:password1@192.168.1.12`

### IPv6 Attacks

{% embed url="https://github.com/fox-it/mitm6" %}

Feature like Active Directory Certificate Services can make the attack more powerful. If a AD CS certificate   
is enabled, we can run LDAP or LDAPS to attack

{% embed url="https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/" %}

![](../.gitbook/assets/image%20%2818%29.png)

![](../.gitbook/assets/image%20%2822%29.png)

![](../.gitbook/assets/image%20%2823%29.png)

![Login from admin dc led to relay and create another user for you to get inside](../.gitbook/assets/image%20%2815%29.png)



