# Post Compromise Enumeration

### POWERVIEW

{% embed url="https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1" %}

{% embed url="https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993" %}

![](<../.gitbook/assets/image (27).png>)

### SharpHound

{% embed url="https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1" %}

<pre><code><strong>PS>
</strong><strong>Import-Module C:\Enterprise-Share\sharphound.ps
</strong>Invoke-BloodHound -CollectionMethod All

ie. a zip will be created that we can import in Bloodhound in below format:
20211217084021_BloodHound.zip</code></pre>

### BLOODHOUND

{% embed url="https://bloodhound.readthedocs.io/en/latest/installation/linux.html" %}

```
sudo apt-get install neo4j
sudo neo4j console
```

This would run the neo4j service. \
INFO Bolt enabled on localhost:7687\
INFO Remote interface available at http://localhost:7474/

Default Credentials: neo4j/neo4j

If there is password error while logging in,

1. Stop neo4j if its running
2. edit /etc/neo4j/neo4j.conf, and uncomment `dbms.security.auth_enabled=false`
3.  connect to the database and run

    ALTER USER neo4j SET PASSWORD 'mynewpass'; :exit
4. Stop neo4j
5. comment out the `dbms.security.auth_enabled=false`
6. start neo4j

```
apt install bloodhound
```

setup neo4j console and open it in browser to access. We can run invoke-bloodhound to collect data and import it in neo4j localhost to get idea about AD.&#x20;

{% embed url="https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1" %}

![](<../.gitbook/assets/image (28).png>)

![](<../.gitbook/assets/image (29).png>)
