## Exercise 1
1. Create two new users in your LDAP directory:
	- If you haven't already created the `jetsons` group with `gid` `6200`, do so
	- Jane Jetson (`username`: `jane`, `uid`: `6012`, has the `jetsons` group as her primary group)
	- Elroy Jetson (`username`: `elroy`, `uid`: `6013`, has the `jetsons` group as his primary group)
2. `Jane` and `Elroy`'s home directories should be inside the same directory as `george`'s.
3. Test to make sure you can successfully log in to each of these users via `ssh` or `su`, that they have a proper home directory and shell and the like.

### Solution
```bash
cd ~/ldifs
cp george.ldif jane.ldif
cp george.ldif elroy.ldif

# could have done this as one ldif file apparently
vi jane.ldif
# Customize values to match the stuff given
vi elroy.ldif
# Customize values to match the stuff given

# add users to ldap
ldapadd -x -W -D "cn=admin,dc=fuckead,dc=io" -f jane.ldif -H ldap://server
ldapadd -x -W -D "cn=admin,dc=fuckead,dc=io" -f elroy.ldif -H ldap://server

# Make home directories
sudo cp /etc/skel /space/jane -R
sudo cp /etc/skel /space/elroy -R
sudo chown 6012:6101 /space/jane
sudo chown 6013:6101 /space/elroy

# Set their ldap passwords
ldappasswd -S -D "cn=admin,dc=fuckhead,dc=io" -W -x -H ldap://server "uid=jane,ou=users,dc=fuckhead,dc=io"
ldappasswd -S -D "cn=admin,dc=fuckhead,dc=io" -W -x -H ldap://server "uid=elroy,ou=users,dc=fuckhead,dc=io"

# Test it
su jane
```

## Exercise 2
- For this exercise, you will partner with a fellow student. You will perform some server setup on your server, and then you'll test out _their_ installation from your server.
- Remember, you'll both have to have each others' servers in your `/etc/hosts` file under the name you used to sign your server's certificate.
- Reference the PowerPoints for LDAP for guidance on these operations - this exercise does not necessarily lead you through detail by detail.

#### Server Setup:
1. Create a new LDAP database for your server - it is okay if you wipe out your old saskpolytech.edu database (you can always recreate it later if you want). The new database should be for the domain **`victorians.org`**.
2. You should **not** need to change any of your SSL certificates so long as your LDAP server retains the same domain name, regardless of the domain you're providing LDAP information for. When you purge the database though, it will reset your `cn=config` info though so you'll have to re-add the `olcTLSCACertificateFile`, `olcTLSCertificateKeyFile`, and `olcTLSCertificateFile` entries to it. If you don't still have the`ldifs` you used to add those in the first place, you might want to take note of the values you ended up with them before you purge the LDAP database!
3. Do whatever steps you need to do to prepare the **`DIT`** to add **users** and **groups**
4. Create the following users in your **LDAP DIT**, all with the password `password`
	- `wilde`, `uid` `6501`, `gid` `6550`, home directory `/victorians/wilde`, everything else default
	- `tennyson`, `uid` `6502`, `gid` `6550`, home directory `/victorians/alfred`, everything else default
	- `bronte`, `uid` `6503`, `gid` 6551, home directory `/victorians/emily`, everything else default
5. Create the following groups in your LDAP DIT:
	- `poets`, `gid` `6550`
	- `novelists`, `gid` `6551`
6. You will also set up NFS on your server to share out the home directories of your LDAP users. Create the a directory called `/srv/victorian-homes` directory, and appropriately create and `chown` the directories for `wilde`, `tennyson`, and `bronte` inside of it. It should be exported over NFS so that anyone on the `10.36.106` network can read and write to it.

#### Client Setup:
1. On your client, mount the `/srv/victorian-homes` directory from your partner's server to `/victorians` on your client.
2. Modify your client's LDAP setup to use your partner's server for LDAP. You may need to flush the cache or the like to get it to take - check the PowerPoints for troubleshooting hints.
3. Finally, verify it is all working by `ssh` into your client as the different LDAP users you should now be able to log in as.

## Solution
```bash

```