# Attack Vectors

{% embed url="https://medium.com/@adam.toscher/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa" %}

### LLMNR Poisoning

![](../.gitbook/assets/image%20%2815%29.png)

{% embed url="https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/" %}

Basically we are mitm and wait for someone in the domain to access non-existing domain which will lead to sending a broadcast request through which we capture the hash and then maybe crack it to get access.



