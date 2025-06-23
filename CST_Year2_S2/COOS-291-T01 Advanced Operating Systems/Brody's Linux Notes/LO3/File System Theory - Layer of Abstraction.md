[[#Linux File System Structure]]

---

Ext file system families. We are using Ext4, the modern version. They have a fixed number of inodes.

Old version had problems with power outages, and now has journaling. They now have large file system support.

XFS and Btrfs exist too.
XFS is used by Red Hat by default, it has its own version history and journaling. This has many commonalities to ext. This has the benefit of running large file systems.
Btrfs is newer and Red Hat almost moved over to it. It had advanced features like built in snapshots, compressions, and copy-on-write technique to eliminate file corruption.

Basically, ext has "extents" for file allocations instead of simple rigid blocks for continuous space use.
## Linux File System Structure

---

In Linux, everything starts at the root, it does not have a name because nothing contains it.
Directories are files that stores a list of files with their names and "inodes" or index node.

Devices/disks are mounted at different locations in the file system at mount points.
View mount points with `df -Th`.

### Inodes

Like superblocks, these data structures store metadata. These do not store file names or data, only pointers.
They have data like owners, permissions, and other file "stats".
`stat` can look at this data.

### Terminology

Data blocks

Block bitmap

inode bitmap

pvremove can save a disk's data when removing it from a volume grouped.