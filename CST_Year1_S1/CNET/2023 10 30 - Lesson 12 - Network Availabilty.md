Secure Shell (SSH)
	Used to remote into command line on another system
	Used on TCP/22

Server Authentication by a host key
	Client Authentication
	Username/Password
	Public Key Authentication
	Kerberos

Telnet
	client-server protocol over TCP
	Allows remote control of PCs via text input
	Unsecure command line interface over port TCP/23, not used much anymore because security
	Plaintext Protocol - no security
	typically disabled
	similar to PuTTY

Remote Desktop Protocol
	GUI remote administration over TCP/3389
	Session can be encrypted
	Range of clients for different PC and Mobile operating systems
	requires a better connection

Network Time Protocol (NTP)
	Essential service
	Critical time services - Authentication, logging, task scheduling, backup etc.
	NTP servers use an accurate time source (i.e. Atomic clock), so clients can connect to them to synchronize and have an accurate time.

Performance Metrics, Bottlenecks, and Baselines
		Bandwidth, throughput, CPU and memory resource, storage resource, goodput
	Bottlenecks
		Pinch points that cause the system to underperform
	Performance Baseline
		Record metrics as comparison
		Update Baselines

Environmental Monitoring
	Environmental sensors detect factors that could affect the integrity/reliability of an appliance
	Device Chassis sensors
		Temperature, fan speed, voltage fluctuation, intrusion
	Ambient Sensors
		Temperature, humidity, electrical, flooding

Simple Network Management Protocol (SNMP)
	Agents
		Manage Information Base (MIB)
		Object Identifier (OID)
		Community Name
		Read/only or read/write access
		Traps
	SNMP Monitor
		Get, Trap, walk
		Ports UDP/161 (queries) and UDP/162 (traps)
	Walk - get all information
	Trap - Tells the PC when something is wrong
	Get - Tells you one bit of information

Network Device Logs
	Performance, troubleshooting and security (auditing) information
		Metadata + event description
	Log types
		System and application logs
		Audit logs
		Performance/traffic logs

Log collectors and Syslog
	Centralized collection of events from multiple sources
	Syslog protocol for forwarding over UDP/514
	Syslog open format for log messages
		PRI Code
		Header
		Message
		might use spaces or comma delimiters

Event management
	Windows
		Information, warning or critical
		Audit success or fail
	Syslog severity levels
		0 (emergency) down to 7 (debug)
	Logging level and alert configuration
		Threshold
		Alert vs notifications and alarms
		Ticket systems

Log reviews
	Monitoring - looking at data in real time (checking task manager)
	Review - Collect the data and review it at a later time
	Trends
	Graphing

Topic 12C - Use Performance Metrics

Network Metrics
	Applications requirements for high bandwidth and sensitivity to delay (QOS)
	Bandwidth
		Speed, throughput, goodput
		Calculating requirements for audio and video
	Latency and jitter
		Signal delay measured in milliseconds (ms)
		Variation in delay
		Measurement tools (pathping and mtr)
		One-way vs Round Trip Time (RTT)

Bandwidth Management
	Provision higher bandwidth links (better routers, etc.) or prioritize traffic classes using:
	Differentiated Services (DiffServ) (Layer 3)
		Type of Service field in the IPv4 Header/Traffic Class in IPv6
		Router policies can then be defined to use the packet classification to prioritize the delay

Traffic Shaping
	Class of Service (CoS) - make individual choices per packet
	Quality of Service (QoS) - 
	Traffic shaping - delays packets
	Traffic policing - deletes packets

Interface Monitoring Metrics
	Link State
		Uptime and downtime
	Resets
	Speed
	Duplex

Trouble