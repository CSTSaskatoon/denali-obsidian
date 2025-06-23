Content (each a lesson):
[[#Dynamic Host Configuration Protocol]]
[[#Deploy DHCP]]
[[#High Availability]]
[[#Manage and Troubleshoot DHCP]]

---
## Dynamic Host Configuration Protocol

---
It doesn't just give IP address, it gives out:

- Subnet mask
- Gateway
- DNS server
- Timer servers
- Domain suffix

Hard coding IP addresses would be a lot of work because you have to enter the other settings and services.

DHCP are platform independent - Windows, Linux, and MAC and any operating system at any time. Some (old/hardware) devices do not known how to talk to the DHCP server.

Automatic addressing saves a lot of work and get rid of human error. Updating client TCP/IP settings automatically. A single DHCP can handle over 10k devices.

### How are address leased

**DORA**
These are the steps a device needs to do to get an IP address:

- *Discover* through broadcasts (look for DHCP)
- *Offer* from DHCP
	- If multiple DHCP, they all offer and device takes the first one
- *Request* to DHCP (broadcast) to take that address
	- If multiple DHCP, they take back their offer
- *Acknowledge* (Ack) from DHCP will give you all the other configurations and servers
	- Not Acknowledge (NAck) if it fails, then DORA would happen again

### Address lease

After the IP request and no DHCP responds, it then looks for alternative hard coded address. After all fails it will have an IPPIPA address.

**Renewing the lease (DHCPREQUEST)**
After a certain amount of time, the device will continue to renew their lease on the IP address. How they do this, they wait until the 50% mark to request a renewal with a unicast. This is when new settings would be applied from DHCP.

Failing to renew address, it will wait until the 87.5% mark to make a DHCPDISCOVER broadcast. If it fails to renew, it will give itself an APPIPA address.

A default lease it 8 days, so 87.5% is 7 days.

APPIPA address are nearly useless, but it will automatically make a discover broadcast every so often.

#### Shutting down then back up

A device will keep the same address if it still has the lease time. It will contact the original DHCP with a unicast. It will then get the renewal no matter what the percentage was. If there was no responds from the DHCP, it will contact the gateway and if that responds then it assumes the address is useable.

Some systems will release the address when it is shutdown, this is disabled by default.

## Deploy DHCP

---

Installing process is from Roles and Features from Windows Server or from PowerShell. Some configurations are necessary and need to be authorized (in Windows).

### Authorizing DHCP

This is process done because they do not want rogue DHCP servers giving out bad IP addresses. It will request for authorization from Active Directory Domain Service. If it is on AD DS, it will not need a password to authorize.
This process is not effective for actual attackers since they can use Linux, or some other DHCP service to do their attacks. At the end of the day, it stops administrators from making simple mistakes.

### Scopes

>DHCP uses scopes
>DNS uses zones

IP and subnet mask tell you how to communicate. So the scope will contain:

- Range of IP addresses
- Subnet mask
- Lease duration

It may also contain:

- Default gateway address
- DNS server and suffix
- Other network options

Using a DHCP services, it will need to configured with a scope.
The scope will have an address pool. It will also be deactivated by default.
It will suggest the same DNS the server is currently using, and validate the DNS when it is selected.

*Superscope* is a container for one or more scopes that are not multicast. This is used to review statistics and configuring failover for all the scopes, while each scope is configured individually. You can use this superscope it choose from any of the scopes. This would be used to make multiple subnets work together and treat it like a big pool.

### Lease and Duration

A temporary assignment. The duration is depending on business rules and requirements of organization. A network does not want to have long duration for a place where the turnaround of users is high. Thought, a shorter duration means that renewal requests will be frequent.
Wired devices may use 8 days, wireless devices may use 24-48 hours. Hotspots (like coffee shop) may be an hour. Offices may be 8 hours.

Always make sure 20% of the DHCP pool remains available and a cushion.

### Reservation and Exclusion

Donovan starts his scope at 20 because it is his personal practice. He hard codes his servers at those addresses. He also excludes those addresses manually by not including it in the scopes. This is doable for SOHO.

Most organization do rely on their reservations for servers, and exclusions knowing they will not be deleted.
x.x.x.001 is used for gateway.

**Reservations**
It will match MAC addresses to a reservation pool. The reservation will not be leased to anyone else, even if the rest of the pool is full.

### DHCP Manage options

Common ones are:

- Router (3)
- Default gateway (6)
- DNS server (15)

Option Scope:
If there are conflicts, the closer to the IP address (or scope) it will use that. Generic at server, specific at reservations and reservations will be chosen first.

- Server
- Scope
- Class
- Reservation

**IPv4 and Scope Properties**

- Conflict detection attempts - can be set to 1 to avoid some conflict errors
- Lists database
- Database backup (in same directory)
- Enabling DNS dynamic updates 
	- Secure dynamic makes it so only the creator can change the DNS record
	- If the creator (can be the DNS server) changes, that record will be locked there

### Multicast Scopes

Multicast: machine to machines that are open to it (groups)
Unicast: machine to machine
Broadcast: machine to all machines

Multicast is in a class B range, with the following options:

- Exclusions
- Lease Duration - these can be very long

### DHCP Policies

Starting with Windows Server 2012, DHCP policies can give granular control over scopes, based on device type or its roles.

Two types of policies: User class and Vendor class.

**Vendor class**
These are premade. Their information is requested from manufacturer.

**User class**
These are made by administration. It is for a group of clients that require similar configuration.

These policies can be makes to assign ranges of IP in a subnet for certain devices. Example: printers, desktops, phones, etc. in their own range. The client will need to know what type of class they are, the client announces this class when they try to connect. These are not used often.

This can be used for these scenarios:

- Vendor class to assign a range of IPs for phones. This can make connecting and communicating more simple as they other clients would know that group are IP phones
- User class is good for defining rules for devices added to that group. It can also be used to apply different settings. A rule can be returning laptops need to be checked at different gateway before connection to main network

Microsoft made Health Services for remote access that does something similar.

#### Configure PCE Boot Clients

Basically, a machine with no operating system and use the network server OS to install a OS.
This must be configured in CMD, or in Setting Predefined Options (option 60). This option is NOT available by default so a network administrator must define this option.

The name can say "060 PXE Clients" and set the value to the IP value (as a string) to the destination of where they can get their OS to do their PXE boot.

Like many things, if the administrator know what the options are they can utilize it.
These options are known in the standard.

### Relay Agent

Routers block broadcasts, so network extending through routers would not be able to reach a single DHCP server. With two DHCP servers, they have to share address and move available address around.

The DHCP relay agent listens to broadcasts, then make that broadcast into a unicast to go to router and DHCP server, then it will return as a a broadcast again to reach requesting client. It will be assigned to certain scopes depending on their address and subnet range.

The relay agent are used in larger networks typically on dedicated hardware. It should also be on a different server than DHCP server. It could also be implemented as software on router or other network devices.

## High Availability

---

DHCP is supposed to give new machines an address and renew leases. Giving new address does not need to be done often sometimes, but renewing leases is often.

**Split scopes**
Use two DHCP servers and use the 80/20 rule. The first server has the majority of distinct addresses, but if it goes down then the second server should have enough addresses to assign while the first server is being repaired. This does not handle lease renewals. The timeline to repair server one is dependent on how long lease renewal times are \*0.5.

When this is created, they copy the address pool ranges but just exclude the percentage they are not using. The then stop communicating changes to their pools and act independently.

**Server cluster**
Use a *DHCP failover* to replicate information between the two DHCP server, this was introduced with Windows Server 2012.
Remember, these clusters used shared clustered storage. [[Lesson 5 High Availability with Failover Clustering|Failover Clustering Notes]].

**Standby server**
Uses a hot standby DHCP server with identical copes and options as the production DHCP server. This is used in clustering. It can either be configured as a hot backup(standby), or be use for load balancing(sharing). The hot standby is better used if the servers are in different locations as an emergency. Load balancing has better performance if they are in the same network and location.

Maximum Client Lead Time is set to an hour by default. This is how long before a client checks to see if the DHCP is responsive, but it can be any number because it also used the lease 50% renewal as a check as well.
## Configure DHCP Security Options

---

This talks about limiting physical access to network, disconnect ports, DHCP filtering, auditing and DNS protection. None of them actually relate directly to DHCP security, the best thing it to monitor traffic and use an intrusion detection system (IDS) to track offers and acknowledgment are coming from a known DHCP server.

### DHCP Name Protection

DHCP will register in the DNS for users and an ID is associated with that client. This ID is used to protect names in the DNS from others trying to steal that name, though this is rare. Name protection is not that important, but it can be easily enabled.

### Policy

Classes and policies based policies. MAC addresses (not secure), Client Identifier (FQDN) and Relay Agent Information can be used for them too.

These policies can be at different levels.

### Database

```
dhcp.mdb
```

This is the file with all scope information, leases, reservation, policies in this database file. It also as a nearby backup for itself in case it has to restore itself.
Manually backups are recommend is you are changes or making a *compact*. A compact will be required if they become too large (may be outdated), but what it does is that it removes unneeded temporary place holder. 
*Jetpack* is a program (you have to download) to copy a database into a temporary file to compact it and then replace the old one after testing it. The book does not mention this program.

There is another copy in the registry. You can *reconcile* the DHCP to check if it's information is the same as the one in the registry, this will reserve leases so when that conflicting address is given to the one that says it should have that IP. This could be used for troubleshooting.
## Manage and Troubleshoot DHCP

---

Basically, check the scope and commonalities between machines effect and unaffected.

Client:

- Make sure their settings are set for DHCP

Common issues:

- IP address conflict (rare)
- Failed to get IP (Appipa) (very common, problem comes from identifying where broadcasts are going)
- Obtained IP in the wrong subnet (rogue DHCP, relay agent misconfigured)
- DHCP database corrupt and DHCP server cannot start (restart service works)
- DHCP has exhausted IP address pool
