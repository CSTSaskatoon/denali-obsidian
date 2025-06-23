### Local and type

Local "keyword" command is used in functions. This is to match expression to a local scope.

```bash
type local # Shows info on commands on built-in commands
help local # Shows info similar to man
```

### IP

`eth0` is your IP address.

```bash
ip addr # Shows IP
```

#### /ect/hosts

This is DNS, domain name resolution.

```bash
cat /etc/hosts
```

Adding to this list:

```bash
vi /etc/hosts
10.36.106.116    brody
```
## SSH Server

Saved host are stored in `~/.ssh`. This just connects you to a bash shell (or default set).

```bash
sudo apt install openssh-server
ssh student@localhost
```

### Moving files between local and SSH

The destination is the address so could be to remote (name@localhost) or to local machine.

```bash
scp [file] [detination]:[new file name] # Works like the copy command
```

### Remote execution

```bash
ssh student@localhost ls -a
echo $SSH_CONNECTION # Checks who you are remoted into, will be empty if local
# Your address and port then their address and port
```

### Generate public private key

This is saved as `id_rsa`.

```bash
ssh-keygen -t rsa
# Saved in ~/.ssh be default
ssh-copy-id student@localhost # Move key to ssh
````
