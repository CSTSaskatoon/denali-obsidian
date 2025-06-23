## System Administration
**Related Fields**
- Database administrator
- Network administrator
- Security administrator
- Web administrator
- Computer operator

### User Administration
Two ways of identification - `username` and `userid` (`uid`)
The **`root`** user (`uid` of 0) is omnipotent and can do anything
Special users are usually created for specific tasks/running certain services
- most distros will reserve certain ids for this (500 - 1000)

Regular users don't have any specific permissions

#### Managing Users
User accounts are stored in `/etc/passwd`
- format is `username:password:uid:gid:comment:home directory:shell`
- Comment can be modified with `chfn`
- Important commands - `su`, `useradd`, `adduser` (interactive), `userdel`, `userdel -r`, `usermod`, `id`, `pwck`
- Default home directory is `/home/[username]`, copy contents from `/etc/skel`

**Groups**
- basically just have a name and a group id (gid)
- Users have a primary group and other supplementary groups
- Important commands - `groups`

### Important files
`/ect/passwd` - contains information about users, used to include password
`/etc/shadow` - only accessible to root or `shadow` group, contains password information (hashed)
`etc/group` - contains information about all groups and users who have said groups as their secondary group (Won't list users who have it as their primary group)
`/etc/adduser.conf` - default configuration for new users

## Linux Run levels
- **deprecated, Ubuntu doesn't really use them**
- use `runlevel` to find what the level was previously and what it is currently (`N` means there was no run level previously)
- use `sudo init $LEVEL` to change what level you are on
- 0 - system halt - turn it off
- 1 - Single user mode
- 2 - Multiple user mode with no NFS (network file system)
- 3 - Multiple user mode under CLI and not GUI
- 4 - user-definable
- 5 - Multiple user mode with GUI, standard run level for most linux systems
- 6 - Reboot

### `systemd` and `systemctl`
- Roughly maps to runlevels
- `systemctl get-default` can be used to get the current default
- `systemctl set-default` lets you set a different default

### Single User Mode
- skips a bunch of launch stuff like verifying the filesystem and launching services
- Useful if the machine won't boot normally or if you forget the root password
- Can set a password in BIOS or other things to prevent attacks using this
- Users that allow other users to login aren't started
- open GRUB by pressing `esc`, press `e` and change `ro` to `rw init=/bin/bash`
- From here you can check the file system consistency with `fsck`, change the root password with `passwd` and `touch ./autorelabel`
