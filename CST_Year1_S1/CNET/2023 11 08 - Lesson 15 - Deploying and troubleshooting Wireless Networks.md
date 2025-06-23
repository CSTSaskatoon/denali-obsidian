Objectives - Wireless standards

IEEE 802.11 Wireless Standards
	WIFI modulation and carrier methods
	Carrier sense Multiple Access with collision avoidance (CSMA/CA)
		Ack undamaged frames
		Request to send/clear to send - need to ask machine if the network is clear and then send it
		half duplex
	Original data rate just 1Mbps
	Wired of the same spec is ALWAYS faster than wireless
		You can have a wireless connection that is faster than a wired connection, but if you use the same specs wired will always be faster
	Wireless Standards Diagram
		![](Pasted%20image%2020231108093851.png)

IEEE 802.11a and 5 GHz Channel Bandwidth
	2.4 GHz - Better propagation, but fewer channel and greater interference risk
	5 GHz - Lower range, but less congested, lose energy fast, get blocked easily (hard to go through walls, water, etc.)
	IEEE 802.11a (54Mbps)
		Original and 5 GHz
		Orthogonal Frequency Division Multiplexing (OFDM)
		23 x non-overlapping 20 MHz channels
		Dynamic Frequency Selection (DFS) and regulatory impacts

IEEE 802.11b/g and 2.4GHz Channel Bandwidth
	IEEE 802.11b (11Mbps)
		Direct Sequence Spread Spectrum (DSSS), along with complimentary code Keying (CCK) signal encoding
		14 x 5 MHz channel bandwidth
		WIFI still needs 20MHz channel bandwidth
		Channels need careful config to avoid overlap
	802.11g (54Mbps)
		OFDM
		802.11b compatibility mode
	2.4GHz WIFI frequencies in GHz
		![](Pasted%20image%2020231108095219.png)

IEEE 802.11n, MIMO, and channel Bonding
	Single user Multiple input multiple output (SU-MIMO)
		Ax:Bc transmit and recieve antennas plus maximum simultaneous streams
		Spatial multiplexing and spatial diversity
	Can use 5 GHz or 2.4 GHz bands with channel bonding
	High throughput (HT)/greenfield
		288.8 Mbps for single channel and 600 Mbps for bonded channels
		HT Mixed mode for compatibility with older standards
	In recent years, Wi-Fi standards have been renamed with simpler digit numbers. 802.11n is now officially Wi-Fi 4

WiFi 5 and WiFi 6
	WiFi 5 (802.11ac)
		5 GHz only
		80 or 160 MHz channel bonding
		up to 8 spatial streams
		Denser modulation
		1300 Mbps
	WiFi 6 (802.11ax)
		More complex modulation and signal encoding to improve the amount of data sent per packet by about 40%
		High Efficiency (HE)
		2.4 or 5 GHz (and new 6 GHz band)
		Enhancements to support internet of things devices (IoT)
			OFDM with multiple access (OFDMA)
			Not so much throughput, but less latency

Multiuser MIMO
	Beamforrming - using ripples of signals to amplify signal in one direction
	Downlink MU-MIMO (DL MU-MIMO)
		Seperate signals by alignemnt
		up to 4 in WiFi 5 and 8 in WiFi 6
	Uplink MU-MIMO (UL MU-MIMO)

4G and 5G Cellular Technologies
	Long term evolution (LTE) for 4G
		Convergence between the GSM and "CDMA" camps - uses Orthogonal Frequency Division Multiple Access (OFDMA)
	5G
		Aims for 1Gbps but achieves 50-300 Mbps
		uses hundreds of small antennas in different frequency bands unlike current wireless cells
		Fixed-Wireless broadband solutions
		uses the same frequency and such, just crams the data better so you can fit more

Infrastructure Topology and Wireless Access Points
	In an infrastructure topology, each station is configured to connect through a base station or access point (AP), forming a logical star topology.
	Access Point (AP) - Bridges wireless stations (STA) and cabled network
	Basic Service Set (BSS)
		MAC address of AP is used as Basic Service set identifier (BSSID)
		More than one BSS can be grouped together in Extended Service Set (ESS)

