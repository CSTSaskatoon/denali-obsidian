## Q1
Create a new 500MB Logical volume called second, put an `xfs` filesystem on it, mount it at `/mnt/second`, make it persist on boot (Add to `ftsab`)
```bash
sudo lvcreate -L 500MB -n second coos
sudo mkfs.xfs /dev/coos/second
sudo mkdir /mnt/second/
sudo mount /dev/coos/second /mnt/second/

vi /etc/fstab
# Add this line to the file
/dev/coos/second /mnt/second xfs defaults 0 2 # 2 should be different depending on how many drive you have

sudo mount -a # optional, but just reloads everything from fstab, so you can make sure it's mounting correctly
```

## Q2
**I'm not actually doing this exercise because I feel comfortable with it already**
We want to go through and start from scratch therefore do following exercise after removing all `lv`, `vg`, `pv`, and extra `/etc/fstab` lines from the system (do not remove the original lines from `/etc/fstab`). 
1. Unmount any logical volumes that are currently mounted
	1. `df`  to identify
	2. `umount` to unmount (always leave System stuff alone `/` `/Boot` , `/dev`, `/sys` )
2. Delete All logical volumes from the system.
	1. `lvscan` to detect volumes
	2. `lvremove /dev/volGroup/LogicalVolume`
3. Delete all Volume Groups from system
	1. `vgscan` to detect
	2. `vgremove` to remove the volume groups
4. Delete all physical volumes from the system
	1. `pvscan` to detect
	2. `pvremove` to remove the physical volumes
5. Shutdown the system (`sudo shutdown –h now`)
6. Finally go through and delete the extra drives we created for the system from Hyper-V. You may also remove them from the filesystem as well by deleting them on Windows after removing them from your VM.

### Exercise Step 1
 1. With the Linux machine off – add 4 drives to the system in Hyper-V
 2. Drives 1 and 2: make these 1 GB in size
 3. Drives 3: make this 3 GB in Size
 4. Drive 4: make this 5 GB in Size

### Exercise Step 2
1. How can we identify which drive is which on the system? - `ls /dev/sd*` - lists all partitions/drives
2. Write the sizes down for reference
3. Fill in the following table:

|                                     |         |
| ----------------------------------- | ------- |
| Device (should start with /dev/sd…) | Size GB |
|                                     |         |
|                                     |         |
|                                     |         |
|                                     |         |
|                                     |         |

### Exercise Step 3
1. You can now create the physical volumes. Use the `pvcreate` command.
2. Run `pvdisplay` and fill out the following table:

|   |   |   |   |   |
|---|---|---|---|---|
|Physical Volume|Size GB|Volume Group Name|Allocatable|PE Size|
||||||
||||||
||||||
||||||

### Exercise Step 4
To create a volume group we have to specify
- The extent size (use 4 M)
- The name of the volume group
- The devices we want to include

1. let’s start out by creating a volume group with one of the smaller physical volumes (use the first one from the table above). Call this volume group `vg_exer`
2. We can then extend the volume group by adding additional disks to it - Do this for each of the physical volumes and then run `pvdisplay` again and finish the following table:

|   |   |   |   |   |
|---|---|---|---|---|
|Physical Volume|Size GB|Volume Group Name|Allocatable|Total PE|
||||||
||||||
||||||
||||||

### Questions
Question? What is PE referring to? 
- **Physical Extents, smallest units of space you can allocate in `lvm`/`lvm2`**

For the small volumes why is this value 255?
- It's the max size of **one Byte**
