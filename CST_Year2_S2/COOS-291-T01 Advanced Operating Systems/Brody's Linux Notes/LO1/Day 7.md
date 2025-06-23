I missed last class.

[Bash Globbing](https://linuxhint.com/bash_globbing_tutorial/) is using wildcards for finding file names, or inside files.

`sed` is a stream editor for transforming text. It is a single pass, so you can continue piping it.
`-s` is search and replace based on regex. `'s/regex/replacement/'`

```bash
ls -la | sed 's/.bash/.sh'
ps aux | sed 's/^root/admin/'
ps aux | awk '/^student/ {print $11 " (" $2 ")"}' | sed 's/.*/\///'
```

## Script Student Practice - Backup Script

Write a script called `backup.bash` which does the following things:

1. Checks to see if the directory BACKUPS exists in the current directory.
    - If it does not, check to see if there is a non-directory file called BACKUPS in the current directory
        - If there is, exit with an error message saying the BACKUPS directory could not be created
        - If there is nothing called BACKUPS, make a BACKUPS directory
2. Go through every file in the current directory, and
    - If the file doesn't exist in the BACKUPS directory, copy it to the BACKUPS directory
    - If the file does exist in the BACKUPS directory but the copy in the current directory is newer, copy the one in the current directory overtop of the BACKUPS directory
    - If the file cannot be copied for any reason, print an error message
    - Keep track of how many files were successfully copied
    - Keep track of how many files weren't able to be copied because the copy command failed
3. At the end, print out a message saying the backup is done and reporting how many files were copied, and how many file could not be copied.

Once you've got the basics done, add some more user-friendly features:

- Ensure the script exits with an appropriate error code - a code of 0 if everything was backed up successfully, a code of 1 if errors were encountered and the script couldn't back up everything, or an error code of 2 if the user supplied invalid input
- Allow the user to supply a -e switch to ignore empty files when doing the backup.
- Allow the user to supply a -d \<directory name> switch to specify a different directory to use other than BACKUPS

```bash
if [[ ! -d]]
```