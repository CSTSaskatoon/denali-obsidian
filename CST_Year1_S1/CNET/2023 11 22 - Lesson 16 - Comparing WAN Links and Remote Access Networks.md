Wide area Network Technologies and the OSI Model
	WAN physical layer
		Modulation and Demodulation
		Analog modems and digital modems
	WAN Data Link Layer
		point-to-point links using serial data protocols
		Ethernet
	WAN Network Layer
		Customer Edge (CE) router link to Provider Edge (PE) router (demarc point)

WAN Provider links
	Demarcation Point (demarc)
		Termination pint for service provider's cabling
		Minimum point of entry (MPOE)
		Where your network traffic goes to get to the internet
	Customer premises equipment (CPE)
	Entrance facilities

T-Carrier and Leased Line Provider Links
	Time Division Multiplexing (TDM) circuits
		64Kbps
		24 channels multiplexed as a T1 leased line
	Smart Jack/Network Interface Unit (NIU)
		Serial digital signal over 2-pair UTP
		RJ-48C or RJ-48X to connect to the CSU/DSU
	Channel Service Unit/Data Service Unit (CSU/DSU)
		DSU Digital modem encodes signal from PBX/router
		CSU performs diagnostics
		Typically Implemented as WAN interface card
	Data link Layer
		High level Data link Control (HDLC) or point-to-point protocol (PPP)

Digital Subscriber Line Provider Links
	Shares same physical telephone line but uses higher frequency range
	DSL modem installed as CPE
	Filters must be installed on telephone points
	DSL types
		Symmetrical DSL (SDSL)
		Asymmetrical DSL (ADSL)

Fiber to the Curb (FTTC)
	Fiber to the X (FTTx)
		Fiber optic cabling in the last mile
		To the home (FTTH), to the premise (FTTP)
		To the node (FTTN), to the curb (FTTC)
	Very High Bitrate DSL (VDSL)
		supports FTTC with VDSL over the last part of link (up to 300m)
		Up to 52Mbps downstream and 6Mbps upstream
		VDSL2 up to 100Mbps over 100m (300 feet)

Cable Provider Links
	Shares same physical cable as cable access TV (CATV)
		COAX link to customer premises
		Fiber optic core network
	Cable modem installed as CPE
		Connects to service provider network using coax F-connector
	Data Over Cable Service Interface Specification (DOCSIS)
		Downlink speeds of up to 38Mbps (NA) or 50Mbps (EU) and uplinks of up to 27Mbps
		DOCSIS version 3 allows use of multiplexed channels to achieve higher bandwidth

Metro-optical Provider Links
	Carrier Ethernet
		Carrier Ethernet provisions point-to-point or point-to-multipoint Ethernet leased lines over wide area networks
		Carrier Ethernet may also be referred to as a metro-optical provider link
		Physical service types
		Service categories
	Passive Optical Network
		Residential/SME Fiber to the Home (FTTH) or Premises (FTTP) service
		Speeds of 100Mbps+
		CPE router connects to optical network terminator (ONT) at demarc via fiber optic patch cable

Microwave Satellite
	Align with orbiting satellites
		Geostationary with the equator
	Subject to higher latency
	ISP installs very small aperture terminal (VSAT) satellite dish at customer site
	Connected via coax to a Digital Video Broadcast Satellite (DVB-S) modem

Remote Network Access Authentication and Authorization
	Authenticate and Authorize Users
	Document service, risks, and countermeasures for better security
	Define policy restrictions
		Users/groups, time of day, privileges, auditing...
	Manage Remote Devices

Tunneling and Encapsulation Protocol
	Establish a host on the same logical network over a connection through a different network
	Point-to-Point Protocol (PPP)
		Encapsulation for higher layer packets at layer 2
		Works over serial point-to-point links
	Generic Routing Encapsulation (GRE)
		Encapsulates packets at layer 3 (IP protocol #47 and has it's own IP source and header address fields)
		Supports point-to-point and point-to-multipoint (mGRE)
		Independent of PHY/data link network implementation
	IPSecurity (IPSec)
	Transport Layer Security (TLS) and Datagram TLS (DTLS)

Client-to-site Virtual Private Networks
	Remote Access or telecommuter model
	Protocols
		TLS, Secure Socket Tunneling Protocol (SSTP), layer 2 Tunneling Protocol (L2TP), IPSec
		EAO/RADIUS authentication
	Split tunnel - sends regular internet traffic not through the VPN, only network Traffic
	Full Tunnel - everything gets sent through the VPN

Remote Host Access and Remote Desktop Gateways
	Remote Host Access
		Remote Configuration and Administation (Graphical or Terminal)
		Remote User Access to a Desktop (RDP)
		Remote Desktop Gateways for Virtual desktops and apps (VDI)
	Remote Desktop Protocol (RDP) and Virtual Network Computing (VNC)

Site-to-Site Virtual Private Networks
	Graphic
		![](Pasted%20image%2020231122092848.png)

Hub and Spoke VPNs and VPN Headends
	Hub and Spoke Technology
		VPN Headend
	Dynamic Multipoint VPN (DMVPN)
		IPSec for Security

Internet Protocol Security (IPSec)
	Layer 3 encryption protocol suite
	Authentication Header (AH)
		Provides authentication/integrity only
	Encapsulating Security Payload (ESP)
		Confidentiality and authentication/integrity
	IPv4 and IPv6 implementations
		Principles are the same, but the header formats are different

IKE and IPSec Models
	Internet Key Exchange (IKE)

Out of Band management Methods
	managed vs unmanaged appliances
	Management Interface
		Console port/command line interface (CLI)
		AUX port dial-up link
		management port (Connect over IP)
			Web interface
			Virtual terminal over Telnet/SSH (CLI)
	In band vs out of band - you connect in a different way than normal data (in band) or 