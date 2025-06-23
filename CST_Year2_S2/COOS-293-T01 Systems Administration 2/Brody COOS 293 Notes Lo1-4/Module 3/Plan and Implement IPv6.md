Content:
[[#Set up IPv6]]
[[#IPv6 Host Address]]
[[#DHCPv6]]
[[#Lesson 2 - Node Types]]

---
## Set up IPv6

---

128 bit, AAAA records, Address resolution is multicast neighbor solicitation messages, better security, easier to configure.

### Fragmentation

IPv4 fragmentation - The packet is too large for the network so the data will be taken out, and break the data in multiple packets, send it out, and reassemble the data at the destination.

Allows:

- Reduce overhead
- More transportation methods

This causes:

- Fragment (packet) loss
- All data has to be resent (more traffic and causes more issues)
- First packet has header info, and subsequent packets do not and can be blocked from firewalls
- Out of order packets received and required more technology to reordering

IPv6 fragmentation - This stops at the network, send the host a request to smaller packets, then the host has to fragment the packets and not put strain on the router. It sends back an ICPMPv6 error of type 2: "Packet Too Big" code 0.

This causes:

- ICMP is often blocked, so the request back to host may be blocked

### Benefits of IPv6

Larger number of address. The address structure is hierarchical. Addresses are also "stateless" (not quite UDP, but more flags for better Quality of Service), real-time delivery of data.
IPv4 subnet is by itself, it in groups. IPv6 uses groupings of subnets and has a mapping scheme (fewer routing table compared to IPv4).
IPv6 is simpler because you can have multiple address to do multiple things, instead of IPv4 having to use its single address with many packet types.
IPv6 standard was going to have security built-in at all time, but it was not implemented to be required for backwards compatibility and fragmentation support. The security support is good.
## IPv6 Host Address

---

128bits long, arranged in eight groups each of which is 16 bits. Each group is four hexadecimal digits.

```
FE80:CD00:0000:0CDE:1257:0000:211E:729C
```

**Simplification**
Addresses are simplified by removing leading 0's. All 0's could be represented as `:0:` or `::`. The 0's are sometimes all combined for many groups but it can only be done *once* to prevent ambiguity, so groups are `::`, and single group combined is `:0:`.

**Loopback** - `::1`
**Autoconfigured** - `FE80::/60` - This is APIPA.
**Multicast** - `FF00::/8` - Does not use broadcast, used multicast and anycasts instead.

Hosting uses Neighbor Discovery protocol to generate their own node component. This uses the EUI-64 addressing scheme, but Microsoft does something else (a mystery to this day). This uses the MAC address to create a unique address.
Generating steps:

- Take MAC address (48 bit)
- `FFFE` is added in the middle, after the 3 octet
- Change 7th bit from left and inverts it (for some strange reason)
- Generates 64 bit host address

Steps:

- Generates address based on MAC address
- Multicast to NDP to check if that address it generated available
	- If it is duplicated, it will have to be manually assign

### Types of IPv6 Addressing

Unicast is going to one address.
Broadcasts (IPv4) only, go to every address.
Multicast goes to a group of receiver addresses.
Anycast goes to one address in a group of a receiver, and if it does not accept it will go down a list of addresses in that group until someone accepts. Once it reaches an address, that address will spread the packet to the rest of the group.

![[Pasted image 20250124090845.png|400]]

### Address

**Global** address is a public address. Everyone will typically have their own public address instead of sharing one with IPv4. They start with `2000::/3`, they start with a `2`, the `/3` means something else.
**Unique local** is private address used internally. `FD00::/8`, no "subnetting" in a private address.
**Link local** is `FE80` and is basically APIPA, very machine generates this with NDP and stay with the machine when it gets a property Unique local and perhaps global address.
**Site-local** is old technology replaced by unique local.

IPv6 uses the same link-local address to distinguish their zone `%zone_id`.

### Global Unicast Addresses

These are routable on the internet.

- Allocate 16 bits for internal subnetting
- Begin with 2 or 3 (`2000::/3`), but three is yet unused

![[Pasted image 20250124091655.png|400]]

![[Pasted image 20250124091707.png]]

The first 48 determine the network address (my company), 16 bits are always subnet, and 64 bits are always hosts.
The subnetting does not barrow bits, always 16 bits.

### Unique Local

Are equivalent to IPv4 private address.

- Require the organization ID to be randomly generated
- Allocate 16 bits for internal subnetting

![[Pasted image 20250124092036.png]]

### Link-Local

Automatically generated on all IPv6 hosts.

- Similar to IPv4 APIPA addresses
- Are sometimes used in place of IPv4 broadcast messages
- Include a zone ID

![[Pasted image 20250124092352.png]]

#### Autoconfiguration Options

After NDP computer is happy with that address. Next step is to find the network address. The stateless router has a "router advertisement" (Neighbor Solicitation, not a broadcast) that will send out network portion so it will be combined to make a global address.

Stateful routers do not do router advertisements and will require a DHCPv6. These will still only give out the network portion.

Often a combination will be used, router advertisement will be used and will redirect to DHCPv6 server. Redundancy is simpler since you do not need to worry about duplicate addresses.

##### Configuration States

Like DHCP leases. Network portion never changes, and MAC should not change. They use a *lifespan/tentative* on these address in case the network portion does change or for other reasons, like changes to options (think DHCP). Global addresses have lifespans.

*Valid* means address is unique.
*Preferred lifespan* works normal.
*Deprecated* means the address is still used but will be phased out, so it will not make "new conversation". Will be force to solicitate a new address.

![[Pasted image 20250124093228.png]]
## DHCPv6

---

Supports IPv6 by default, can configure scopes and all those other things, treats IPv6 and IPv4 the same.

Routers periodically multicast router advertisement messages. Valid Lifetime is typically 30 mins.
# Lesson 3 - Tunneling

---

IPv4/IPv6 node supported protocol is most commonly done. Internal will use IPv6, and to get out it will use IPv4 public address.
If it does use the mix, it will use one of the other, or tunnel it (I think).

Dual Stack or dual layer are slightly different.
Dual stack is separate protocols to handle IPv4 and IPv6, older.
Dual architecture uses one stack for both is newer, simpler but less redundancy.

### Tunneling and Transitioning

Transitioning technology was dropped from the text book so will only be covered in class.

IPv6 is not used everywhere and the internet only used IPv4.

### Encapsulation Technologies

#### ISATAP - Intra-Site Automatic Tunnel Address Protocol

IPv6 on both ends with IPv4 used in the middle. This is for *intranet*, but could go outside into the internet. There are also routers designed for ISATOP.
Connect an IPv4 only network with a IPv6 network where ISATOP is the bridge.
IPv4 is assigned an ISATAP tunnel with IPv6 address, with an interface address on the end. It was has a common prefix configured by administrator or router.
IPv6 packed is placed in an IPv4 packet, by pulling the end of the address.

IPv6 address will use a portion of the IPv4 address.
Address example:
Private: `FD00::0:5EFE:192:168:137:1333`
Public: `2001:db8::2000:5EFE:131:107:137:133`
Format: `2002:WWXX:YYZZ:subnet_ID::/64`

The router advertises itself. This advertises an ISATOP address and IPv6 will build their address differently because of that.
Configure ISATOP host record in DNS and other setups.
Not compactable with NAT.

**6to4 Tunneling**

`2002-2003` is a public/global address, but these are used for 6to4. Typically `2001` is global, but is not 6to4.
At the router it will be encapsulated into IPv4, and when it gets to the intranet router it will become an IPv6 address again.

#### Teredo

This requires more infrastructure: Server, relay, etc. It is compatible with NAT.
NAT(PAT,NPAT) is based on ports.
It also needs the address for the server.

![[Pasted image 20250128102722.png]]

Teredo objects:

- Teredo client
- Teredo server - Tunnels and Sends
- Teredo relay - Receives and Untunnel
- Teredo host-specific relay

**IPv4 UDP Tunnels**

Can use the same public address as other clients.
The ports and address are obfuscated.