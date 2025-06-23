## Q1
Exercise: Chaining commands

`date +%s%N` will get you the current epoch time in nanoseconds 

`set dir_listing=mylisting.txt`, and `set error_log=myerrors.txt`

Write a one-line bash command which which does an "`ls -R` ." and output the directory listing to the filename specified in the `dir_listing` variable, outputs any errors from the `ls` to the file specified in `error_log`.

When the ls is done, if there were no errors display  "Done. Took `<insert time inms>` ms." If the ls did have errors, display instead "Could not list all directories. Errors in `<location of the error log>`."

**Solution**
```bash
START_TIME=$(date +%s%N); ls -R . > $dir_listing 2> $error_log && echo "Done. Took $((($(date +%s%N) - ${START_TIME})/100000)) ms" || echo "Could not list add directories. Errors in $error_log" 
```

**Script version with some extra features**
```bash
#!/bin/bash

# Times how long an ls takes to run

echo "My positional parameters are: 0: $0 1: $1 2: $2 3: $3 4: $4"

target_directory=$1
directory_listing=mylisting.txt
error_log=myerrors.txt

# Test if the directory is invalid
if [[ ! -d $target_directory ]]
then
	echo "$target_directory is not valid, please supply a target"
	exit 2
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

## Q2
Using the sort, head, and ls commands, generate a file that contains the names and information on the 10 biggest files in the current directory.

**Solution**
```bash
ls -ls | sort -nrk 1 | head -10 > biggest10.txt
```

## Q3
**Solution**
```bash
wc -l * 2> /dev/null | sort -nr | head -11 | tail -10
```

## Q4
Write a script that will take an argument a file that has a list of filenames. For each file, print whether the file is a directory, an empty file, or something else. It should have two optional arguments `–i` will ignore empty files, and `–s` will print out a sum of how many files of each type were found.

Hint: You can use `awk '{print $2}'` to print out the second column of output.

Add error handling – quit with error if passed in an invalid file, print out “doesn’t exist” for line that point to files that don’t exit, and sum should display how many of the lines weren’t a file.

**Solution**
```bash
#!/bin/bash

ignore_empty=0
sum_files=0

while [[ $# -gt 1]]
do
	key=$1
	shift
	case $key in
		"-i")
			ignore_empty=1
			;;
		"-s")
			sum_files=1
			;;
		*)
			echo "Argument $key not recognized"
			exit 2
			;;
	esac
done

file_to_search=$1

# check if file is invalid

if [[ -d $file_to_search ]]
then
	if [[ ignore_empty = 0 || ls -1 $file_to_search | wc -l -gt 0]]
		# would sum file types here
	fi

fi
```

## Q5 - Backup Script
Write a script called `backup.bash` which does the following things:

1. Checks to see if the directory `BACKUPS` exists in the current directory.
    - If it does not, check to see if there is a non-directory file called BACKUPS in the current directory
        - If there is, exit with an error message saying the `BACKUPS` directory could not be created
        - If there is nothing called `BACKUPS`, make a `BACKUPS` directory
2. Go through every file in the current directory, and
    - If the file doesn't exist in the `BACKUPS` directory, copy it to the `BACKUPS` directory
    - If the file does exist in the `BACKUPS` directory but the copy in the current directory is newer, copy the one in the current directory overtop of the `BACKUPS` directory
    - If the file cannot be copied for any reason, print an error message
    - Keep track of how many files were successfully copied
    - Keep track of how many files weren't able to be copied because the copy command failed
3. At the end, print out a message saying the backup is done and reporting how many files were copied, and how many file could not be copied.

Once you've got the basics done, add some more user-friendly features:

- Ensure the script exits with an appropriate error code - a code of 0 if everything was backed up successfully, a code of 1 if errors were encountered and the script couldn't back up everything, or an error code of 2 if the user supplied invalid input
- Allow the user to supply a `-e` switch to ignore empty files when doing the backup.
- Allow the user to supply a `-d` `<directory name>` switch to specify a different directory to use other than `BACKUPS`

```bash
#!/bin/bash
#
# Create Backups

