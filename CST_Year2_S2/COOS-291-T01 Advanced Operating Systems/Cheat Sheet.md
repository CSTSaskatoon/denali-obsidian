## Table Of Contents
- [My Computer Info](#My%20Computer%20Info)
- [Shortcuts](#Shortcuts)
- [Hyper-V Shortcuts](#Hyper-V%20Shortcuts)
- [Important Files](#Important%20Files)
- [Commands](#Commands)
	- [General Use](#General%20Use)
	- [Files](#Files)
	- [Text Manipulation](#Text%20Manipulation)
	- [Redirection](#Redirection)
	- [User/Group Administration](#User/Group%20Administration)
	- [File Management](#File%20Management)
	- [SSH](#SSH)
	- [NFS](#NFS)
	- [FTP](#FTP)
	- [Processes](#Processes)
	- [Web Servers](#Web%20Servers)
	- [LDAP](#LDAP)
	- [DNS](#DNS)
	- [SAMBA](#SAMBA)
	- [CIFS (Common Internet File System)](#CIFS%20(Common%20Internet%20File%20System))
- [Vim](#Vim)
	- [Global](#Global)
	- [Editing](#Editing)
	- [Navigation](#Navigation)

## My Computer Info
[Table Of Contents](#Table%20Of%20Contents)
Username - `student`
IPv4 Addresses - `10.36.106.106` & `10.36.106.200`
Netmask - `255.255.252.0`
Gateway - `10.36.104.1`
DNS - `142.99.32.197, 142.99.32.196`

## Shortcuts
[Table Of Contents](#Table%20Of%20Contents)
`CTRL + ALT + T` - Opens Terminal

## Hyper-V Shortcuts
[Table Of Contents](#Table%20Of%20Contents)
`CTRL + ALT + HOME` - Shows the "Connection bar" where you can manage the VM

---
## Important Files
- [Table Of Contents](#Table%20Of%20Contents)
- *`/etc/passwd`* - User information
- *`/etc/group`* - Secondary group information (doesn't list people who have the group as their secondary group)
- *`/etc/hosts`* - A list of hostnames to resolve without DNS
- *`/etc/resolv.conf`* (**DNS**)- connecting local clients to the internal DNS stub resolver of `systemd-resolved`, lists all the configured search domains
- *`/etc/nsswitch.conf`* (**NSS**) -  defines the "search order of network databases" (what order it will try to find information about hosts, users, groups and other services)
- *`/etc/apache2/ports.conf`* (**APACHE2**) - A list ports for apache2 to listen to and what module to use for the connection
- *`/etc/apache2/sites-available/*.conf`* (**APACHE2**) - files that specify an apache2 site configuration
- *`.htpasswd`* (**APACHE2**) a list of usernames/passwords that will allow you to authenticate for specific apache2sites, the location for this is set in it's corresponding `.htaccess` file
- *`.htaccess`* (**APACHE2**)- Allows you to override the config file of an apache2site. Have to enable the override functionality, they are all disabled by default. File location is whatever site path you want to override (Ex. `http://example.com/about` might have the `.htaccess` file in `/var/www/example.com/html/about/.htaccess`)
- *`/var/log/apache2/*.log`* (**APACHE2**) - log files for your apache2 server
- *`/etc/vsftpd.conf`* (**FTP**) - Configuration for setting up your machine as an ftp server
- *`.ldif`* (**LDAP**) - specifies a LDAP user/group that you can add/modify/remove from your server
- *`/etc/exports`* (**NFS**) - Configure what directories you are sharing out with NFS
- *`/etc/bind/named.conf`* (**DNS**) - Main DNS Config file
- *`/etc/bind/named.conf.default-zones`* (**DNS**) - Default zones config file
- *`/etc/bind/named.conf.local`* (**DNS**) - Local zones and settings config file
- *`/etc/bind/db.empty`* (**DNS**) - Example forward Lookup zone file
- *`/usr/share/dns/root.hints`* (**DNS**) - Root DNS Server hints

---
## Commands
[Table Of Contents](#Table%20Of%20Contents)
### General Use
- [Table Of Contents](#Table%20Of%20Contents)
- `shutdown -h now` - shuts down the machine immediately
- `man` - manual pager (help)
- `cd` - change directory
- `ls` - list directories
- `pwd` - present working directory
- `sudo apt install tree` - installs the tree app
- `ps` - list processes
- `df` - list storage
- `who` or `w` - List users
- `which` - put before command, tells you what executable is being run
- `local` - keyword to initialize a variable to a local function
- `type` - keyword to find where a command comes from
- `alias` - add or remove aliases, doesn't persist
- `sudo hostnamectl set-hostname $NEW_NAME` - change your computer hostname

### Files
- [Table Of Contents](#Table%20Of%20Contents)
- `touch fileName` - creates a file
- `rm fileName` - deletes a file
- `mkdir directoryName` - makes a directory
- `rmdir directoryName` - deletes a directory (can't do if it's not empty)
- `mv fileName directoryName` - Moves a file to location specified
- `cat fileName` - technically concatenate, can use multiple files
- `more fileName` - open a file that you can page
- `less fileName` - basically better `more`, you can scroll
- `clear` - clears the terminal
- `echo` - prints something out
- `head` - lists the top few lines of a file
- `tail` - lists the bottom few lines of a file
- `wc` - get the word count of a file
- `cut` - cutting out sections from each line of files
- `ln` - add a link to a file

### Text Manipulation
- [Table Of Contents](#Table%20Of%20Contents)
- `awk` - text manipulation program, Ex. `ls -la | awk '{print toupper($0)}` prints every just the items in the first column from `ls -la`, and converts them all to uppercase
- `grep` - search a file for a string of text, returns all rows where the text occurs to `stdout`

### Redirection
- [Table Of Contents](#Table%20Of%20Contents)
- `>` - redirect **`stdout`** to a file, Ex. `echo "Some text" > something.txt`
- `<` - redirects **`stdin`**, Ex. `command < somefile.txt` would pass the contents of `somefile.txt` instead of the file itself.
- `>>` - redirects **`stdout`** to a file, **appending** it
- `&>` - redirects all output (`stdout` and `stderr`) to a file
- Can specify to redirect just `stdin`, `stdout` and `stderr` with `0>`, `1>` and `2>`
	- Can redirect errors to `/dev/null` with `command 2> /dev/null`, basically saying **don't show me the errors**
- `echo "this is an error message" >&2` - **writing an error out out to `stderr`**,  `&` specifies that what comes next is a file descriptor (only for right side of the `>`), `2` is the `stderr` descriptor number

### User/Group Administration
- [Table Of Contents](#Table%20Of%20Contents)
- `adduser` - Interactive version of `useradd`, has defaults
- `usermod` - allows you to manage a user
- `pwck` - password check

### File Management
- [Table Of Contents](#Table%20Of%20Contents)
- `mkfs` - make file systems on drive partitions
- `fdisk` - format/partition drives
- `blkid` - tells you the UUID of a drive
- `vgcreate` - create a new volume group
- `lvcreate` - create a new logical volume (need a volume group first)
- `vgs` - display information about your volume groups
- `lvs` - display information about your logical volumes
- Also `vgextend`, `vgreduce`, `lvcreate`, `lvremove`, `lvresize`
- Line to add a logical volume fs to **`fstab`** - `/dev/<LG_NAME>/<LV_NAME> /<MOUNT_LOCATION> xfs defaults 0 2`
- Line to add a partition fs to **`fstab`** - `/dev/disk/by-uuid/<ID_HERE>/<MOUNT_LOCATION> ext4 default 0 2`

### NFS
- [Table Of Contents](#Table%20Of%20Contents)
- `/etc/exports` - List of NFS Exports
- `/srv/sharing *(ro,sync,no_subtree_check,root_squash) brody(rw,sync,no_subtree_check,root_squash)` - Example `/etc/exports` line
- `sudo mount -t nfs karbn:/home/student/nfs-exercise /home/student/mountpoint` - mount `/home/student/nfs-exercise` on the server to `/home/student/mountpoint` on the client
- `sudo exportfs` - list the directories you are sharing with NFS
- `sudo exportfs -r` - reload your exports

### FTP
- [Table Of Contents](#Table%20Of%20Contents)
- Install with `sudo apt-get install vsftpd`
- Settings are in `/etc/vsftpd.conf`

### SSH
- [Table Of Contents](#Table%20Of%20Contents)
- `scp` - lets you copy files over SSH
- `ssh` - start an SSH session

### Processes
- [Table Of Contents](#Table%20Of%20Contents)
- `ps -ely` - List all system processes
- `top` - basically running `ps` every few seconds and organizing them
- use `&` to background a process
- `jobs` - get a list of processes that are running in a shell (often in the background)
- `fg $JOB_NUMBER` - 'foreground' the process (gain control over it)
- `kill` - kill a program, can be trapped, default is `15`
- `kill -L` - list a table of kill options
- `nice` - set the scheduling priority of a program
- `pkill`/`pgrep` - kill/search in process table based on a pattern instead of using PID, can delete multiple

### Web Servers
- [Table Of Contents](#Table%20Of%20Contents)
- `/etc/apache2` - All Config files
- `apachectl` - administrate the Apache Daemon
- `http://localhost/manual` - Apache documentation
- `apachectl configtest` - will tell you if there are any problems with your config files
- `apachectl -S` - Check what you are currently hosting
- `sudo a2ensite <site-name>` and `a2dissite <site-name>` - enable/disable sites
- `sudo a2enmod <module-name>` - enable mod

### LDAP
- [Table Of Contents](#Table%20Of%20Contents)
- `sudo dpkg-reconfigure slapd` - configure OpenLDAP setup (To create a new database)
- `sudo systemctl status slapd` - check the stand alone LDAP daemon status
- `ldapwhoami -x -H ldap:///` - should return anonymous
- `ldapadd -x -W -f template.ldif -D "cn=admin,dc=fuckhead,dc=io"` - Try to add a user to the LDAP server, `-W` makes it prompt for password
- `ldapdelete -x -W -D "cn=admin,dc=fuckhead,dc=io" -H ldap://server "uid=george,ou=users,dc=fuckhead,dc=io"`
- `ldappasswd -x -S -W -D "cn=admin,dc=fuckhead,dc=io" "cn=george,ou=users,dc=fuckhead,dc=io` - `-S` prompts for the user's new password
- `ldapsearch -x -H ldap://karbnldap.server -b "dc=fuckhead,dc=io"`

### DNS
- **On Server**
- [Table Of Contents](#Table%20Of%20Contents)
- Install `bind9` - `sudo apt install bind9 bind9utils bind9-doc dnsutils`
- Change hostname for `.local` - `sudo hostnamectl set-hostname <name>.local`
- Domain Information Groper - `dig <name>` or `dig -x <ip address>`
- Name Server Lookup - `nslookup <name>`
- Main config file is `/etc/bind/named.conf`
- Default zones config file - `/etc/bind/named.conf.default-zones`
- Local zones and settings config file - `/etc/bind/named.conf.local`
- Root DNS hints are in `/usr/share/dns/root.hints`
- Copy `db.empty` to `/etc/bind/zones/` - `cp /etc/bind/db.empty /etc/bind/zones/db.karbn.de`

### SAMBA
- **On Server**
- [Table Of Contents](#Table%20Of%20Contents)
- `/etc/samba/smb.conf` - Main SAMBA config file
- `testparm` - Test your SAMBA Config
- `smb`/`smbd` - SAMBA Daemon, file sharing and print services
- `nmb`/`nmvd` - NetBIOS Name with browsing Daemon (Allow server to be found from Windows machines)
- `/var/lib/samba/printers` - Printer drivers
- `sudo smbpasswd -a karbn` - Add a user as an SMB user and set their SMB password (Can be different than user password)
- **On Windows Machine** - `net use R: \\10.36.106.200\stuff /USER:karbn` - Mount the SAMBA share to the `R:` drive on your windows machine as the user specified (prompts for password)

### CIFS (Common Internet File System)
- **On Client**
- [Table Of Contents](#Table%20Of%20Contents)
- `sudo apt-get install cifs-utils`
- `sudo mount.cifs //10.34.56.224/VM-2$ /vmach -o user=therrien1784` - Mount a Windows SMB Share to `/vmach` using the credentials of `therrien1784`, will prompt for password

---
## Vim
- [Table Of Contents](#Table%20Of%20Contents)
### Global
- [Table Of Contents](#Table%20Of%20Contents)
- `:h keyword` - help for keyword 

### Editing
- [Table Of Contents](#Table%20Of%20Contents)
- `i` - insert mode
- `a` - append (insert mode)
- `r` - replace a single character
- `u` - undo
- `x` - delete (cut) any character
- `p` - paste clipboard
- `yy` - copy a line
- `yiw` - copy word under cursor

### Navigation
- [Table Of Contents](#Table%20Of%20Contents)
- `esc` - command mode
- `h` - left
- `j` - move cursor down
- `k` - move cursor up
- `l` - move cursor right
- `H` - move to top of screen
- `M` - move to middle of screen
- `L` - move to bottom of screen
