## Q1
1. Create a 2GB partition on your new disk
2. Format the partition with `ext4`
3. Mount it to `/studentdata`

```bash
sudo fdisk /dev/sdb
n
+2G
w
sudo mkfs.ext4 /dev/sdb2
sudo mkdir /studentdata
sudo mount /dev/sdb2 /studentdata
```

## Q2
Add a new disk sized to 4GB and format two new partitions on the new `sdc`:
- 2GB `xfs` filesystem (you may have to install the `xfsprogs` package)
- `ext4` filesystem that uses up the remaining space

mount the new `xfs` filesystem `/data/cststaff/vms` 
mount the new `ext4` filesystem at `/data/cststaff/exams`
Write a file into each directory and test that it is on the new disks.

Ensure that the file mounted at `/data/cststaff/exams` will be mounted automatically after reboot. Test by rebooting your system - `/data/cststaff/vms` should no longer have the disk mounted, but `/data/cststaff/exams` should still have `/dev/sdc2` mounted. Use the `df` command to check.
Make a group called `examaccounts`
Two users in the group `exam1` and `exam2` with home directories under `cststaff/exams/e1` and `cststaff/exams/e2`
Try logging in as them and making a few files with touch etc. in their home directory.
Switch back to your administrator user and unmount the `/data/cststaff/exams` mount point, then login again as one of the exam accounts – what happens when they try to cd into `~`?

```bash
# Create new virtual drive in Hyper-V
sudo apt-get install xfsprogs
sudo fdisk -l /dev/sd* # Verify which drive is new, shouldn't have any paritions yet. In my case it's sdc
sudo fdisk /dev/fdc

g # create new GPT partition table
n # create new partition
enter # default
enter # default
+2G # 2 GB

n # new partition
enter # default
enter # default
enter # default - take up the remaining space on the drive

p # print partition table, verify it's what you want
w # write the changes to the disk and exit

sudo fdisk -l /dev/sdc* # see your new partitions on the drive
sudo mkfs.xfs /dev/sdc1 # format first partition as xfs
sudo mkfs.ext4 /dev/sdc2 # format the second partition as ext4

# Make /data/cststaff/vms and /data/cststaff/exams
sudo mount /dev/sdc1 /data/cststaff/vms
sudo mount /dev/sdc2 /data/cststaff/exams

sudo blkid /dev/sdc2 # get the UUID for the first partition
sudo vi /ect/fstab
# Add your UUID you got form blkid in here like /dev/disk/by-uuid/$ID_HERE /data/cststaff/exams ext4 default 0 3

sudo addgroup examaccounts
sudo adduser exam1 --ingroup examaccounts --home /data/cststaff/exams/e1
sudo adduser exam2 --ingroup examaccounts --home /data/cststaff/exams/e2

# User accounts and their home directories are now created, what happens if you unmount the drive?
sudo umount /dev/sdc2
su exam1 # switch to their user
```