Security Appliance - standalone device for security (firewall) or more commonly now it's bundled with other things.

Network Segmentation Enforcement
	Creates boundries for network traffic
	Traffic between segments can be filtered
	Network security zones - Internet facing vs internal, perimeter network, often vLANs

Screened Subnets
	Different security configs for public and private
	Screening firewalls on the public interface
	choke firewall on internal surface (also called back-to-back firewall)
	Triple homed firewall config
	Screened Subnets Diagram
		![](Pasted%20image%2020231108081602.png)

Firewall Uses and Types
	Packet filtering firewalls
		Access Control List (ACL) with accept or deny rules
		Layer 3(+ TCP/UDP Port Number) only
		IP Source/destination, IP protocol type, source/destination port
		looks at each packet and makes a decision, doesn't care if you are part of the conversation or not
	Stateful inspection firewalls
		Doesn't do real decision making, if you are "part of the conversation" it will let you through
		Layer 4 - Monitoring connection status
		Layer 7 - Inspect application protocol packet contents

Firewall selection and placement
	Placement - Perimeter vs internal vs host, load
	Appliance firewall - Routed vs layer 2
	Router firewall - Enterprise vs SOHO

Proxy Servers
	Computer between you and something else
	Outbound proxy completes requests on behalf of clients
	Application specific vs multipurpose
	Caching
	Transparent/Non-Transparent
	Reverse Proxies

Network Address Translation (NAT)
	Mapping between internal private IP address ranges and public addresses
	Static NAT/Dynamic NAT

Port Address Translation/Network Address Port Translation (PAT/NAPT)
	Overloading
	router is configured with single public IP
	Maps clients connections ephemeral ports

Intrusion Detection and prevention systems
	Intrusion Detection systems (IDS)
		Sniffs traffic to match signatures of suspicious packets
		Passive detection
	Intrusion prevention systems (IPS)
		Can block traffic
	Standalone/integrated with firewall

Troubleshoot Service and Security Issues

DHCP issues
	Server scope and exhaustion issues
		Server offline
		Address pool exhausted
		No DHCP Relay
		the router between the client and DHCP server doesn't support BOOTP forwarding (DHCP discovery broadcasts getting blocked by router)
		clients may have expired config
	Rogue DHCP server issues
		Accidental deployment
		Malicious

Name resolution Issues
	Name resolution methods
		Verify name resolution sequence
		Test services with HOSTS
		check client's DNS server address config
		check server availability
	DNS config issues
		Suspect name resolution issue when you can connect via IP but not name
		Establish scope of the problem - single client?/subnet?
		Verify client config - DNS server and suffix, static assignment or DHCP
		Lookup tools to verify resource records on DNS server

VLAN Assignment Issues
	Check config on switch
	Check VLAN membership
	Check services available to VLAN (Routing, DHCP, DNS, Authentication/Network applications)

Unresponsive service and Network performance issues
	Verify scope - Client or server problem?
	Application or OS crash
	Hardware overutilization
	Network congestion
	Broadcast storm
	Denial of Service (DoS)

Misconfigured Firewall and ACL Issues
	Authorized application blocked
		Blocked TCP or UDP port
		Blocked IP or network
		test from inside and outside firewall
		inspect firewall log

Untrusted Certificate Issues
	Must be a trust relationship with server's CA
	Check root certificates store
	self-signed certificates - fine to use in your network, but people outside the network will likely not trust it
	Subject name and key usage issues
	Expired/revoked certificates
	Time sync

Other Common Issues
	NTP issues - verify accurate time sync
	Bring your own device (BYOD) challenges
		Compatibility support
		Security issues
		Enterprise Mobility Management (EMM) and corporate workspaces
	Licensed update features
		Expiry of trial periods
		Activation failure

