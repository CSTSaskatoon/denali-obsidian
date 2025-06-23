Graphic features with G-Vim:

```
sudo apt instal vim-gtk3
```

This has a graphic window for the editor.

Neovim is like visual studio code, but looks like VIM. It is easier for 3rd party to make extensions.

```
sudo apt install neovim
```

### Timer Script IF USES TEST

```bash
#1/bin/bash

# Times how long an ls takes to run

target_directory=$1 # This can take in arguments. Positional parameter. Pass in directory to read
directory_listing=mylisting.txt
# directory_listing=${DIRLISTING}:=mylisting.txt # This is optional, forces user to export this env var
error_log=myerrors.txt

# if test -d $target_directory
# if [ -d $target_directory ] # Same as "test" command
if [[ ! -d $target_directory ]] # Built/add-on that does what "test" does, with extra options
then
	echo "$target_directory is not valid, please supply a target."
	exit 2
fi

# Timer
start$(date +%s%N)

if ls -R ${target_directory} > ${directory_listing} 2> ${error_log}
then
	totaltime=$((($(date +%s%N) - start)/1000000))
	echo "Done. Took $((($(date +%s%N) - start)/1000000))ms."
else
	echo "Could not list all directories in ${error_log}."
fi
```

### Test `[]`

This command can do many IO and data type checks. They return status codes, 0 for pass, >0 for failures.

The double `[[]]` square brackets does additional functions to test. It has extra features including:

- IF Statements (`-d` directory exist, `-e` file exist, `nt` newer than)
- Handles empty strings
- AND and OR
- JavaScript like comparisons
- Regex matching

### Positional Arguments Script

`posisionalarguments.bash`

```bash
#!/bin/bash
# Demonstare Positional Argumetns

echo "Positional arguments 0: $0, 1: $1, 2: $2, 3: $3, 4: $4, and so on"
echo "We have $# positional arguments."

shift

echo "Positional arguments 0: $0, 1: $1, 2: $2, 3: $3, 4: $4, and so on"
echo "We have $# positional arguments."
```

Loop through arguments with `shift`.
Makes the arguments decrease an index, so it erases the `$1` index and replaces with `$2`.
`#$` is the number of positional arguments.

This can be use for *while* loops.

```bash
#!/bin/bash
# Demonstare Positional Argumetns

echo "Positional arguments 0: $0, 1: $1, 2: $2, 3: $3, 4: $4, and so on"
echo "We have $# positional arguments."

while [[ $# -gt 0 ]]
do
	echo "We have $# positional arguments left."
	echo "Positional arguments in position 1: $1"
	shift
done
```

`gt` is "greater than". This is inside the `test` man pages.

#### Loops Script

```bash
#!/bin/bash

# Demonstrate how loops work in bash

# Foreach loop
for element in one two three # Space seperated list of elements
do
	echo "Element is $element"
done

for element in *
do
	echo "Element is $element"
done

my_array=(a b c d e)
for element in ${my_array[@]}
do
	echo "Element in $element"
done

# C-style or Java  for loop
for ((i=0; i < ${#my_array[@]}; i++)) # The double bracks indicates it is a c-style loop
do
	echo "C-Style Loop $i: ${my_array[$i]}"
done

# While loop
while_counter = 0
while [[\#mymy_array[@]} ]] # the hashtag before the array gets the number/COUNT of elements. Backslash not needed, just need it for Obsidian notes
do
	echo "While loop: ${my_array[$while_counter]}"
	let "while_counter++"
done

# Until lop
until_counter=${#my_array[@]}
until [[ $until_counter -lt 0 ]]
do
	echo "until loop: $(my_array[#until_counter])"
	let "until_counter--"
done

# This is included for fast user menus.
select value in one two three four
do
	echo "You chose $value"
done

trap "echo Goodbye; exit 0" SIGINT # Make sure to exit or else user will be trapped

# This will let the user chose the .bash file they want to select. This also starts at 1
select value in *.bash
do
	echo "You chose $value"
done
```

Wild cards in loops.
`*` can get a list of files easily.

### Ctrl + c

This is an interrupt *signal*. A signal is what goes in-between programs. They can be intercept with the `trap` so run program function when that signal is caught. `SIGINT` is the signal for interrupt in particular.

### Flow Control and Case Statements

`flowcontrol.bash`

```bash
#!/bin/bash

# Demonstrate flow control in bash

# We're taking in one argument:
key=$1

# Using boolean oeprators
test $key = "Yes" && echo "You said Yes." || echo "You said something other than yes."

$ If statements
if test $key = "Yes"
then
	echo "You said Yes"
elif test $key = "No"
then
	echo "You said No"
else
	echo "You said something other than yes or no"
fi

# Case statement
case $key in
	Yes|yes) # The user siad yes
		echo "You said Yes"
		;;   # This is the break
	No|no)   # The user said no
		echo "You said No"
		;;
	*)       # Default case, it is not mandatory
		echo "You said neight yes nor no"
		;;
esac
```

