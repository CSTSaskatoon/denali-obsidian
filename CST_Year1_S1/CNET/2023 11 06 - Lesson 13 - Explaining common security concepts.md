Objectives - Explain common security concepts and Authentication process

Security Concepts
	CIA - Confidentiality, Integrity, Availability
	Confidentiality
		Certain information that should only be known by certain people
	Integrity
		Data stored and transferred as intended, any modification needs Auth.
	Availability
		Information is accessible to those authorized to view or modify it
	Vulnerability, threat and risk diagram
		![[Pasted image 20231106081058.png]]
	Vulnerability
		Door without a lock
	Threat
		Someone might use the vulnerability (open the unlocked door)

Security Risk Assessments
	Posture Assessment (How many hoops someone has to jump through to get through security)
		Enterprise risk management
		Comparison with standard frameworks
		Assess use of security controls (Control = Solution)
	Process Assessment (Look at individual components of your security)
		Mission essential function (MEF) - secure the most important things first (servers)
		Business essential function (BIA)
		Business continuity planning (BCP) - How do you keep your business going when something happens? (Power going out)

Vulnerability and Exploit types
	Vulnerability - Something that can be used against you
	Exploits - Method where a vulnerability is used maliciously
	Zero-day exploits - known vulnerability but no known fix
	Unpatched legacy systems
	Vulnerability assessment
		Manual and automatic scanning
		Identify deviation from config baseline - Minimum amount of security you will need
	Common Vulnerabilities and Exposures (CVE)

Threat Types and Assessment
	Internal vs Internal threats
	Threat Assessment - signs and symptoms you might be under attack
		Identify adversary tactics, techniques and procedures (TTPs)
		Research Sources
		Data feeds for automated detection tools
			Behavioral threat research - examples of attacks and TTPs
			Reputational threat intelligence - lists IP addresses and domains associated with malicious behavior plus signatures of known file-based malware
			Threat Data - Computer data that can correlate events observed on a customer's own networks and logs with known TTP and threat actor indicators

Security Information and Event Management
	Log aggregation
	Event Correlation - Indicator of Compromise (IoC), Alerting
	Log Storage and Retention (compliance)

Penetration Testing
	Authorized or Ethical Hacking
	Goes beyond vulnerability scanning to actively test controls
	Pen testing is an intrusive assessment technique
	Even though the potential for the exploit exists, it might not be able to be used because of server permissions. A pen test might find this whereas a vulnerability scan wouldn't

Privileged Access Management (PAM)
	How much privilege a user has over the network
	Least privilege
	Role-based access
	Zero trust

Vendor Assessment
	Supply chain vulnerability management
	Onboarding Suppliers
	Validate supplier sercurity maturity level
		A vendor may supply documentation and certification to prove it has implemented a security policy robustly

Authentication

Authentication Methods and access controls
	Subjects and objects - subjects are users, objects are things on the system (windows sees everything as objects)
	Access control list (ACL) - list of subjects and rights/permissions they have been granted on the object
	Identify and access management (IAM) - Identification, Authorization, Authentication, Accounting

Multifactor and Two-factor Authentication
	Oftentimes, ease of use and security are opposites (Tap makes it easier to pay, but a lot easier to steal)
	Account identify and credentials
	Authentication factors/credential format
		Knowledge factor - something you know (password)
		Ownership factor - something you have (smart card)
		Human factor - something you are (fingerprint)
		Behavioral factor - something you do (signature)
		Location factor - somewhere you are (IP or GPS) - Netflix giving you different shows based on your country
	Multifactor requires more than one type

Local Authentication and single sign-on
	Cryptographic hashing of passwords
	Windows Authentication
		Local sign-in, windows network sign-in, remote sign-in
	Linux authentication
		/etc/passwd user file and /etc/shadow password file
		Secure Shell (SSH)
		Pluggable authentication modules (PAM)
	Single sign-on (SSO)
		Authenticate once - authorize many

Kerberos
	Kerberos Diagram
		![](Pasted%20image%2020231106092536.png)

Digital Certificates and PKI
	Public key cryptography (asymmetric encryption)
	Public key Infrastructure (PKI) authenticates the public key
	Subject is certificate holder (user or server)

Extensible Authentication Protocol and IEEE 802.1X
	Extensible Authentication Protocol (EAP)
	IEE 802.1X Port-based Network Access Control (NAC)
	Diagram
		![](Pasted%20image%2020231106093207.png)

Lightweight Directory Access Protocol (LDAP)
	List of network users and resources
	Access control lists (ACLs)
	Authorizations
	Directory Database (Objects and Attributes)
	X.500 Distinguished Names
		Attribute=Value Pairs
		Schema

LDAP Secure
	Binding Methods (Authentication)
		None
		Simple Authentication
		Simple Authentication and Security Layer (SASL)
		LDAPS (TLS over TCP port 636)
	Access Control Policy
		Read-only (Query)
		Read/Write (Update)

