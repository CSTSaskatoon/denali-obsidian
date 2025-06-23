### GREP

Select then pipe to filter by grep's regex search.
```
ls -la | grep 4096
```

Find a file by name instead of searching by text.
Can still use grep.
```
ls -R / | grep .bashrc
```
 
-R is recursive
Many of them are errors, so redirect to /dev/null. This is know as the "Bit Bucket", it writes in into the ether. Reading from here will get nothing.
This output is much better, just shows result without all the errors.
```
ls -R / 2> /dev/null | grep .bashrc
```
### Find

Find looks for files in the file hierarchy.
Can search by name but there are many other searching's. `-name` or `--name` traditionally, but you do not need to with this.
```
find / -name .bashrc
```
## Root user

Start a terminal to be the super user or root. Root shell is discouraged since everything should be intentional.
### sudo

Switch user do, or super user do.
Run a single command as a super user.
Run as users other than root.

Not every user can use sudo, only users in the sudoer's list. The default in Ubuntu is on this list. Other users will have to be added manually.
## top

Linux equivalent to Windows Task manager.
Sorted by top usage (CPU by default).
## Disk usage with disk free

df
```
df -Th
```

tmpfs is RAM basically.
### flags
`-Th` to show mb instead of blocks.
`h`
`hcs` total space used
## Users

`sudo who` shows whos on the system logged in.
`sudo w` is short hand.
### Which

This command, it shows what location of what executable is being run.
```
which [executable]
```
Example: `which ls`
## Environment variable

`$PATH` to show which directory to check in when launching an executable in cmd. Windows does this but it will also check the local directory. `./foo` would be used in linux.
### Alias

`alias` shows current aliases.
Example: `ls --color=auto`. So `usr/bin/ls` will run without the color being used.

Adding. This makes `gohome` run that `cd ~` command:
```
alias gohome='cd ~'
```

Remove:
```
unalias gohone
```

This is useful for repetitive commands, or a script would be used.

Alias *does not* persist, will be gone when terminal is closed.
Can add an alias to starting script so it does persist.
## Network Commands

Looks for certain addresses and wait for responds.
`ping 8.8.8.8`

Show network information. This replaces `ipconfig`.
`ip addr`
### Cancel updates
```
sudo systemctl disable unattended-upgrades
```
## Installing packages

```
sudo apt install gcc vim
```
# VI Text Editor

---
```
vi textEdit.vi
```

Modal editor, changes how keys work.
Edit mode at start.

Command, press `:`
Insert, press `i` - Esc to go back to edit.
`a` - to append, like normal typing.
`o` - go to next line.
`O` - insert line above.
`w` - next work
`b` - beginning of current word
`e` - end of next work
`gg` - beginning of file
`G` - end of file
`#G` - to go to a number on line
`x` - delete character
`dd` - delete line
`gg#` - delete that many lines

Save. Cmd, write, quit.
`:wq`

Quit without save:
`:q!`
## VIM
[OpenVim - Interactive Vim tutorial](https://openvim.com/)

### Writing C with VIM

```
vi hello.c
```

```c
#inlcude <stdio.h>

int main()
{
	printf("Hello world.\n");
	return 0;
}
```

```bash
ls *.c
gcc -o hello hello.c
ls hello*
./hello
```
## Directory and file placement

Show files at root.
`ls -la /`
### Filesystem Hierarchy Standard

You can do whatever you want, but that there is a standard.
`/` is start.
`/bin` are binary executable files.
`/etc` has many system configuration files.
`/home` is a users directory and personal settings.
`/opt` is applications.
### User file management

State shows file information.
```
stat hello.c
```

File data is stored in iNode, and a file label points at an iNode. Renaming or moving a file changed label location, unless it is on a different disk.

Stat shows "links" and it's how many labels point to that iNode.
Add links with `ln`.
```
ln file link
```
```
ln text.txt linktext.txt
```

Removing any extra link will not delete the data.
After all the links are removed, then the data will be ready to be overwritten.

s is symbolic.
`ln -s`

This will make the link only work if the base link works. It's tied to location in hierarchy, so if that original link is created with other data, then the symbolic link to point to that new data. Basically a pointer to a pointer.
## Permissions

Change access modifier to nothing.
```
chmod 000 [file]
```

Read only
```
chmod 444 [file]
```

Read and write
```
chmod 644 [file]
```

Read write and execute per three dashed. Example with all `wrx`.
`- --- --- ---`

It is repeated three times.
File type, Owner, group and other.
`- --- --- ---`

File type is d, -, or l. Directory, file, or symbolic link.
File x, permission to run.
Directory x, permission to go into the file.

Group is initially created with same name as first user.

`Chmod` flags/numbers.
644 - `rw- r-- r--`
6 = 110
4 = 100

For `r-x rw- --x` = `chmod 561`
5 = 101
6 = 110
1 = 001

`chmod` can also use characters instead of numbers.
o is owner, g is group, a is everyone.
`cmod o+r [file]` -> Owner can read on that file.
`cmod a-x [file]` -> Everyone cannot execute that file.

sudo ignored permissions.

>Expect CHMOD on exams