BACKUPS="./BACKUPS"
COPIED=0
NOTCOPIED=0
IGNOREEMPTIES=0

while getopts ":ed:" OPTION
do
	case $OPTION in
		"e")
			echo "Ignoring empty files"
			IGNOREEMPTIES=1
			;;
		"d")
			BACKUPS="$OPTARG"
			echo "Using $BACKUPS as the backup directory"
			;;
		*)
			echo "Only valid options are e or d"
			exit 2
			;;
	esac
done

if [[! -d "BACKUPS" ]]; then
	if ! mkdir "$BACKUPS" 2> /dev/null; then
		echo "Could not create backup directory $BACKUPS"
		exit 1
	fi
fi

for file in *
do
	if [[ $IGNOREEMPTIES -eq 1 && $(wc -c "$file" 2> /dev/null | cut -f 1 -d " ") -eq 0]]; then
		SKIP=1
	else
		SKIP=0
	fi

	if [[ $SKIP -eq 0 && ( ! -e "$BACKUPS/$file" || "$file" -nt "$BACKUPS/$file" ) ]]; then
		if cp "$file" "$BACKUPS/$file" 2> /dev/null; then
			let "COPIED++"
		else
			echo "Could not copy $file"
			let "NOTCOPIED++"
		fi
	fi
done

echo "Successfully copied $COPIED files, and failed to copy $NOTCOPIED files"

if [[ $NOTCOPIED -ne 0 ]]
	exit 1
fi

exit 0
```

## Q6 - File Renamer
A frequent tedious task you can encounter is having to rename a bunch of files. Maybe you downloaded a bunch of files `PictureDog`, `PictureCat`, etc. and you want to renamed them to `PictureDog.jpg`, `PictureCat.jpg`, etc. Or you downloaded a bunch of files called `DOCUMENT1`, `DOCUMENT2`, `DOCUMENT3`, etc. and you want them renamed to `Assignment1.docx`, `Assignment2.docx`, `Assignment3.docx`

Write a script called `filerename.bash.` It should take the following arguments:

- **`-p <string>`** - apply the given string as a prefix to all the files supplied to the script
- **`-s <string>`** - apply the given string as a suffix to all the files supplied to the script
- **`-r <string1> <string2>`** - for all the files, anywhere string1 occurs in the filename replace it with string2
- After any switches, the rest of the arguments should be what files to rename

**Example usage:**
**`filerename.bash -s .docx Document1 Document2`**
- Adds the `.docx` prefix to Document1 and Document2

**`filename.bash -s .rtf`**
- This should return an error because no filenames were supplied to do the rename on.

**`filerename.bash -p My -r Picture Image *.jpg`**
- For all the files in the current directory that end in `.jpg`, add the prefix `My` to the filename and replace the word `Picture` with the word `Image` in the filename.

**`filename.bash -r First Last *.docx`**
- In all the files in the current directory that end in `.docx`, replace the word `First` in their names with the word `Last`.

**`filename.bash -r Mine Yours`**
- This should also return an error because no file names were supplied.

```bash
#!/bin/bash
#
# Create Backups

$PREFIX=""
$SUFFIX=""
$FIND=""
$REPLACE=""
declare -a FILE_LIST=()

while [[ $# -gt 1 ]]
do
	key=$1
	shift

	case $key in
		"-p") # Change the directory listing
			$PREFIX=$1
			shift
			echo "Prefix is $PREFIX"
			;;
		"-s") # Specific location to write errors
			$SUFFIX=$1
			shift
			echo "Suffix is $SUFFIX"
			;;
		"-r") # Usage notes about the program
			$FIND=$1
			shift
			$REPLACE=$1
			shift
			echo "Replacing $FIND with $REPLACE"
			
			;;
		*)
			if find $1; then
				FILE_LIST+=($1)
			else
				echo "$1 is not a file or directory"
				exit 2
			fi
			;;
	esac
done

if $FIND -ne "" || $REPLACE -ne ""; then
	mv $(grep $FIND)

```
