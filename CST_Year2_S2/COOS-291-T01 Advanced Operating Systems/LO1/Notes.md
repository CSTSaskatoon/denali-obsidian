## Commands
`man man` - manual pager (help system)
Files that start with a `.` are hidden by default
`history` - lists all the commands you have used
- can use `!41` to run command 41 in your history

## reading `ls -la`
Ex. `drwxr-r-x--- 18 student student 4096 Jan 8 10:40`
- `d` means directory
- `18` is the SIM number?
- `rwxr-r-x---` specifies permissions
- 1st `student` - who owns the file/directory
- 2nd `student` - group that owns the file/directory (often same as the user)
- `4096` - File/directory length (size)
- `Jan 8 10:42` - Date and time accessed

`echo Hello There! > hi.txt` - redirects into the `hi.txt` file instead of the terminal
`ls . /foo > myls.txt 2>errors.txt` - `2>` specifies we are redirecting `stderr`, by default we are redirecting `stdout`
- `&>` is shorthand for outputting `stderr` and `stdout` to the same file
- `>>` appends the info instead of deleting it

`grep txt < myls.txt`
`grep txt <<MARKER`

## Piping
`ls -la | grep txt`

## Brace Expansion
`touch file{a,b,c}` - essentially doing `touch filea fileb filec`
`touch file{1..5}`
`cp file1{,.old}` - copies `file1` into `file1.old`

## Error Codes
`echo $?` - returns the last command's exit code

## sed
Stream editor, lets you sort, filter, find and replace, etc.
Ex. `ls -la | 's/.bash/.sh/'` - Replace all `.bash` with `.sh`
