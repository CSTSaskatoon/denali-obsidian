>Jason is teaching

Content:
[[#What is a system administrator]]
[[#User Administration and Groups]]
[[#Linux Run Levels]]
[[#GRUB - Single User Mode]]

---
## What is a system administrator

They are responsible for upkeep, configuration, reliable, and security operation of computer systems.

### Related Fields

Database Administration (not in this class).

**Network Administration**
Wade will cover this when he returns.

**Security**
We will look into this and touch on the firewall.

**Web Server with Apache**
Topic on this will covered later in-depth. FTP and DNS will be covered.

**Computer Operator/Expert User or Administrator of a single system**
RAID operation will be mentioned.
## User Administration and Groups

---

**Two ways to identify users**:

- `username` This is the friendly "display" name
- `userid (uid)` This is what mattered to the system/administrator as it is just a number

**Types of users**:

- `root` user has `userid 0` - This is what `sudo` gives you access to
- *Special user* is like the system account on windows, it is for certain services
	- Distros will use `userid`'s below 500 or 1000 for these
- *Regular users* do not have special permissions, but can be set up in many ways

### Managing Users

Users are stored in a series of files. Three things that have to be managed are *user, password, and permissions*.

### Password

Stored on `/etc/passwd` formatted in the following, they are encrypted but readable by everyone:

```
username:password:uid:gid:comment:home directory:shell
```

Passwords just have an `x` now, as having it there was legacy. They are stored in `/etc/shadow` since it is denied who can look at this file. When reading it, `*` shows if no password and other passwords are stored encrypted. This is stored in the following:

```
usernameLpassword:lastchanged:minimum:maximum:warn:inactive:expire
```

The shell for service accounts are `/usr/sbin/nologin` since they have access but cannot be logged into.

Comment can be modified with `chnf` (change full name) to fill in comma separated user information sometimes called "`gecos`" (refers to the general electric comprehensive operating system which used the format).

| CMD      | Name     |
| -------- | -------- |
| `passwd` | Password |
The man `passwd` says `PASSWD(1)`, meaning it is that section of information based on what you are looking up. Another example is `man 7 man` will look at the 7th section of man.

### Important Commands

| CMD         | Name                   | Info                                                                                                                    |
| ----------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `su`        | Switch User            |                                                                                                                         |
| `id`        | Show current user      | Shows `uid`, `gid`, `sudo` group and many other groups                                                                  |
| `id <name>` | Find user              | This looks for a user such as `root`.                                                                                   |
| `useradd`   | Add user               | This is low level, older one for Debian                                                                                 |
| `adduser`   | Add user (interactive) | This adds users with CMD and the skel files. We will use this in class                                                  |
| `userdel`   | Delete user            |                                                                                                                         |
| `deluser`   |                        | This has config file for defaults                                                                                       |
| `usermod`   | Modify user            | Can use `-g` to change primary group. Home directory will be owned by new group. `-aG` is adding to supplementary group |
|             |                        |                                                                                                                         |
### The Skeleton Directory

`/etc/skel` is a configuration file/template thing that all users will pull from.

#### Creating User Example

Inside `/etc/skel`. Must use Sudo to add users. By default behavior, it will make a group of the same name.

```bash
sudo adduser mybuddy
New Password: admin
```

Can find this user in `/home`.

Switch to this new user with `su`.

```bash
su mybuddy
admin
```

This will only change the user within the terminal.

### Groups

Each group is associated with a group id `gid`.

Users have a primary group and then can belong to "supplementary" groups.

```bash
/ect/groups # Shows all the groups
groups # Shows current group or other group typed in param
```

Groups will show users that are in it. ??? This may show only primary or only supplementary.

| CMD        | Name             | Info                                |
| ---------- | ---------------- | ----------------------------------- |
| `groups`   |                  |                                     |
| `groupadd` |                  |                                     |
| `addgroup` |                  | Wraps `groupadd` friendlier command |
| `groupdel` |                  |                                     |
| `chfn`     | Change full name |                                     |
|            |                  |                                     |
|            |                  |                                     |
#### Create group example

```bash
sudo addgroup --gid 2600 myfriends
admin
cat /etc/group
```

Move `mybuddy` primary users tp `myfriends`.

```bash
sudo usermod mybuddy -g myfriends
sudo ls -la mybuddy
```

#### Removing User

```bash
sudo deluser mybuddy
sudo delgroup mybuddy
```

It will warn that group they belong to is empty and that it will not remove that group. Case in which default group that matches name, it would be deleted too.

After the user is deleted, their old user id will still remain on system files like ownership. If a user is created and takes that user id, it will *inherit* all that the user id was associated with.

#### Adding back a user with the same user id

```bash
sudo adduser anotherfriend --ingroup myfriends
```

Since the recently deleted user had the most recent id, then it inherited `mybuddy`'s stuff.

Trying to delete the `myfriends` group will with warn that a user has that group as their primary group.

There is three ways to change passwords, `usermod`, `passwd` and `chage`. `usermod` can do everything.
#### Commands

Graveyard is where to place empty home directories.

```bash
chown graveyard:graveyard ... || 
userdel ...
```
## Linux Run Levels

---

These are used in some distros. Ubuntu considers them deprecated for start ups. These are groups of services the system will run or stop depending on if it is `halt` or `reboot`.

Run levels 0-6, 0 is turn of system, 6 is restart. In-between they are levels of abilities, so 1 is like a rescue mode, 2 has multiple users in cmd mode only and no NFS, 3 can use NFS but no GUI. 5 has a GUI working and this would be the default boot.

```bash
runlevel
```

N means no run level, and 5 is the default.
This used to be used by `SysV init`. Ubuntu uses `systemd`. SystemD uses targets and uses levels in parallel.

Level 3 should be no GUI, can go into levels with:

```
sudo init 3
```

Turns out, our VMs do not change, at least the GUI is still present. Level 1 will have an affect.
In the VM, it disconnects and Hyper-V has trouble reconnecting.

### Systemctl and Systemd

```bash
sudo systemclt set-default multi-user.target
```

### Wall

This will display a message from root to all users. Useful for when a system is shutting down.

```bash
sudo wall "Going down soon"
```

### GRUB - Single User Mode

Restart machine and hit escape key to enter what is like the BIOS. Can change the root password here. Hard to get into in the VM.

### File system table

```bash
cat /etc/fstab
```

This shows partitions with a label at a location.

```bash
/dev/disk/by-uuid/934y9-02374-90324 /userdata 
```
