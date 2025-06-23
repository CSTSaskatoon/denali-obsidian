# LO2
### What is the difference Between a disk and a volume?
### How many Primary partitions can you have on a table?
### What are the two standard disk configurations?
### What are the different types of Dynamic Volumes?
### What is Defragmentation

# Brody's Questions
#### Part 1
Server 2022 Editions
- Essential, Standard, Datacenter
Core-Based licensing model
- MS makes you pay more if you want a better server computer
Semi-Annually Channel (SAC)
- Update your OS semi annually (Microsoft makes these updates include just key features)
Long-Term Servicing Channel (LTSC)
- OS is no longer updated, but support for it is still there, lasts much longer than the SAC
Server Core
- Only CMD line stuff, a few applications have graphical interfaces
- Much less resource intensive
In-Place upgrade
- Upgrade your OS (Windows 10 -> 11) without re-installing
- May cause issues with applications
Server Migration
- Moving your server from one computer to another one
- Very little downtime
- Usually it's an upgrade, going from Windows 10 -> 11 or something
Key Management Services (KMS) server
- Managed by network administrator
- Keys are lent out to workstations for a certain period of time
- Keys are bought in bulk form MS
#### Part 2
Partition Tables
- Tells the computer where files are
Partitions
- Logical separations on a dynamic disk
Volume
- Logical separations on a simple disk
Sector
- Set by the manufacturer
- Like clusters, but you can't change them
Allocation Unit (Cluster)
- How big your data chunks will be grouped into
- Bigger = better performance, worse space management
Basic Disk
- Recognized by all operating systems
- Don't have stiped, mirrored, RAID (Software side), or spanned
Dynamic Disk
- Windows Proprietary
- more advanced storage configurations for more parity/redundancy or space
SCSI and iSCSI
- old hard drive configuration
- iSCSI is newer
FAT
- File allocation Table
- Good performance, but can't hold that much space
NTFS
- New Technology File System
- Windows Proprietary
- gives you access to encryption and sharing
ReFS
- Can be a lot bigger storage than NTFS, but not as much features
- Good redundancy
- Only really good if you have a ridiculously large file server
VHD
- Virtual Hard Drive
- Used for VMs
- Essentially just a file
RAID 0,1,5
- 0 - No parity, if one drive fails they all go (Striped)
- 1 - If one drive fails, you have a backup (Mirror)
- 5 - Minimum 3 drives, it has parity on each of them so it's able to restore data if only one of the drives is destroyed
Striped
- Must be on dynamic Disk
- Splits the data across multiple drives
- If one drive fails it's fucked
Spanned
- When one drive is full, it writes to the next one
- Must be on dynamic disk
- Only lose data on drive that's destroyed
Mirrored
- Must be on dynamic disk
- Everything that's written on disk 1 is also written on disk 2
- parity level 1
- can lose 1 disk with no data loss
- kinda space inefficient
parity
- redundancy
- If you lose some data on a drive you can recover it by doing some magic with the drive's bits
MBR
- Master Boot Record
- Tells the PC where all the hard drives are when the computer boots up
GUID
- Newer version of GUID
- has info on disk information
- Needed if you're using Dynamic Drives
#### Part 3
DAS
- Direct Attached storage
- drives attracted to the server
NAS
- Network Attached Storage
- drives attached to something like the router
SAN
- Server attached storage
- Drives have their own part of the network
File level storage
- No idea
Block Level Storage
- No idea
Object level storage
- no idea
Fiber channel
- Don't remember
iSNS
- No idea
DCB
- No idea
MPIO
- Mulltipath input/output
NFS
- Network File share
- windows proprietary
- permissions
SMB
- server message block
- works on linux
- generic
- not very many permissions
Direct Access Storage
- lets you get storage from the server faster
Network
- Bruh
Storage area network
- no idea