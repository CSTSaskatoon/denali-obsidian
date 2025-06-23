`sudo apt install openssh-server` - installs the `ssh` server onto your machine

## Generate a public/private key pair for SSH
`ssh-keygen -t rsa`
`ssh-copy-id student@localhost` - copy the public 
`echo $SSH_CONNECTION` - see if you have an active SSH session

## Processes

## NFS
Install NFS and Tools - `sudo apt install nfs-common nfs-kernel-server net-tools`
Show mount information of an NFS server - `showmount`
- Ex. `showmount -e 10.36.106.11`

mount `/sharedfiles/` from `10.36.106.11` to `~/wadesharedfiles/` - `sudo mount -t nfs 10.36.106.11:/sharedfiles ~/wadesharedfiles/`
- can also do `sudo mount -t nfs office:/sharedfiles ~/wadesharedfiles/` if you add `office` to the `/etc/hosts` file

`/etc/exports` contains a list of files/directories that are exported via NFS
- Ex. `/srv/sharing	*(ro,sync,no_subtree_check,root_squash) brody(rw,sync,no_subtree_check,root_squash)`
- `*` means anybody
- `ro` is read only
- `sync` syncs files
- `root_squash` means it doesn't matter if they `sudo`

### Start the Server
Stop your NFS server - `sudo systemctl stop nfs-server`
Start your NFS server - `sudo systemctl start nfs-server`
Restart your NFS server - `sudo systemctl restart nfs-server`
Check your NFS server status - `sudo systemctl status nfs-server`
Show all your NFS mounts - `showmount -e`
Show all your NFS exports - `sudo exportfs`
Reload your NFS exports - `sudo exportfs -r`

## Resize your drive
- **Turn off** your VM
- Disable and delete any Checkpoints on the VM
- In your VM Settings, click on the OS disk
- Select **Edit**
- Select **Expand**
- Enter the **size** of your new disk
- **Start up** your VM

Delete the partition and make the new one
```bash
sudo fdisk /dev/sda # will get a warning you are editing a disk with the file system, it's fine
d
1
n
1
# Default (use all space)
n # If you pick yes it will bork your VM
p # make sure it says the new drive space
w # write the changes if it's good

sudo touch /forcefsck # force the filesystem check on startup

# Restart your machine
# Extend your fs
sudo resize2fs /dev/sda1
```

## File Transfer Protocol (FTP)
- Insecure (transfers in plaintext)

Connect via ftp - `ftp 10.36.106.100`
- Username is `ftpguy`
- Password is `password`
- can also do `ftp ftpguy@wade`

### Using the Interface
- Help menu - `?`
- Open a new Shell to run commands (Closes after the command is done) - `!` - Ex. `!cat test.txt`
- Change directories - `lcd`
- Get file - `get $file`
- Get multiple files - `mget $pattern # Ex. mget *`
- Upload a file - `put $file $file` basically works like `cp`

### User list
- setting in `vsftpd.conf`
- enable it with `userlist_enable=YES`
- set it to blacklist mode - `userlist_deny=YES`
- Set it to whitelist mode - `userlist_deny=NO`
- Specify list location (`/etc/vsftpd.denied_user_list` for me) - `userlist_file=/etc/vsftpd.denied_user_list`

### `chroot`
![](Pasted%20image%2020250227103448.png)

### `sftp` (using `ssl`)
Generate key - `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/myftpserver.key -out /etc/ssl/certs/myftpserver.crt`
- cert information isn't required

### Firewall
Enable firewall - `sudo ufw enable`
Status - `sudo ufw status`
Allow a port - `sudo ufw allow 20:22/tcp`