Network and User Configuration Files
	Linux store configuration information within files stored in /etc
	/etc/hostname - Hostname information
	/etc/hosts - Host IP Configuration
	/etc/network/interfaces - Network Configuration Information
	*(THESE SETTINGS VARY BASED ON LINUX VARIATION)*
	/etc/passwd - Stores User Information
	/etc/group - Stores group Information
	/etc/shadow - stores password information, encrypted

TCP/IP Configuration
	ifconfig - deprecated
	ip addr - equivalent replacement
	should be 2 interfaces
		lo - local loopback for testing
		eth0 - wired NIC
			ens33 used as virtual adapter in VMWare

Linux Users
	3 Types
	Standard User
		Can only create modify and delete content within their home folder *(/home/<username>)*
	Administrator User - 1st User is almost always Admin
		Can create, modify, and delete content within their home folder and elsewhere
		Can perform Admin functions including creating user accounts
		With Debian distros all Administrative functions must be run as sudoer
			First User will have default access to sudo
			Other users can be given access by adding to sudo group (wheel in some distributions) or editing /etc/sudoer
			Complicates Administration
				All graphical admin tools will prompt for password like windows
				When typing commands in terminal that require admin access must preface command with sudo command
				You will be prompted to enter a password
	root
		Has admin access to all commands and files (We almost never use root users because they have too much power)
		Also referred to as root account, root user, or superuser
		In Debian distros root has no password by default, Linux users with no password cannot be used to logon.

Sudo
	command line utility that allows trusted users to run commands as another user, root by default
	2 ways to grant sudo privileges
		Add to the sudoers file

UIDs, GIDs
	In windows SIDs are used to uniquely identify security principles like users, groups, and computers
	Linux uses UIDs and GIDs

Groups
	Organizational units to organize admin and user accounts
	Primary purpose is to define permissions
	Two types of groups
		Primary - When a user creates a file, the file's group is set to the user's primary group. Usually the name of the group is the same as the user.

/etc/group
	all group info stored here
	One entry per line with 4 fields per line entry seperated by colon (:)
	Each row represents one group
	To see default groups and their settings, command is cat /etc/group
		Sample entry *(instructors:x:1000:bryce, donovan, michael, rick)*
		Order goes: GroupName:GroupPassword:Size:Users

Creating a group
	Type groupadd followed by group name
	command adds an entry for the new group to your /etc/group and /etc/gshadow files

/etc/passwd
	All user login data stored here
	Simple text file
	File is readable by all but only modifyable from root
	Each line of the file contains seven comma-seperated fields
	Username - max 32 characters
	Password - passord in passwd file is just "x", and stored in the shadow file
	UID - User Identifier uniquely assigned to each user
	GID - User's group Identifier, referring to user's primary group

Create Users in Terminal
	useradd
	Sample Syntax
		useradd rick -u 1234 -g rick -G sudo -m -s /bin/bash
			Username - rick
			UID - 1234
			Primary Group of rick (can be left out)
			-G assigns a secondary group of sudo
			-m sets home directory with username under /home
			-s sets shell to /bin/bash

Setting Passwords
	User requires 3 things to sign in
		A shell
		A home directory
		A Password
	Passwords are stored in /etc/shadow

/etc/shadow
	Stores user's password in encrypted form
	Only readable by root user
	contains user auth info 

Deleting a user
	userdel
	Invoke command and pass in username
		userdel username

Managing Groups
	to add a user to a secondary group use usermod -aG followed by name of group and user

Deleting a group
	use groupdel followed by group name
	groupdel groupname
	this removes the group from /etc/group and /etc/gshadow files

File Permission
	Linux Divides resource access to 2 levels - Ownership and permission
	These concepts are crucial

