## Scripts

#### Making a simple script
```bash
echo "echo hellow world" > hellowworld.bash
```

source takes the commands and runs them for you. `.` is the short cut.
Bash does the same thing
```bash
source helloworld.bash
```
```bash
. helloworld.bash
bash helloworld
```

Execute permission with this file.
```bash
chmod u+x helloworld.bash
./hellowworld.bash
```
#### Making multiple files

Brace expansion.
```bash
touch file{a,b,c}
ls -la file*
touch file{1..5}
ls file*
cp file1{,.old}
ls file*
touch file{1{a,b,c},2{e,f,g}}
```
#### Running commands from shell

Running an executable which still having access to bash. Background a process. Program will still shutdown when terminal closes.
Output may be put into shell.
```bash
[program] &
```
### Running commands back to back - checking while chaining

Simple way to chain commands with optional checking.

`;` semicolon is like using a new line. Lets your one line a bunch of commands.
```bash
mkdir test; touch test/foll
```

Checking if a command succeeds - run this, if it does succeed then run that.
```bash
[command] && [follow up command]
```

Running if failed - run this, if it does not succeed then run that.
```bash
[command] || [back up command]
```

Can run `true` and `false` command in the shell for simple Boolean returns. Each command has an exit status.
`$` is variables, `$?` checks the exit status code.
>0 is success, 1 (or any other) is error

`man errorno` shows the norm.
### Script that already exist

`.bash_logout` can be opened in vi.
`bash_rc` This is run when a shell is launched.
### Bash Shell

Based of SH (born shell). Born again shell. This is program and can be opened within bash.
### VI

#! is called a shabang. `/bin/bash` is what interpreter/shell to use. This is a comment.
```bash
#!/bin/bash
```
### If statements

Like most statements in Linux, it ends with the starting word backwards.

if:
```bash
if cd test; then echo "I changed into test";fi
```

else:
```bash
if cd test; then echo "I changed into test";else echo "I wasn't able to change into test";fi
```
#### Multiline command

The if can take a command, so it just runs it and checks the exit status.
```bash
#!/bin/bash
# A script to touch the file bar instide of the directory foo

if touch foo/bar
then
	ehco "Successfully touched foo/bar"
else
	mkdir foo
	touch foo/bar
	echo "Had to make foo first. Then touched bar."
if
```

`test` commands and variables.
### Variables

Variables stores everything in text, so there are no types. They are also tied just to the current shell it was made, so if they are named the same it will go with the "closest" one in scope.

Set variable.
```bash
MYVAR="Stuff"
```

Get variable value:
```bash
$MYVAR
```

This will not work - it will think it is running a command:
```bash
MYVAR = "Stuff"
```
#### Export

Bring variable to subshell. It will be *copied* to the subshell, but it can NOT be passed back up.
```bash
MYVAR=57
export MYVAR
bash $MYVAR
MYVAR=90
echo MYVAR
exit
echo MYVAR
```
