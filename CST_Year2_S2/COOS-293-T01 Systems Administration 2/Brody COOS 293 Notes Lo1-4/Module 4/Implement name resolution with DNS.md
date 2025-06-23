[[#DNS on the Internet]]
[[#Troubleshoot DNS]]
[[#Configuring Zones]]

---

FQDN is made up of Hostname (@it) + Domain (.saskpolytech) + Top level (.com's), written right to left. Normally, there is dot of the right end of an address we don't use as humans. Zones/namespace are the FQDN. Scope refers to DHCP.

NetBIOS was MS was of DNS back in the, back may of may not be used still.

IP address always change, so this is where DNS comes in. This is good at home for self hosted websites. DNS server uses many databases.

Components:

- DNS server
- DNS zone (forward and reverse lookup zones)
- DNS forwarder
- DNS delegation
	- There are two: Delegation by security and delegation by name space
- DNS client/resolver
- Resource records

### DNS on the Internet

There are 13 (more unlisted) root servers for DNS resolutions. There are hundreds of servers over 130 locations around the world, but they are clustered into 13 because of there IPv4 scheme.

When a client needs an address resolved:

- Checks if looking for itself
- Check local cache
- Check host/Imhost file

Queries the DNS

- DNS checks its cache
- Checks its zones
- Checks forwarders
- Starts at root

#### Types of Queries - Forwarders

**Recursive queries**
A clients waits for a response, or an "I don't know".
A client does all the work. A root DNS server will never take a recursive query, although it is just a checkbox to enable it.

**Iterative query**
The DNS server will check the FQDN right to left, going to each server to query. The complete answer is given back to the host.

Authoritative is when the client already has information, unauthoritative is when it has to queries from servers and cache.

### DNS Zones and Records

Zone content can be stored in a file or in AD DS.
Each zone has it's own database.

Zone types:

- Forward lookup zone (name into address)
- Reverse lookup zone (address into word)

Host records for forward lookup:

- A, AAAA, MX, SRV, NS, SOA, and CNAME (like an alias)
- New zones get NS (name server), SOA (start of authority (son's of anarchy))

#### Zones

Primary zones are DNS that are read and write.
Secondary zones are copied to other networks that are read only for faster responses. Needs to reference a primary.

### DNS Database Backup

### Delegate Administration of DNS

These are permissions, and a local server administrator can manage it with full permission.

### Troubleshoot DNS

Most common:

- Missing records
- Incomplete records
- Incorrectly configured records

Troubleshooting:

- Nslookup
- DNSCmd - PowerShell is better
- DNSlint - Used for testing
- Ipconfig /displaydns, /flushdns, /registerdns (put client into DNS)
- Monitoring on DNS server
- Ping to test for connection (often blocked, so could use telnet)
## Configuring Zones

---

Can be active directory integrated with many benefits. They have replications between servers, otherwise traditionally using zone transfer.

With zone transfer or AD, best practice to have those backup zones and do the refresh regularly.
Types of zone transfers:

- Full zone transfer - usually when making a new zone such as the secondary zone
- Incremental zone transfer - what has changed
- Fast zone transfer - not common, like compressed replication or AD replications

AD Replication

### Caching

DNS carries a cache of records saved. Client will check cache, then host file, then DNS - then the DNS will check it's cache (authoritative) before looking somewhere else. They save these records for 1 hour by default.
For centralized networks, a cached only DNS may be for efficient for speed.

### Forwarding

When the DNS has to search for a name resolution, it will do an iterative search. It does not always do that iterative search, instead it will send the request to another DNS to resolve. So there is a chain that can reach the ISP.

*Conditional forwards* exist too, it will point to a DNS server that has that record, though it knows information but does not need permission.

### Stub Zone

It will only contain information about a specific zone's authoritative DNS server. This is similar to a conditional forwarder and is a secondary zone, it does need permission to forward (trusted zone trasfers). It is more accurate since it will update itself often for changes.

![[Pasted image 20250204104928.png]]

![[Pasted image 20250303203644.png]]
### DNS Zone Delegation

This will see records and forward to another server that has that authority. It is it's own zone, but another server takes card of it.

### AD DS DNS Integration

These use a SRV record. These service records are an alias with extra information (host records). This allows multi-model.
AD has many partitions, two partitions for DNS - forest and domain level.

### Secure Updates - AD DS

Ensures that errand updates do not get pushed to DNS. Not every client support Secure Dynamic Updates.
## Advanced DNS Settings

---

This advanced tab has DNS round robin, netmask reordering, recursion.
Round robin is crude load balancing.
netmask reordering just checks your hop count between networks/subnets.

DNSSEC is a digital signature, and public key is needed to check that signature.