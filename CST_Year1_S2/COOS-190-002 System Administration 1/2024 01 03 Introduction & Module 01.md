---
quickshare-date: 2024-01-10 10:59:52
quickshare-url: "https://noteshare.space/note/clr810avy159301mwr172s8h0#bKapp3+KLjL14cwrvY+4achzqxA1p1S58oyMC7AQ2oU"
---
EXAMS ARE NOT CUMULATIVE (Final only includes material covered after the second midterm), and the 2 midterms and final are all worth 28%
15% of grade is quizzes/labs (5 quizzes, 4 labs randomly marked)
Xtremelabs bundle - https://store.xtremelabs.io/product/saskatchewan-polytechnic-20740wv-55382-installation-storage-and-compute-with-windows-server-prof-onishenko-/276?cp=true&sa=false&sbp=false&q=false&category_id=45
Xtremelabs link I found so I don't have to buy the bundle - https://www.xtremelabs.io/products/copy-of-55315-introduction-to-sql-databases?_pos=1&_sid=4b2a78110&_ss=r
Textbook link - 
# NOTES - Module 1
### Keywords/Abbreviations
- Software-Defined networking (SDN)
- Microsoft Management Console (MMC)
- Remote Server Administration Tools (RSAT)
- Long-Term Servicing Channel (LTSC)
- Password Export Server (PES)
- Generic Volume License Key (GVLK)
### Overview of Windows Server
- Windows server is a line of operating systems that Microsoft specifically creates for use on a server
- In almost all cases, Windows Server is only used in business environments
- Windows Server 2022 is the latest version

### How to select a suitable Windows Server 2022 edition
- Windows Server 2022 Essentials - Small business, not an actual server, works more like a workstation (25 Devices)
- Windows Server 2022 Standard - Can run 2 virtual servers
- Windows Server 2022 Datacenter - Few more features, more virtualization capacity
- Datacenter: Azure Editions - Cloud based, not really in the same realm as other windows servers
### Standard vs Datacenter
- Most of the same features
- Major differences between the 2 are the number of virtual servers you can creates under the license of the host OS, support for certain Hyper-V features	
- Standard edition - One physical server, 2 virtual servers on it	
- Datacenter edition - One physical server, unlimited virtual servers
- Datacenter features not in Standard
- Software-Defined networking (SDN) and Network Controller. Centrally configure your network from the server

### Hardware Requirements
- Processor Architecture 64-bit to 64-bit
- Processor Speed 1.4 Ghz single processor to 64 processors, unlimited number of cores
- RAM 2GB or 512MB for server core to 48TB
- Hard Drive Space 36GB to unlimited

### Core-based licensing model
- If you have Windows server Standard or Datacenter editions you have a core-based licensing model
- Number of licenses you need is determined by the number of server cores inside the number of processors
- Rules
	- Every Processor must be licensed to cover a minimum of 8 cores
	- Every server must be licensed to cover a minimum of 16 cores
	- All Physical cores in the server must be licensed
- After you have your cores figured out, you need additional Client Access Licenses (CALs) to cover every user device that connects to the server (Includes devices likes printers)
- Example
	- Server 2022 Standard 16 core + 20 User CAL is about $1300CAD (Datacenter is $6000) additional cores are $100 each but must be bought in groups of 2

### Installation Process and Options
- You can install Windows Server from
	- ISO burned to DVD
	- ISO attached to VM
	- Virtual Hard Disk file
- During the installation process you are prompted for
	- Language, time, currency format, keyboard layout
	- Install now or Repair your Computer
	- License Agreement
	- Upgrade or custom installation
	- Operating System edition
	- Hard disk space allocation

### How can you manage Windows Server remotely
- Windows Admin Center
- Remote Desktop
- Microsoft Management Console (MMC)
- Server Manager
- Command-line tools (Cmd and Powershell)
- Remote Server Administration Tools (RSAT)

### Windows Server updates and servicing channels
- Beginning with windows server 2022, the Long-Term Servicing Channel (LTSC) is the only primary release channel available
- Can configure updates in Server Manager
- Recommended to use "Download updates automatically and notify when they are ready to be installed"
- The Semi-Annual Channel receives twice-yearly updates, once in spring and once in fall. These contain new features, services and other major changes. Security updates, optimizations and other minor updates or patches are released the month after
![500](Pasted%20image%2020240103093317.png)
### Core Overview
- More security enhanced, less resource-intensive installation option than the desktop experience installation
- Default installation option for Windows Server
- Managed locally using windows PowerShell and other standard tools
- Cannot be converted to Server with Desktop Experience
- Some roles and features are not supported on Server Core
- Tools in server core
	- Powershell
	- CMD
	- Sconfig.cmd
	- Regedt32.exe (Graphical)
	- Msinfo32.exe (Graphical)
	- Taskmgr.exe (Graphical)
	- may be few more
