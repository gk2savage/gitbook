# Pivoting

**Pivoting** allows you to attack machines or networks that would otherwise be unreachable. Pivoting to somewhat extent depends upon Port Forwarding. If not then the compromised machine might be having the permissions through a firewall / access what others cannot. I dont think pivoting depends on port forwarding necessarily tho it might be a component. Pivoting is just using a computer or device that has been compromised to attack and compromise other devices in the network.

Thus, Pivoting is a term for pentester, whereas in networking we call it proxy. So we can say that pivoting is happening due to port forwarding and routing is just packets being routed to its destination.

We use Pivoting when there are two different networks, Whereas we use routing when its a single network mostly. In simple terms, if machines are in the same network we can use routing Otherwise we can use pivoting to pivot via port forwarding.

When we are using route command, you can say that we are using routing to pivot&#x20;

There's some pivoting that involves proxychains. You do specific routes over the proxy.&#x20;



There are two main methods encompassed in this area of pentesting:

* **Tunnelling/Proxying:** Creating a proxy type connection through a compromised machine in order to route all desired traffic into the targeted network. This could potentially also be _tunnelled_ inside another protocol (e.g. SSH tunnelling), which can be useful for evading a basic **I**ntrusion **D**etection **S**ystem (IDS) or firewall\

* **Port Forwarding:** Creating a connection between a local port and a single port on a target, via a compromised host

A proxy is good if we want to redirect lots of different kinds of traffic into our target network -- for example, with an nmap scan, or to access multiple ports on multiple different machines.

Port Forwarding tends to be faster and more reliable, but only allows us to access a single port (or a small range) on a target device.



Tools for Pivoting are:

* Meterpreter, auto route along with proxychains
* Sshuttle (best) for \*nix / Linux targets
  * If Port 22 if closed, then&#x20;
* Socat can be used
* Also IPtables can be used to port forward, if you want to stick with route tables on a different network

Tools for Routing are:

* IP tables if the new set of machines are in a different network
  * IP tables is the way to port forward&#x20;
* Route command / Static Routing

### Using route

#### Syntax : `route`

**`route add -net <network_address> gw <gatewayaddr> <interfacename>`**

```
route add -net 10.0.2.0/24 gw 192.168.0.1 eth1
```

### Using ip

#### Syntax : `ip route`

* Prints the routing table for the host you are on

`ip route add [new network] via [gateway]`

Pivoting is the exclusive method of using an instance also known by ‘foothold’ to be able to “move” from place to place inside the compromised network. It uses the first compromised system foothold to allow us to compromise other devices and servers that are otherwise inaccessible directly.

**Pivoting** - We can use Sshuttle to create a Tunnel. \* If we know SSH creds and port is open.

* **Port Forwarding** - if we discover some Ports open on localhost, via `netstat -tulpn`. We can use the Port Forwarding method via SSH
* **Tunneling -** Finally, if SSH port is not open or we don't have the credentials. We can use Socat / Chisel to pivot across the network

## SSH Port Forwarding&#x20;

```
ssh -L 8000:127.0.0.1:8000 roy@10.10.10.212
```

* We can port forward or you can say ssh tunnel a port and forward it on your localhost&#x20;
* So the 8000 port running on machine 10.10.10.212 will be forwarded to run on your localhost at localhost:8000



