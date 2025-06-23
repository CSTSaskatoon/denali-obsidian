Adding and managing disks, partitions management and setting up mount points.
Required to make drives network available (NFS).

#### Adding VM Hard Drive

Close VM, VM settings -> Hard Drive

Add, new drive and create new virtual drive.

### Partitioning Disk

SDA should be first disk, SDB should be second. Sometimes this is swapped.

List every drive.

```bash
sudo fdisk -l
```

```bash
sudo fdisk -l /dev/sdb
```

#### Making Partition

```bash
sudo fdisk /dev/sdb
p # Double check which disk is being used
g # GPT partition
p # Will show the new data
n # New parition
enter # Number 1 is nect
enter # 2048 Sector size default
+1G # Last sector (size), adding 1 GB
w # Write, aka save. q would quit
```

Disk has not been formatted yet.

#### Format the drive

Make filesystem
`mkfs.ext4` or `mkfs.xfs`

```bash
sudo mkfs.ext4 /dev/sdb1
```

This makes an unmounted super disk.

### Mount point

Root is top of the file system and no drive letters.
Create a location to tie to new partitions (mount point)

```bash
sudo mkdir /userdata
sudo mount /dev/sdb1 /userdata
```

Inside we can find a `lost+found`.

Take access with:

```
cd /userdata
sudo mkdir mydata
sudo chown student mydata
```

### Read File system

Show file system and where the files are mounted.

```
df -Th
```

#### Remove Mount

Cannot remove while file is being read.

```bash
sudo umount /userdata
```

##### Exercise

Create a 2GB partition on the new disk (sdb), format with ext4 and mount it to /studentdata.
