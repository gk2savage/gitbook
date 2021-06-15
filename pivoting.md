# Pivoting

**Pivoting** allows you to attack machines or networks that would otherwise be unreachable. Pivoting to somewhat extent depends upon Port Forwarding. If not then the compromised machine might be having the permissions through a firewall / access what others cannot. I dont think pivoting depends on port forwarding necessarily tho it might be a component. Pivoting is just using a computer or device that has been compromised to attack and compromise other devices in the network.

Thus, Pivoting is a term for pentester, whereas in networking we call it proxy. So we can say that pivoting is happening due to port forwarding and routing is just packets being routed to its destination.

We use Pivoting when there are two different networks, Whereas we use routing when its a single network mostly. In simple terms, if machines are in the same network we can use routing Otherwise we can use pivoting to pivot via port forwarding.

When we are using route command, you can say that we are using routing to pivot 

There's some pivoting that involves proxychains. You do specific routes over the proxy. 

Tools for Pivoting are:

* Meterpreter, auto route along with proxychains
* Sshuttle \(best\) for \*nix / Linux targets
  * If Port 22 if closed, then 
* Socat can be used
* Also IPtables can be used to port forward, if you want to stick with route tables on a different network

Tools for Routing are:

* IP tables if the new set of machines are in a different network
  * IP tables is the way to port forward 
* Route command / Static Routing

### Using route

#### Syntax : `route`

**`route add -net <network_address> gw <gatewayaddr> <interfacename>`**

```text
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

## SSH Port Forwarding 

Example - `ssh -L 8000:127.0.0.1:8000 roy@10.10.10.212`

* We can port forward or you can say ssh tunnel a port and forward it on your localhost 
* So the 8000 port running on machine 10.10.10.212 will be forwarded to run on your localhost at localhost:8000