Wireless Site Design
	Service Set Identifier (SSID)
		Multiple BSS with the same SSID form and extended Service Set (ESS)
	SSID Broadcast and beacon frame
	Speed and distance requirements
		Max indoor and outdoor ranges vary by standards and conditions
		Radio sources interference
			Competing wireless networks
			Other devices/standards (Bluetooth)

Site Survey/Heat maps
	Inspect floor plan and rooms to identify obstructions
	Plan cells to provide good coverage of the area (Device density, Bandwidth per device)
	Use wireless survey tools to identify signal strength and channel utilization (heat map) to map the basic service area (BSA)

Wireless Roaming and Bridging
	Extended Service Area (ESA)
		Distribution System (DS) where wired network connects Access points via switches
		Access Points use different channels to avoid interference
		Access points all use the same SSID (Extended SSID/ESSID) and security config
	Disassociation/Reassociation
	Wireless Distribution System (WDS)
		Channels, SSID and security configurations must be the same
		Repeater mode
		One AP becomes the base station and is connected to the wired network
	Wireless Bridges
		When WDS is configured in bridge mode, the APs will not support wireless clients, they simply forward traffic between cabled segments

Wireless LAN controllers
	Manage Tens or hundreds of access points
	Appliance or software solution
	Access point governed by controllers is "thin" or "lightweight"
	Lightweight Access Point Protocol (LWAPP)
	VLAN Pooling
	Provide power over ethernet

Ad Hoc and Mesh Topologies
	While most corporate and many SOHO networks are configured in infastructure mode, there are also wireless topologies that allow stations to establish p2p links
	Ad Hoc - p2p or independant basic service set (IBSS)
	Mesh

Wireless performance assessment
	Wireless Issues can be broadly divided into issues with signal strength or interference
	Speed vs Throughput
	Distance
		Radio Frequency (RF) attenuation or free space path loss
		Doubling distance quadruples signal loss
		Decibel, a logarithm (equal to 10 times) ratio of the difference between two values
		dB quantifies the ratio between two values, whereas dBm expresses the absolute power level
		A 3dB gain means (x2) the power. A 3dB loss means half the power. For example, a system with 40 watts of power and a 6dB insertion loss will only have 10 watts of output power

Signal Strength
	Received Signal Strength Indicator (RSSI)
		Up to -65 dBm is a good signal
		-80 dBm is at the limit
	Signal to noise ratio (SNR) - Noise you want really small numbers (-80), Signal you want to be close to 0
	WiFi analyzers

Antenna Types
	Omnidirectional - stick that radiates in a donut shape
	Unidirectional (Yagi and parabolic)
		Signal can be focused in one direction to increase signal strength
		gain measured in dBi (Decibel isotropic) units
		Beamwidth (Directionality) in degrees
	Polarization

Insufficient Wireless Coverage Issues
	Solutions
		Add access point
		configure wireless bridge
	Antenna placement and type
		unidirectional is for point to point not general coverage
	Antenna cable attenuation
	Effective isotropic radiated power (EIRP)

Channel Utilization and Overlap Issues
	Co-channel interference
	Adjacent channel interference
	Channel layout
	Transmit power and site survey
	Overlap for roaming

Overcapacity Issues
	High number of stations overwhelming access point
		25-30 clients per AP as general rule

Interference Issues
	Reflection/Bounce - mirrors/shiny reflection
	Refraction - glass/water can cause radio waves to bend and take a different path to the receiver
	Absorption/Environmental factors - some of the radio waves energy is lost as heat when passing through a wall
	Electromagnetic Interference (EMI) - Interference from a powerful radio or electromagnetic source working in the same frequency band (Microwave)

WiFi encryption standards
	WiFi encryption is pretty much useless
	WiFi Protected Access (WPA)
		can be cracked in 30 seconds
	WPA2
		Slightly better than WPA but the key is based on the router password, easy to crack still

