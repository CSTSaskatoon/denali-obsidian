# LVM Commands Breakdown

## Fdisk
A utility to create partitions that can be used with LVM.

**Purpose**: Create partitions (e.g., /dev/sdb1) or use entire disks (e.g., /dev/sdb) for LVM.

**Example**:
```bash
# Create a new partition on /dev/sdb
fdisk /dev/sdb
# Then follow the prompts to create a new partition
# n (new partition) -> p (primary) -> 1 (partition number) -> Enter (default start) -> Enter (default end) -> t (change type) -> 8e (Linux LVM) -> w (write changes)
```

## Physical Volume Tools

### pvcreate
**Purpose**: Initializes a disk or partition as a physical volume for use with LVM.

**Example**:
```bash
# Create a physical volume on partition
pvcreate /dev/sdb1

# Create a physical volume on entire disk
pvcreate /dev/sdc
```

### pvdisplay
**Purpose**: Shows detailed information about physical volumes.

**Example**:
```bash
# Display all physical volumes
pvdisplay

# Display a specific physical volume
pvdisplay /dev/sdb1
```

### pvs
**Purpose**: Shows concise information about physical volumes.

**Example**:
```bash
# Display all physical volumes in a compact format
pvs

# Display with specific columns
pvs -o pv_name,pv_size,pv_free
```

### pvremove
**Purpose**: Removes the LVM label from a physical volume.

**Example**:
```bash
# Remove a physical volume from LVM
pvremove /dev/sdb1
```

### pvmove
**Purpose**: Moves data from one physical volume to others in the same volume group.

**Example**:
```bash
# Move all data from /dev/sdb1 to other PVs in the same VG
pvmove /dev/sdb1

# Move data to a specific destination
pvmove /dev/sdb1 /dev/sdc1
```

## Volume Group Tools

### vgcreate
**Purpose**: Creates a volume group from one or more physical volumes.

**Example**:
```bash
# Create a volume group named "vg_data" using two physical volumes
vgcreate vg_data /dev/sdb1 /dev/sdc1
```

### vgdisplay/vgs
**Purpose**: Shows information about volume groups.

**Example**:
```bash
# Detailed information about all volume groups
vgdisplay

# Detailed information about a specific volume group
vgdisplay vg_data

# Concise information about all volume groups
vgs
```

### vgextend
**Purpose**: Adds physical volumes to an existing volume group.

**Example**:
```bash
# Add a new physical volume to an existing volume group
vgextend vg_data /dev/sdd1
```

### vgremove
**Purpose**: Removes a volume group.

**Example**:
```bash
# Remove a volume group
vgremove vg_data
```

## Logical Volume Tools

### lvcreate
**Purpose**: Creates a logical volume within a volume group.

**Example**:
```bash
# Create a 10GB logical volume named "lv_apps" in volume group "vg_data"
lvcreate -L 10G -n lv_apps vg_data

# Create a logical volume using 80% of the available space
lvcreate -l 80%VG -n lv_data vg_data
```

### lvdisplay/lvs
**Purpose**: Shows information about logical volumes.

**Example**:
```bash
# Detailed information about all logical volumes
lvdisplay

# Detailed information about a specific logical volume
lvdisplay /dev/vg_data/lv_apps

# Concise information about all logical volumes
lvs
```

### lvremove
**Purpose**: Removes a logical volume.

**Example**:
```bash
# Remove a logical volume
lvremove /dev/vg_data/lv_apps
```

### lvresize
**Purpose**: Changes the size of a logical volume.

**Example**:
```bash
# Increase the size of a logical volume by 5GB
lvresize -L +5G /dev/vg_data/lv_apps

# Resize the logical volume and its filesystem in one command
lvresize --resizefs -L 20G /dev/vg_data/lv_apps

# Reduce the size of a logical volume to 8GB
lvresize -L 8G /dev/vg_data/lv_apps
```

## Complete LVM Workflow Example

```bash
# 1. Create partitions (optional)
fdisk /dev/sdb  # Create partition /dev/sdb1 with type 8e (Linux LVM)

# 2. Create physical volumes
pvcreate /dev/sdb1 /dev/sdc

# 3. Create a volume group and add physical volumes
vgcreate vg_data /dev/sdb1 /dev/sdc

# 4. Create logical volumes from the volume group
lvcreate -L 15G -n lv_home vg_data
lvcreate -l 100%FREE -n lv_backup vg_data  # Use all remaining space

# 5. Format the logical volumes
mkfs.ext4 /dev/vg_data/lv_home
mkfs.xfs /dev/vg_data/lv_backup

# 6. Mount the logical volumes
mkdir -p /home /backup
mount /dev/vg_data/lv_home /home
mount /dev/vg_data/lv_backup /backup

# 7. Add to /etc/fstab for persistent mounting
echo "/dev/vg_data/lv_home /home ext4 defaults 0 2" >> /etc/fstab
echo "/dev/vg_data/lv_backup /backup xfs defaults 0 2" >> /etc/fstab
