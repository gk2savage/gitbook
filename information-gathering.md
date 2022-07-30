---
description: >-
  Information Gathering is the act of gathering different kinds of information
  against the targeted victim or system
---

# Information Gathering | OSINT

Email Gathering : [https://hunter.io](https://hunter.io)\
Find Breached Passwords : pastebin, ghostbin, haveibeenpwned, Breachparse, Advanced Search, RF\
OSINT : [https://osintframework.com/](https://osintframework.com/)\
Usernames : [https://github.com/sherlock-project/sherlock](https://github.com/sherlock-project/sherlock)\
Rev Image Search : Yandex, Bing, Google

\
**Subdomains Hunting :**\
theHarvester\
`theHarvester -d tesla.com -l 500 -b google` \
sublist3r\
[https://crt.sh/](https://crt.sh/) Hunt subdomains with certificate search\
OWASP Amass

{% embed url="https://github.com/tomnomnom/assetfinder" %}

{% embed url="https://github.com/tomnomnom/httprobe" %}

**Web Technologies**\
****[**https://builtwith.com/**](https://builtwith.com/) **** \
****[**https://www.wappalyzer.com/**](https://www.wappalyzer.com/) **** and Widget\
OWASP ZAP

{% embed url="https://portswigger.net/burp" %}

**WHATWEB**

![](<.gitbook/assets/image (3) (2).png>)

**Google Advanced Search:**\
site:tesla.com\
site:tesla.com -www\
filetype:pdf\
intitle:tesla

{% embed url="https://sector035.nl/articles/keeping-a-grip-on-google-ids" %}

{% embed url="https://wigle.net/" %}

**DNS Record Types**\


DNS isn't just for websites though, and multiple types of DNS record exist. We'll go over some of the most common ones that you're likely to come across.\


**A Record**

These records resolve to IPv4 addresses, for example 104.26.10.229

**AAAA Record**

These records resolve to IPv6 addresses, for example 2606:4700:20::681a:be5\


**CNAME Record**

These records resolve to another domain name, for example, TryHackMe's online shop has the subdomain name store.tryhackme.com which returns a CNAME record shops.shopify.com. Another DNS request would then be made to shops.shopify.com to work out the IP address.\


**MX Record**

These records resolve to the address of the servers that handle the email for the domain you are querying, for example an MX record response for tryhackme.com would look something like alt1.aspmx.l.google.com. These records also come with a priority flag. This tells the client in which order to try the servers, this is perfect for if the main server goes down and email needs to be sent to a backup server.

**TXT Record**TXT records are free text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spam and spoofed email). They can also be used to verify ownership of the domain name when signing up for third party services.