##  2024 01 08 - Lesson 3 - In place Upgrade
### In-place upgrades vs Server Migration
#### When you perform an in-place upgrade, the current Operating System (OS) is replaced by Windows Server 2022
- Before starting, create a list of the hardware and software running on the server. Is everything supported? Need drivers?
- Create a complete backup of the server
- During an in-place upgrade, the server will become unavailable on the network
#### Migration refers to performing a clean install of Windows Server 2022 on new hardware and then migrating settings, applications and data from the old server
- Migrations are useful when an upgrade isn't suitable or possible
- Unlike an upgrade, you can perform migrations without disrupting existing network functionality
- Windows Server 2022 includes some tools to help with migrations
### Migration
A migration begins with a clean install on a new server. After, you will need to:
- Install any required applications
- Other stuff
#### When to perform an in-place upgrade
- The hardware config of the existing servers meets the requirements for Windows Server 2022
- The software products that run on existing servers support in-place uprades
- You want to keep all user data and permissions that is on the existing servers
#### Migration benefits
- Doesn't affect the current IT infrastructure
- You perform product migration in a separate environment
- You perform migration of server roles, features, and settings in a separate environment
- New OS enhancements are installed by default
#### Migrate server roles and data within a domain
- Enables you to migrate data from multiple sources on a single server
- The primary usage scenario for Storage Migration Services is to migrate an existing file server on to a new one
- Integrated as part of Windows Admin Center
- During migration, it assigns the identity of the source server to the target server. This includes the server name and teh server IP address
- can also migrate local user accounts 
#### Storage Migration Services
- Phases
	- Makes inventory of souce servers to obtain data about files and config
	- Performs data transfer
	- more
- Server Migration Tools
	- Cmdlets migrate config info and data
	- Need to install required Cmdlets on both servers
- Lets you migrate:
	- IP Config
	- Local users and groups
	- DNS
	- DHCP
#### Migrate server roles across domains or forests
Microsoft offers the active directory Migration tool (ADMT) to simplify migrating user, group, and computer accounts
ADMT can perform
- User account Migration
- Group account Migration
- Computer account migration
- Service account migration
- Trust relationship migration
- Microsoft Exchange Server migration
- Security translation of migrated user accounts
- Rollback and retry operations if transient failures occur
If you're defining a new naming structure for users or groups, you can implement that as part of the migration process
When you migrate user objects, all attributes are migrated by default
- Possible to filter out attributes in the migration process if the attribute's values are no longer valid
If you're using password sync, you have to install Password Export Server (PES) on a DC in the source
- PES is responsible for exporting user password hashes to the source
- if you don't use PES, users will need to make a new password
#### Solution accelerators for migrating to the latest Windows Server Edition
When you're considering deployment, you can use software tools to help you design the deployment
Microsoft Deployment Kit (MDT)
#### Considerations/recommendations
Placement of server roles (AD DS, DNS, DHCP)
- Don't put DNS/DHCP on the same server as AD DS because DNS and DHCP are less secure
- DNS uses high memory low storage, DHCP uses low memory high storage so they fit together well
- cohosting is using VMs to keep the different servers separate on the same hardware
Plan which server server roles you need
## Lesson 4 - Licensing and activation for Windows Server
Licensing model overview
More info up above
Must purchase license based on physical hardware
### Windows Server Activation
Manual activation
- enter product key
- Only valid for single server
Automatic activation
- Deploying a key management servers (KMS) server
- Active directory-based activation
- Volume activation services server role deployed on an existing server
- Multiple Activation Key (MAK) each MAK has a predetermined number allowed activations and is based on your volume licensing agreement
Tools to help manage licensing and activation include
- Volume Activation Management Tool (VAMT)
- Automatic Virtual Machine Activation
#### Volume Activation Using KMS
![[Pasted image 20240108104937.png]]
#### Active Directory-based Activation
Windows 8 and higher
Generic Volume License Key (GVLK)
#### Virtual Machine Activation
Activation will only last 7 days
If you use AVMA you need to have a server running Windows Server 2012