### Timer Script Part 3 - Writing our own flags - includes awk

```bash
#1/bin/bash

# Times how long an ls takes to run
USAGE="./ls_timer.bash [ -e <directory> ] |  [ -l <directory> ] | [ -h <directory>}\n\t -e specifies location to write errors\n\t -l specifies location to save listing\n\t -h prints this usage notes\n\t Last argument on the line must be the directory to do an ls of."

# directory_listing=${DIRLISTING}:=mylisting.txt # This is optional, forces user to export this env var
directory_listing=mylisting.txt
error_log=myerrors.txt
interactive=0

# Optional sitchest are -e and -l. The last argument must still be the directory.

# Exercise:
# Add a -h option which will display some usages notes about the program
# If the user supplies an invalid option, exit with an appropriate error
# status and tell the user they can use -h to print usage notes.

while [[ $# -gt 1 ]]
do
	key=$1
	shift

	case $key in
		"-l") # Specify place to put directory listing
			directory_listing=$1
			shift
			echo "Writing listing to $directory_listing"
			;;
		"-e") # Specify location to writing errors
			error_log=$1
			shift
			echo "Writing errors to $error_log"
			;;
		"-h") # Print usage notes
			echo -e $USAGE # -e allows \n (new line) and other escapse characters
			;;
		"i") # Enable interactive mode
			interactive=1
			;;
		*)
			echo "Argument $key not recongnized. Invoke with -h for help."
			exit 2
			;;
	esac
done

target_directory=$1 # This can take in arguments. Positional parameter. Pass in directory to read

# if test -d $target_directory
# if [ -d $target_directory ] # Same as "test" command
if [[ ! -d $target_directory ]] # Built/add-on that does what "test" does, with extra options
then
	echo "$target_directory is not valid, please supply a target."
	exit 2
fi

# Interactive
if [[ $interactive -eq 1 ]] #eq is equals
then
	read -p "About to do a recursive listing of $target_directory. Continue? [y to continue]" continue_answer
	
	continue_answer=$(echo $continue_answer | awk '{print tolower($0)}') # Redundant with regex below, this was added later
	
	if [[ ! $continue_answer =~ ^(Y|y|yes) ]] # =~ is regex matching. Carrot (^) is starting from the left
	then
		echo "Aborting ls."
		exit 0
	fi
fi

# Timer
start$(date +%s%N)

if ls -R ${target_directory} > ${directory_listing} 2> ${error_log}
then
	totaltime=$((($(date +%s%N) - start)/1000000))
	echo "Done. Took $((($(date +%s%N) - start)/1000000))ms."
else
	echo "Could not list all directories in ${error_log}."
fi
```

**read**

`man builtin` takes input from standard input and put into a variable or into multiple variables, by default is the terminal.
`-p` is prompt.
### awk

Pattern scanning and text processing language. It is used for text transformation mainly for user input.
Converting text into lower case.

```bash
ls -la | awk '{print $4}'          # Print out that 4th column
ls -la | awk '{print toupper($0)}' # To upper case
```

### Read in text from a file

`linenumberer.bash`

```bash
#!/bin/bash

# Demonstate reading in a file and applying line number to it:

filename=$1

if [[ ! -f ${filename} ]]
then
	echo "supply the name of a file to add line numbers to"
	exit 2
fi

lineno=1
while read line # < ${filename} # Read does not increment itself
do
	echo "$lineno: $line"
	let "lineno++"
done < ${filename} # Changes the standard input
```

By default, standard input is the terminal.
Using redirection for reading a file instead.

```bash
./linenumberer.bash lstimer.bash < binlisting.txt
```

### Internal Field Separator (IFS) script

(cut and awk can also do it).

`readwithifs`

```bash
#!/bin/bash

# The IFS environment variable determines what characters to word split on:
echo "IFS is '$IFS'"

old_ifs=$IFS # Preserve old IFS

IFS=","

# Demonstrage the internal field seperator
while read input # Read from standard input and input with equal that result. Breaks on spaces and line break (but read only goes up to the line break)
do
	# echo "$input"
	counter=0
	for word in $input
	do
		echo "Word $counter: $word"
		let "coutner++"
	done
done

$IFS=old_ifs # Restore IFS
```

### Echo instead of Cat

```bash
echo "$(<a.txt)"
echo -e "$(<a.txt)" # Enable escape charcters
```
## Exercise File Type Script

---

Write a script that will take an argument a file that has a list of filenames. For each file, print whether the file is a directory, an empty file, or something else. It should have two optional arguments –i will ignore empty files, and –s will print out a sum of how many files of each type were found.

Add error handling – quit with error if passed in an invalid file, print out “doesn’t exist” for line that point to files that don’t exit, and sum should display how many of the lines weren’t a file.

_Hint:_ You can use the **file** command to display the type of a file. You can use the **awk** command in something like awk ‘{print $2}’ to print out the second column of output. You can also use the **cut** command to chop apart input by a delimiter. All of these commands have man pages.
