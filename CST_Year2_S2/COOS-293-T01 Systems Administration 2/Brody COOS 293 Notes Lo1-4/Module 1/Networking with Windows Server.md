Contents, each a lesson.
[[#Plan and Implement IPv4]]
[[#IPv4 Configuration]]
[[#Manage and Troubleshoot IPv4]]

---
# Plan and Implement IPv4

Network uses binary notation of addresses.

**Classful Network**
This is using a host IP instead of a subnet. A class C typically does this.

**Classless Network**
This is using subnets, typically class A does this.
## Subnet

Address and subnet mask determine which computers can talk to each other.

Network ID (identify network)
Host ID (identify computer)

If the last octet is not 0 or 255, then is a *classless* and is using a subnet. Example 255.255.255.172.
### Gateway

To talk to the same subnet, need to send traffic through a router.
To talk to another subnet or network, need to send traffic to a router that sends it to a *default gateway*.

A default gateway can be configured to do both.
## Private Address

*Public* address to talk to the outside world, not used internally.

- Globally unique
- Routable on the internet
- Assigned by IANA/RIR

*Private* address are used internally.
10.0.0.x/8 are private addresses in class A.
172.16.0.0 - 172.31.0.0/12 are private in class B.
192.168.0.x/16 are private in class C.

*Troubleshooting*:
APIPA 169.254.0.0, this is a problem. This means a host was not given a proper address.
If a device is using a public address, then this is an issue because private addresses are used internally.
## Supernets

This combines multiple small networks into a larger network.
If you're in a situation where there is not enough hosts in a subnet, this will take multiple subnets and treats it like one large subnet.

This is most commonly used in DHCP servers.
# IPv4 Configuration

---
Alternate Configurations

Scenario: Hard coded IP's are used at home, then the alternate IP is used at work.
Other scenario: Server is at a reserved address, but if DHCP does not respond it can used that same address with the alternate configuration static IP.

WINS server uses a *flat name space* that is a not a *fully qualified domain name*. Simple, but the domain name is non-standard.

### Advanced TCP/IP Settings

Can keep adding many IP address. This can be used to add to many subnets and this is good for routers.
A web server can use this to give different pages/sites to bound to certain addresses. It looked like many websites on one web server.

Add many gateways with a custom matric. This is used if a computer is on different subnets to find the proper gateway. Metric is the "cost" or "weight" of travel.
This could be used so certain members can have their own network with benefits and use the normal one as a backup.
## DNS

Words for people, numbers for computers.

*Preferred*

*Alternate* will almost never be used. This is only used if the first one does not respond (not if it's busy or not preferred).
### Advanced DNS Settings

The chances of needing this is very rare and if this is needed then there are other issues.
Can order these.

Can append the primary DNS suffix. This will make the flat name spaces append the suffix.
A number of custom suffix can added so that if old renamed domains exist it can still try to look around.
This is basically used make a "global name space" to make flat name spaces a fully qualified domain name.
## WINS

Do not use WINS, too old.
This can import a *host file* though. A host file is sometimes used in security attacks.
A host file was used to defend redirecting links from advertisements, basically sets them to a 127.0.0.1 (loopback) address.
## Tools

Built-in windows tools.

`netsh` commands can be used for networking.
This creates a named interface address and give DNS settings.

PowerShell can do a bunch of these, so typically just PowerShell is used instead of all the CMD tools.
# Manage and Troubleshoot IPv4

---
## Routing

Reminder, to get out of subnet, you must go through a router (layer 3 switch).
Routers are not proper edge device (going out to internet).

Routing table has:

- Network destination - subnet
- Netmask
- Gateway
- Interface - NIC and routing table (route print - bottom first)
- Metric - cost, weight

`route print` on the command link is very good to see if a machine can talk to the gateway.

Router talk to each other to see if neighbors have other addresses and they all share with each other to build their routing table. Depending on how traversals needed, it will look for the shortest path (or the next one if it is busy).
### Modify IPv4

You can assign routes manually.
This would be good for situations where you want a certain route to be chosen all the time. This can be good for security if you route through devices you control.
### Troubleshooting

Ask:

- Who is affected - *scope* of the issue and help determine what the issue could be
- When did the issue start
- Can you reproduce the issue
- Which networking functionalities have issues and which functionalities are operational

### Common CMD

`ipconfig` Check for apippa.
`ping` Memorize a couple good IPs like the server. icmpecho. This is often blocked for security purposes.
`tracert` Trace route. View network hops to get to a destination. See where the router fails. `pathping` is also good for this.
`nsloopup` This is good for viewing DNS, good for security people too.
`netstat -ab` Can put an IP to do it from another device. It checks every *port* and what's listening.