[[Commands]]

---
Terminal is using Bash.

### Basic commands and concepts

Man is manual pager, the help system. This is the textbook and can be used in exams.
```
man man
```
### Navigation with ls

`dir`  works but should use `ls`.

`Username@computer:location$` - Displays who is viewing and important for permissions.

cd can get you around, `~` is the root, aka `/`.
Can view the root files with (list (long, all) root location):
```
ls -la /
```

Permissions, ownership, group, size (blocks), date, location.

Print working directory. This will should your current location.
```
pwd
```
>Important: There is no drive letters.

Linus uses forward slashed (`/`). If a path starts with a slash, then it is an absolute path. If it does not, then it is a relative path.
## Creating and Removing Files

```
touch myfile
```

This can create files. It will also update time stamps.

Remove:
```
rm myfile
```

Make directory
```
mkdir mydir
```

Remove directory:
```
rmdir mydir
```

Move file:
```
mv [source] [target directory]
```

Renaming file:
```
mv [source] [new name]
```
## Printing

Cat - Catatename
```
cat [directory]
```

More - Press space bar to view pages at a time
```
more [directory]
```

Less - Press arrow keys to view pages like a scroll wheel
```
less [directory]
```

Clear command to clear screen.

Echo - Just prints to the terminal. This can be used for redirection.
```
echo Hello there
```

Redirection - basically just saves output to a file:
```
echo hello there > hi.txt
```

Redirection errors - This produces an error (404) but will not saved that error message.
```
ls . /foo > myls.txt
```

Save error messages (Explanation below):
```
ls . /foo > myls.txt 2> errors.txt
```
#### Input and outputs

Save error messages:
```
ls . /foo > myls.txt 2> errors.txt
```

Standard in, out, error:
stdin 0, stdout 1, stdere 2 in terminal.

The 2 indicates you are writing to standard 2 errors. ls assumes you are always going to standard 1, so redirect tells ls to move it's output to standard 2.

You can redirect to standard 1 that will concatenate (globerate) at the front.

Concatenate at the end:
```
ls . /foo >> myls.txt
```

To automatically 
```
ls . /foo &> myls.txt
```
### Global Regular Expression Print (grep) - search

[Grep](https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix), short for “global regular expression print”, is a command used for searching and matching text patterns in files contained in the regular expressions. Furthermore, the command comes pre-installed in every Linux distribution. In this guide, we will look at the most common grep command usages, along with popular use cases.
```
grep txt < myls.txt
```

Marker - continuous writing:
```
grep txt <<MARKER
Some text
that can be multiple lines
this will be passed as input for the grep command
and is basically a file
end this command and save with
MARKER
```
## Piping commands

Take output, pipe that into grep, then it will show all the lines of files that contain txt.
```
ls -la | grep txt
```
## Flags
### ls flags
`-l` long form
`-a` all files (hidden files start with a `.`, example `.lesshst`) (no file extensions)
`-la` combines these, the order does not matter it is handled by the creator
### rm
`-d` Remove directory not files. This can be used instead of `rmdir`.
`-r` Recursively remove all files and directories
#### Command history

Arrow key to look back.
ctrl + r to view
ctrl + p
alt + . will display last text
!! will run the last command
history will show list of all commands

Run command in history:
!\[line in history] so like !41.
!\[ech] is like a tab complete to run the most recent command that looks like it.

`^Hello^Hi` does some shit idk.
