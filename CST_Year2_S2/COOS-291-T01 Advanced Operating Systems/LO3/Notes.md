## Disk and file system Administration
- use `fdisk` to mange disk partitions
- use `lshow -C disk` to just show the physical hardware
- `g` option can be used to use the GPT partition table
- use various `mkfs` programs (Ex. `mkfs.ext4`) to format the partition
- Mount a drive with `mount $DRIVE $LOCATION` - Ex. `mount /dev/sdb1 /userdata`
- `du` and `df` can be used to check disk usage and information

### `/ect/fstab`
- Specifies partitions that are mounted on startup
- Each line is a partition
- UUID can be found with `blkid`

**Options**
- `auto`/`noauto` - whether it should be loaded on boot
- `exec`/`noexec` - whether you can execute files on it
- `ro`/`rw` - read only/read write
- `sync`/`async` - system can decide when to perform writes
- `nouser`/`user` - user has mounting and unmounting privileges

Can manually mount all drives in `fstab` with `mount -a` (This also happens every time you boot)
