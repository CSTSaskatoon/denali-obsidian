### `lstimer.bash`
```bash
#!/bin/bash

# Times how long an ls takes to run
USAGE="./ls_timer.bash [-e <directory>]|[-l <directory>]|[-h]|[-i] <directory>\n\t-e specifies location to write errors\n\t-l specifies location to save listing\n\t-h prints this usage note\n\t-i enables interactive mode\n\tLast argument on the line must be the directory to do an ls of."

directory_listing=mylisting.txt
error_log=myerrors.txt
interactive=0

# Optional switches are -e and -l, last argument is still the directory
while [[ $# -gt 1 ]]
do
	key=$1
	shift

	case $key in
		"-l") # Change the directory listing
			directory_listing=$1
			shift
			echo "Writing listing to $directory_listing"
			;;
		"-e") # Specific location to write errors
			error_log=$1
			shift
			echo "Writing errors to $error_log"
			;;
		"-h") # Usage notes about the program
			echo -e $USAGE
			;;
		"-i") # Enable interactive mode
			interactive=1
			;;
		*)
			echo -e "Argument $key not recognized. Invoke with -h for help."
			exit 2
			;;
	esac
done

target_directory=$1
# Test if the directory is invalid
if [[ ! -d $target_directory ]]
then
	echo "$target_directory is not valid, please supply a target"
	exit 2
fi

if [[ $interactive -eq 1 ]]
then
	read -p "About to do a recursive listing of $target_directory. Continue? [y to continue]" continue_answer

	continue_answer=$(echo $continue_answer | awk '{print tolower($0)}')
	if [[ ! $continue_answer =~ ^(Y|y|yes) ]] # technically don't need Y cause we converted it
	then
		echo "Aborting ls."
		exit 0
	fi
fi

start=$(date +%s%N)

if ls -R ${target_directory} > ${directory_listing} 2> ${error_log}
then
	totaltime=$((($(date +%s%N) - start)/100000))
	echo "Done. Took $totaltime ms"
else
	echo "Could not list all directories. Errors in ${error_log}"
fi
```

### `positionalarguments.bash`
```bash
#!/bin/bash
# Demonstrate positional arguments
echo "Positional Arguments are 0: $0, 1: $1, 2: $2, 3: $3, 4: $4 and so on"
echo "We have $# positional arguments"

while [[ $# -gt 0 ]]
do
	echo "We have $# positional arguments left"
	echo "Positional argument in position 1: $1"
	shift
done
```

### `loops.bash`
```bash
#!/bin/bash
# Loops

# foeach
for element in one two three
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
	echo "Element is $element"
done

# C style for loop
for ((i=0; i < ${#my_array[@]}; i++))
do
	echo "C loop style $i: ${my_array[$i]}"
done

# While loop
while_counter=0
while [[ $while_counter -lt ${#my_array[@]} ]]
do
	echo "While loop: ${my_array[$while_counter]}"
	let "while_counter++"
done

# Until loop
until_counter=$((${#my_array[@]} - 1))
until [[ $until_counter -le 0 ]]
do
	echo "Until loop: ${my_array[$until_counter]}"
	let "until_counter--"
done

# does the command in quotes when you hit ctrl + c
trap "echo Goodbye you goober" SIGINT 

select value in one two three four
do
	echo "You chose $value"
done
```

### `flowcontrol.bash`
```bash
#!/bin/bash
#
# Demonstrate flow control in bash

# Taking in one argument
key=$1

# Using boolean operators
test $key = "Yes" && echo "You said yes" || echo "You said something other than yes."

# If statements
if test $key = "Yes"
then
	echo "You said Yes"
elif test $key = "No"
then
	echo "You said No"
else
	echo "You said something else"
fi

# Case statement
case $key in 
	Yes|yes) # user said yes
		echo "You said yes"
		;;
	No|no)
		echo "You said no"
		;;
	*) # Default case
		echo "You said something else"
		;;
esac
```

### `linenumber.bash`
```bash
#!/bin/bash
#
# Demonstrate reading in a file and applying line numbers to it

filename=$1

if [[ ! -f $filename ]]
then
	echo "Supply the name of a file to add line numbers to"
	exit 2
fi

lineno=1
while read line
do
	echo "$lineno: $line"
	let "lineno++"
done < ${filename}
```

### `readwithifs.bash`
```bash
#!/bin/bash
#
# Demonstrate the internal field seperator

# the IFS environment variable determines what characters to split on
echo "IFS is '$IFS'" # By default it's a newline character

old_ifs=$IFS
IFS=","

while read input
do
	counter=0
	for word in $input
	do 
		echo "Word $counter: $word"
		let "counter++"
	done
done

IFS=$old_ifs
```

### `filetypes.bash`
```bash
#!/bin/bash
#
# Read in a list of files, determine what type they are

FILEOFFIELNAMES=$1

while read LINE
do
	FILETYPE="$(file $LINE | awk '{print $2}')"
	case $FILETYPE
		"empty")
			echo "$LINE: Empty File"
			;;
		"directory")
			echo "$LINE: Directory"
			;;
		"cannot")
			# For now, skip file we can't access
			;;
		*)
			echo "Something else"
			;;
	esac
done < $FILEOFFILENAMES
```

### `getopts.bash`
```bash
#!/bin/bash
#
# getopts shell feature

while getopts ":ab:c" OPTION
do
	echo "Option is $OPTION"
	echo "Optarg is $OPTARG"
	echo "Optind is $OPTIND"
done

echo "Done parsing using optargs"
echo "The first position variable is $1"
echo "$OPTIND is the next index, let's shift by that amount"
shift $((OPTIND - 1))
echo "Now the next argument is $1"

echo "Maybe it's a command that takes in more than one argument that isn't a switch"

while [[ $# -gt 0]]
do
	file $1
	shift
done
```
**`getopt` is not recommended**

### `say_hello.bash`
```bash
#!/bin/bash
#
# Demonstrate functions in bash

# say_hello - command not found because it's not declared yet

say_hello ()
{
	NUMTIMES=$1
	for ((i=0; i<$NUMTIMES; i++))
	do
		echo "Hello fucker"
	done
	echo "1: $1, 2: $2, 3: $3"
}

# Pass in arguments like you would for a command line argument
say_hello 5
```

**Can also declare these on the command line, ex.**
```bash
say_something () { echo "Something says $1"; }

say_something else # prints 'Something says else'
```

### `subshells.bash`
```bash
#!/bin/bash
#
# Demonstrate subshells

MYVAR="A variable"
echo "MYVAR is $MYVAR"
(
	# Apparently it does copy environment variables into the subshell
	echo "In the subshell, MYVAR is $MYVAR"
	MYVAR="New var"
	for ((i=0; i<5; i++))
	do
		sleep 1
		echo "Sleeping $i"
	done
	echo "In the subshell, I changed MYVAR to $MYVAR"
) & # & makes it work in the background

# Even though we changed it in the subshell it's still the same
echo "MYVAR is $MYVAR"
```
