Hardening - Making something more secure, changing things from the default, getting rid of things you don't need. 

General Attack Types
	Understand attacker types and their motivations
	Footprinting and fingerprinting
		Gathering information, passive, company doesn't know it's happening. Can look up stock prices, research company, etc. and company will never know
	Spoofing
		Attacker disguises their identity
	Denial of service
		attack that makes service unavailable to users
		may be purely destructive of may allow attacker to spoof legitimate service
	Different experience levels
		Script Kiddie - found their stuff online, don't really know what they're doing, dangerous because of this
		Intermediate - semi-dangerous
		Expert - probably can't stop this person because they're so experienced

On-Path Attacks
	Threat actor intercepts communication path
		"Man in the middle"
		True man in the middle pretends to be the server/client on both ends so everything goes through them
	MAC spoofing and IP spoofing
		change address value in packet
	ARP spoofing
		broadcast unsolicited/gratuitous ARP replies
		Masquerade as MAC address of default gateway
		Gets cached on client and/or server
	Rouge DHCP
		Configure clients with malicious default gateway/DNS server IP

DNS poisoning Attack
	Spoofing trusted hosts/sites with own IP (pharming)
	Denial of Service (DoS)
	Client-side attacks
		change/intercept resolver traffic
		modify hosts
	Server-side attacks
		Hack server and change name records
		pollute server cache

VLAN Hopping Attacks
	Send traffic to VLAN that would not normally be accessable
		Double tag exploit against weakly configured VLANs
			Create packet with 2 VLAN tags
		Masquerade as Trunk

Wireless Network Attacks
	Rogue access points
		potential backdoor
		Risks from shadow IT
		packet sniffing
	Evil twins
		Spoofs SSID and BSSID (MAC) of legitimate IP or something similar
	De-authentication attacks
		Cause clients to disconnect from AP

Distributed DoS attacks and Botnets
	Coordinated attacks launched by multiple hosts simultaneously
		Overwhelm bandwidth
		Overwhelm processing resource (Flood state table)
	Distributed reflection DoS
		Amplification attack
		Spoof victim IP to overwhelm it with responses
	Botnets
		Group of compromised hosts used to penetrate DDoS/DRDoS
		Handler/herders versus bots
		Command and control (C&C/C2) network

Malware and Ransomware
	Malware Classification by vector
		Virus - requires human interaction & worms - like virus but does not require human interaction, multiply
		Trojan - self explanitory
		Potentially Unwanted Programs (PUPs/PUAs)
	Malware Classification by payload
		Spyware, rootkit, remote access trojan (RAT), ransomware...
	Ransomware
		Spoof shell/dialogs/notifications
			Simple, single machine typically, rare now
		Crypto-malware
			Now has added exfiltration

Password Attacks
	Password Capture
		Plaintext storage and transmission
		Password hashes
	Password hash cracking
		Dictionary
		Brute force
		hybrid
	Protecting password hashes
		Early SMB for example is un-encrypted

Human Environmental Attacks
	Social Engineering of hacking the human
		Reasons for effectiveness - lots of different methods and situations
	Phishing
		Social engineering over email
		Also uses spoofed resource (website)
	shoulder surfing
		Observing password entry/PIN entry
	Tailgating and piggybacking
		gaining unauthorized entry to premises

Device and Service Hardening
	Hardening means applying a secure configuration to each network host or appliance
		Change default passwords
		Enforce password complexity/length requirements
		Configure role-based access
		Disable unneeded network services
		Disable unsecure protocols
	Different Devices (roles) will be hardened differently

Endpoint Security and Switchport Protection
	Disable unneeded switchports
		restrict physical access/unplug patch cord
		Administratively disable port
		Assign black hole VLAN
	Configure protection mechanisms
		MAC filtering and Dynamic ARP inspection
		DHCP snooping
		Neighbor discovery (ND) inspection and router advertisemnet (RA) Guard (IPv6)
		Port security (IEEE 802.1X Port-Based Network Access Control)

VLAN and PVLAN Best Practices
	Private VLAN
		Further segment traffic within host/primary VLAN
		Promiscuous, isolated, and community ports
	Default VLAN and native VLAN
		VLAN ID 1 is default VLAN, all ports all ports start with this
		Native VLAN contains untagged traffic on trunks
		Native VLAN is also VLAN 1 by default, should change to unique value on both ends of the trunk

Firewall Rules and ACL Config
	Network Access Control List (ACL)
		Top-to-bottom
		Default block (Implicit deny)
		Explicit Deny
		Tuples
	IPtables
		Chains(INPUT, OUTPUT, and FORWARD)
		Stateful rules

Control Plane Policing
	Control, data, and management planes
	Control and management require CPU resource
	Control and management must always be kept "open"
		Sufficient Bandwidth
		Sufficient processing resouce
	Control plane policing policy
		Mitigate route processor vulnerabilities
		ACL-based filters
		Rate-limiting

Wireless Security
	Preshared keys (PSKs)
	Extensible Authentication Protocol
	Captive protocol
	MAC filtering
	Geofencing
	Antenna placement and power levels
	Wireless client isolation
	Guest network isolation

IOT Access Considerations
	Audits to prevent use of shadow IT
	Secure Administration interfaces
	Include IoT in patch and vulnerability management

Patch and Firmware Management
	Monitor security and patch advisories
	Appliance firmware updates vs OS patches
	Firmware upgrade procedure
	Downgrading/rollback firmware
		Config backup