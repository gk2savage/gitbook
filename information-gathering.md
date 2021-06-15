# Information Gathering

Email Gathering : [https://hunter.io](https://hunter.io)  
Find Breached Passwords : pastebin, ghostbin, haveibeenpwned, Breachparse, Advanced Search, RF  
OSINT : [https://osintframework.com/](https://osintframework.com/)  
Usernames : [https://github.com/sherlock-project/sherlock](https://github.com/sherlock-project/sherlock)  
Rev Image Search : Yandex, Bing, Google

  
**Subdomains Hunting :**  
theHarvester  
`theHarvester -d tesla.com -l 500 -b google`   
sublist3r  
[https://crt.sh/](https://crt.sh/) Hunt subdomains with certificate search  
OWASP Amass

{% embed url="https://github.com/tomnomnom/assetfinder" %}

{% embed url="https://github.com/tomnomnom/httprobe" %}

**Web Technologies**  
[**https://builtwith.com/**](https://builtwith.com/)   
****[**https://www.wappalyzer.com/**](https://www.wappalyzer.com/) ****and Widget  
OWASP ZAP

{% embed url="https://portswigger.net/burp" %}

**WHATWEB**

![](.gitbook/assets/image%20%281%29.png)

**Google Advanced Search:**  
site:tesla.com  
site:tesla.com -www  
filetype:pdf  
intitle:tesla

{% embed url="https://sector035.nl/articles/keeping-a-grip-on-google-ids" %}

{% embed url="https://wigle.net/" %}

## DNS Enumeration

### **Banner Grabbing**

DNS does not have a "banner" to grab. The closest equivalent is a magic query for `version.bind. CHAOS TXT` which will work on most BIND nameservers.  
You can perform this query using `dig`:

```bash
dig version.bind CHAOS TXT @DNS
```

If that does not work you can use fingerprinting techniques to determine the remote server's version -- the [`fpdns`](https://github.com/kirei/fpdns) tool is one option for that, but there are others.

You can grab the banner also with a **nmap** script:

```text
--script dns-nsid
```

### **Zone Transfer**

```bash
dig axfr @<DNS_IP> #Try zone transfer without domain
dig axfr @<DNS_IP> <DOMAIN> #Try zone transfer guessing the domain
fierce -dns <DOMAIN> #Will try toperform a zone transfer against every authoritative name server and if this doesn'twork, will launch a dictionary attack
```

### More info

```bash
dig ANY @<DNS_IP> <DOMAIN>     #Any information
dig A @<DNS_IP> <DOMAIN>       #Regular DNS request
dig AAAA @<DNS_IP> <DOMAIN>    #IPv6 DNS request
dig TXT @<DNS_IP> <DOMAIN>     #Information
dig MX @<DNS_IP> <DOMAIN>      #Emails related
dig NS @<DNS_IP> <DOMAIN>      #DNS that resolves that name
dig -x 192.168.0.2 @<DNS_IP>   #Reverse lookup
dig -x 2a00:1450:400c:c06::93 @<DNS_IP> #reverse IPv6 lookup

#Use [-p PORT]  or  -6 (to use ivp6 address of dns)
```

#### Using nslookup

```bash
nslookup
> SERVER <IP_DNS> #Select dns server
> 127.0.0.1 #Reverse lookup of 127.0.0.1, maybe...
> <IP_MACHINE> #Reverse lookup of a machine, maybe...
```

### Useful Metasploit modules

```bash
auxiliary/gather/enum_dns #Perform enumeration actions
```

  


