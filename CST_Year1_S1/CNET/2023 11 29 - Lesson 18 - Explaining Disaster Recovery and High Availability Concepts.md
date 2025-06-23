Availability and High Availability
	High Availability
		Percentage Uptime
		Maximum Tolerable Downtime (MTD) - # of nines *(99.9999%)*
		MTD of systems vs devices (System is redundant devices to minimize downtime)
	Recovery Metrics
		Recovery Time Objective (RTO) (x number of minutes/hours you want to fix the device in)
		Work Recovery Time (WRT)
		Recovery Point Objective (RPO) (How much data are you willing to lose?) - usually still measured using a timeframe *(We lost a DAY of data, not we lost 20GB of data)*

Fault Tolerance and Redundancy
	Reliability Metrics
		Mean Time Between Failures (MTBF) (How long a hard drive should last on average)
			Operational Time / # of failures *(For example, if you have 10 appliances that run for 50 hours and 2 of them fail, the MTBF is 250 hours/failure (10 x 50)/2.)*
		Mean Time To Failure (MTTF)
			Used for non-repairable components
			Operational time / # of devices
		Mean Time To Repair (MTTR)
			Unplanned Maintenance / # of incidents
	Redundant System Types
		Hardware spares, network links, power systems, system and data backups, cluster services, ...

Recovery Sites
	Alternate processing sites that will not be affected by same disaster event
	Hot site
		Failover in seconds or minutes
	Warm site
		Failover in hours
	Cold site
		Failover in days
	Cloud site
		Transfer responsibilities to cloud provider
		Cannot transfer all the risk

Facilities and Infrastructure Support
	Heating, Ventilation, air conditioning (HVAC)
		Temperature sensors and moisture detection sensors
		Office areas versus datacenter/equipment rooms
	Fire suppression
		Use gases in server rooms cause water not good for computers and fire extinguishers corrode material
		Emergency procedures and alarms
		Portable extinguisher usage
		Sprinkler systems

Power Management
	Spikes, surges, brownouts, blackouts
	Power Distribution Unit (PDU)
		Filter and stabilize grid power and facilitate remote monitoring
	Battery backups and Uninterruptible Power Supplies (UPSs) - can also conditioning power (Sucks in power surges, uses it's charge to keep voltage consistent in brownouts)
		Battery-backed cache
		UPS runtime
	Generators
		Replacement for power grid
		Must be used with UPS
		Renewable power sources

Network Device Backup Management
	Network Appliance Configuration Backup
		Startup vs running config
		Version history and rollback
	Backup Modes
		State/bare metal
		Config file
	Backing up/logging other state information

Explain High Availability Concepts

Multipathing
	Multiple physical links between nodes
		Routed internetwork
		SAN Mulitpathing
		Multiple ISPs
	Diverse Paths
		Ensure physical separation of first mile links to ISPs
			Could be different cables or include cellular, satellite or other radio systems
		Ensure independence of ISP's networks

Link Aggregation/NIC Teaming
	Bundle multiple physical links into a single channel (Redundancy, faster speeds)
	Channel can use combined bandwidth of links
	Channel redundancy against link failure
	Port Aggregation is done on the switch's side not the NIC
	IEEE 802.3ad/802.1ax
		Link Aggregation Group (LAG)
		Link Aggregation Control Protocol (LACP)

Load Balancer
	Distribute Client Requests
	Placed in front of server farm or resource pool
	Layer 4 switch vs layer 7 switch - Layer 7 is more about the content, more "Smart"
	First method is round robin *(Request 1 goes to server 1, request 2 goes to server 2 and so on - Issue with this is it doesn't take into account if one server is better than the other.)*

Redundant Hardware/Clusters
	Nodes that must share common data
	Virtual IP
		External Address for service shared by processing nodes
		The instances are configured with a private connection, on which each is identified by it's "real" IP address.
			Runs some type of redundancy protocol, such as Common Address Redundancy Protocol (CARP) that enables the active node to "own" the virtual IP and respond to connections
	Active passing and active active clustering

First Hop Redundancy
	Provision multiple default gateways without complex routing on hosts
	Hot Standby Router Protocol (HSRP)
		Routers share common virtual IP and MAC
		Standby group with priority standby router
	Virtual Router Redundancy Protocol (VRRP) - No Specific Standby
	Cluster - Servers know what each other are doing, acts as one machine.
	Load Balancing - Simpler, cheaper, but the servers don't know what each other are doing so if you have to switch servers it doesn't know what you were doing.

