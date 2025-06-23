Variables

```bash
MYVAR="This is a variable"
echo $MYVAR # This is a comment, this echo to to print the variable
echo $PATH
echo $HOME
echo $PS1 # Variables are scoped and would need to be exported to see in children

# Bash has arrays
my_array[2]=5
echo $my_array[2] # This will only bring [2]
echo ${my_array[2]} # This is how to pull the value out. Need to use {} like you would () in Java
echo Somelongstringof${MYVAR}text # Bash uses spaces as breaks, so using {} will manually add the break

# You can referrence/print any variable, so if it's empty or not assigned it will print nothing, no errors
my_array=(a b c d e)
echo ${my_array[0]} # print a
echo ${my_array[3]} # print d
echo ${my_array[@]} # print all (@)
echo $!{my_array[@]} # print all indexes (!)
my_array[99]="Ninety-nine" # if you print all the indexes, you will not see all the rest unassigned

# Wildcards
TEXT="Here is one long big pice of text that goes on for awhile"
```

This is find text within text and remove it.

![[Pasted image 20250115101329.png]]

`#` - remove closes range match from left
`##` - remove largest range match from left
`%` - remove closes range match from right
`%%` - remove largest range match from right

Default value setting, value setting and unsetting:

```bash
${foo:-bar} # Set foo = "bar" if foo is not set (:-)
${foo:=bar} # Set foo = "bar" (:=)
unset foo # Make foo null
```

Variables do not have types. You can manually set types if they are needed. `man builtins` will display them.
Every variable is treated like strings, so arithmetic operator `$(())` is used and anything inside treats it like an integer. You also do not have to use the `$` before each variable in here. `bc()` is a calculator program for c style math.

```bash
num=1
num1=5
echo $((num + $num1))
```

`let` statements. Theses can evaluate an arithmetic operator and set a variable to that. This has access to an increment operator `let "var++"`.

```bash
let "sum = num + num1"
let "sum++"
```

`expr` Does the same thing without the `""` quotation marks. You will have to use the escape `\` character for much of the syntax.
`expr 8 \* 2`.
`''` is strong quoting. It will read your arguments and print it out as you typed it, will not read references.
`""` is weak quoting. It will read variables and extract/print the meaning.

### Command Substitution

This is used to capture outputs of commands. Instead of pushing results to a file, you can push results into a variable.

```bash
stat .bashrc # some expression for this example

mystat=$(stat .bashrc)
echo $mystat # will output the results of that expressiong

$(echo ls) # This will be just be treated as ls, this is an unnecessary wrapping
```

### Date

```bash
data +%s%N # Get current epoch time in milli
```

- The seconds since the epoch (`%s`).
- The nanoseconds (`%N`), which provide precision within the current second.

#### Bash Chain Commands Exercise

```bash
ls -R . # -R is recursive. The . is not nessessesary
dir_listing=mylisting.txt
error_log=myerrors.txt
ls -R . > $dir_listing 2> $error_log
START_TIME=$(date +%s%N);

# Combined. This is as complicated command should get in the command line
START_TIME=$(date +%s%N); ls -R . > $dir_listing 2> $error_log && echo "Done. Took $((($(date +%s%N) - ${START_TIME})/100000)) ms" || echo "Could not list add directories. Errors in $error_log"
```

#### Piping Exercise

```bash
stat .bashrc | grep student
```

Three commands needed.

Show all output:
`cat`

Show first x lines:
`head -5`

To sort - Look at field (column) number in manual (man) pages:
`sort`

Get word and line count of file:
`wc`

10 biggest lines in current directory:

```bash
ls -la | sort # pipe to sort, but it sorts it by first line character
# look for the right column to sort on. -k (key), keydef gives location and type. F is field of column
ls -la | sort -k 5 # sorts on column 5, but sort is based on first few character
ls -la | sort -k -nr5 # n is for numberic

# Combined
ls -la | sort -nrk 5 | head -10 > biggest10.txt
```

Highest number of lines:

```bash
wc -l * 2> /dev/null # Directories are treated as errors
wc -l * 2> /dev/null | sort -nr # Total at top
wc -l * 2> /dev/null | sort -nr | head -11 | tail -10 # Cut out top line
```

**DIFF**
Find the difference between text. Diff is used in git like processes.

### Bash Parser

Take line of input, do some transformations, and then execute them.
Good for debugging.

1. Read in line
2. Process quotes - remove special meaning
3. Split data based on words
4. Look for punctuation, braces
5. Expansions
7. Split command into commands and arguments
8. Execute

#### Exercise - Transform line into script

Start script

```bash
touch lstimer.bash
chmod u+x lstimer.bash
vi lstimer.bash
```

Vim

```bash
#!/bin/bash

# Times how long an ls takes to run

directory_listing=mylisting.txt
error_log=myerrors.txt

start$(date +%s%N)

ls -R . > ${directory_listing} 2> ${error_log} && echo "Done. Took $((($(date +%s%N) - start)/1000000))ms." || echo "Could not list all directories in ${error_log}."
```

Execute script:

```bash
cd ~/scripts/
./lsttimer.bash
```

Reformat Vim code

```bash
#!/bin/bash

# Times how long an ls takes to run

target_directory=$1 # This can take in arguments. Positional parameter
directory_listing=mylisting.txt
error_log=myerrors.txt

start$(date +%s%N)

if ls -R ${target_directory} > ${directory_listing} 2> ${error_log}
then
	totaltime=$((($(date +%s%N) - start)/1000000))
	echo "Done. Took $((($(date +%s%N) - start)/1000000))ms."
else
	echo "Could not list all directories in ${error_log}."
fi
```

### [[Day 5 Bash Timing Script Continued#Timer Script|Script Continued]]

### Positional Parameter:

`$0 $1 $2 etc.` This would be an array in modern languages.
`$0` is the command itself.