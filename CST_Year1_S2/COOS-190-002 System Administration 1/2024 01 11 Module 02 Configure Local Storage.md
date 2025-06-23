
# Overview
Introduces the basics of disks. Also covers distinct volume types supported by Windows Server 2022, and how to have faster and more fault-tolerant disks with RAID protection
# NOTES
### Configuring Disks and Volumes
Although the average disk capacity of storage devices has increased dramatically over the years, there is one thing you can count on - You will never have enough storage
Therefore, you need to know how to configure, manage, and support storage on windows clients
### Select a partition table format
Before you can use a disk, you must create partitions on it
*Partitions are physically and logically separated areas on a disk*
- Each partition can have a different file system
- Each partition is accessed through a drive letter or folder name
*Different operating systems can be installed on each partition*
Data about disk partitions is stored in a partition table (where each partition starts and stops)
*You can store different types of files on each partition*
- One partition contains the OS
- A second partition could be used to store documents
- A third partition could be used to store applications
### Terminology
The simplest way to describe a partition is as a physical subdivision of a storage device like a hard disk
A partition starts and ends at a specific point on the hard drive or in more advanced multi-desk setups it may be a segment on a virtual drive
*Operating systems generally treat partitions as if they were separate physical drives*
*A volume is a self-contained data unit.* It has a volume label (name), a single file system (Ex. NTFS/FAT32) and usually takes up the entire disk/partition
Formatting refers to the process of generating a new file system, creating a table to store the addresses and pointers to each cluster
The terms partition and volume are often used interchangeably. Microsoft tends to use the term Volume for Dynamic Disks and partitions for basic disks
*One major difference between partitions and volumes is that volumes can span multiple physical drives, whereas partitions consist of space on one disk*
### Configure Sector Sizes appropriate for Various Workloads
On disks, a sector is the minimum storage unit of a hard drive
For the disk, each sector is a fixed amount of user-accessible data
- slice of a track
Hard drives are traditionally 512 bytes, CD-ROMs and DVD-ROMs are 2048 bytes
An *allocation unit* also known as a *cluster* is the smallest logical amount of disk space that can be allocated to hold a file or folder
When you format the disks, you may be able to specify the size of the allocation unit, which can be from 512 bytes to 64KB. For a standard user, you should keep the default of 4096 bytes
**If you have a large amount of clusters, your system will be efficient on space (not very much space wasted), but it will be slow. The opposite is true if you use not very many clusters**
### Select a partition table format
Master Boot Record points you to the partition table
**Donovan said that some info on this slide was wrong**
The old standard for configuring disks is the *Master Boot Record* (*MBR*) in which
- Partition table must be stored in the disk's first sector of the disk
- If that sector gets physically damaged, you lose access to the partitions
- Limited to 4 partitions per disk
- Maximum disk size is 2TB
Primary Partitions can be made bootable
Extended partitions can contain many logical drives
The newer standard for configuring disks is the *Globally Unique Identifier* (*GUID*) partition table (*GPT*) in which
- *The partition table is stored in 2 places*, providing fault tolerance if one copy is damaged
- Can create up to 128 partitions
- Maximum disk size is 18 petabytes
### Select a disk type
Windows Server 2022 supports configuring disks as basic or dynamic
*Basic disks are the industry standard*
- Contain partitions
- Data about the partitions is stored in partition tables
- *All operating systems understand basic disks*
Dynamic Disks aren't industry standard (*Spanning across multiple drives by creating a partition on each drive and kind of linking them*)
- Dynamic disks contain *volumes*
- Data about the volumes is stored in a nonstandard database
Basic drives can be converted to dynamic disks non-destructively (preserver data)
Converting from dynamic to basic is destructive (lose all data)
*Enhanced Integrated Drive Electronics* (*EIDE*) is a very old standard
- slow and limited to 128GB
*Serial Advanced Technology Attachment* (*SATA*) replaced EIDE
- Much faster interface
*Small Computer system interface* (*SCSI*) provides faster speeds than SATA and
- SCSI controllers offload processing form the computer's processor
- Highly reliable and supports features such as hot-swapping
*Serial Attached SCSI* (*SAS*) is much faster evolution of SCSI
- Serial communication
*Solid-State drive* (*SSD*)
- Not an interface, so it's different than the things up above
- No moving parts, data is stored in chips
- Very fast, uses less energy, more resilient (Hard drives wear out because they spin, so it fails due to mechanical failure. *SSDs have the issue of wearing out from writing to the chips*)
### Defragmentation
*Takes all the files and "reorders" them so that they are all in order again instead of being spread out*
SSDs don't do this
### Select a file system
After disks have been initialized as MBR or GPT and the disk configured as basic or dynamic, the next task is to create partitions or volumes
- On a basic disk, make a partition
- On a dynamic disk, make a volume
There are many different types of file systems
- *File Allocation Table* (*FAT*) - 2GB partition size, 2GB file size - Newer versions support up to 8PB (8,192 TB)
- *New Technology File System* (*NTFS*) - 256TB partition size, file size is limited by the volume
- *Resilient File System* (*ReFS*) - 1 yobibyte (2^80 bytes), 16 exbibytes (2^64 bytes) file size - Good for redundancy and protection
![600](Pasted%20image%2020240111141852.png)
Technical details
- File allocation tables are typically located on the disk's first sector
- There are 3 major variants of file allocation tables - FAT12, FAT16, FAT32
![700](Pasted%20image%2020240111142017.png)
- main thing with NTFS is it has compression, uncompressed the file onto memory when you want to use the file
- With NTFS you can only encrypt or compress your files, not both
- Journaling - records if a file that was being written was stopped for whatever reason so it can be resumed
- Alternate Data Streams (ADS) make it compatible with MacOS
Apple stuff (**DON'T NEED TO KNOW**)
![600](Pasted%20image%2020240111143002.png)
### Implement Resilient File System (ReFS)
![600](Pasted%20image%2020240111143117.png)
*Designed for people who want huge file systems with lots of resiliency*
![700](Pasted%20image%2020240111143210.png)
![700](Pasted%20image%2020240111143323.png)
![700](Pasted%20image%2020240111143431.png)
![700](Pasted%20image%2020240111143456.png)
![300](Pasted%20image%2020240111143700.png)
![400](Pasted%20image%2020240111143710.png)
# ReFS Demo
1. Initialize the disk
2. Make a simple volume (NTFS format)
3. Open CMD as admin
4. convert drive we made to ReFS format
### Converting from the command line
fsutil - opens file system util (drive has to already exist)
fsutil fsinfo volumeinfo e: - gives info for the drive we made
fsutil fsinfo volumeinfo e: - after converting the format to ReFS
### Making a Virtual Hard Disk (VHD)
right click on the right action pane, configure size and format, name it (opens file manager like you're making a file)
VHD will now show up in Disk Manager as if it's a physical disk
Initialize all disks
Make a partition on your new VHD, we used FAT
You can see your new volume in file explorer as if it's a normal drive, but you can also see it as a file in the drive we made it on
right click and click "detach VHD" to detach it, **BUT NOT DELETE THE FILE**
you can also mount the VHD from file explorer, which will make it show up like a normal physical drive again
you can also right click and "eject" from file explorer which does the same thing as detaching in Disk Management