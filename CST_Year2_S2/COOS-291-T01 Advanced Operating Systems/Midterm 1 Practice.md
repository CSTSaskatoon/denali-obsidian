> I cut some parts out of labs/exercises that weren't really needed. You don't need to write down your answers, but you should at least know the answer to every question

## Class Exercises
### Part 1 (LO1 Lab 1)
1. How do you refer to the root of the Linux file system?
2. What is the Linux command that prints out the directory you are currently in?
3. When you first open the terminal, what directory are you in?
4. In Ubuntu, what directory are all account home directories located in by default?
5. What Linux command is used to list the contents of a directory?
6. What is the short option to list all the files in a directory?
7. What is the long option to list all files in a directory?
8. What is the command to create a directory?
9. What command you use to switch directories?
10. What command would you use to change to the parent directory?
11. What command is used to move a file to another directory?
12. What command is used to rename files/directories?
13. What is the one character abbreviation to refer to your account's home directory?
14. What command is used to delete a directory?
15. What command can you use to view the contents of a file?
16. What is the difference between the `more` and `less` commands?
17. What is the difference between the `more` and `cat` commands?
18. What command is used to display the last few lines of a file?
19. What command is used to display the top few lines of a file?
20. Write a command that will redirect the output of `cat` into a file
21. What does the `<` symbol do?
22. Use `<` to redirect the contents of a file into the `cat` command
23. What does `"Some text" >> somefile.txt` do?
24. Write a command that will list the file in `/etc` in descending order of number of lines in the file (assuming they are all `.txt` files)

### Part 2 (LO1 Lab 2)

## SOLUTIONS (Minimize this header)
### Part 1 (LO1 Lab 1)
1. `/`
2. `pwd`
3. `/home/USERNAME/`
4. `/home/`
5. `ls`
6. `-a`
7. `-la`
8. `mkdir`
9. `cd`
10. `cd ..`
11. `mv`
12. `mv OLDNAME NEWNAME`
13. `~` (tilde)
14. `rmdir` or `rm -d`
15. `cat`
16. `less` does more
17. `more` 'opens' the file for paging, `cat` prints it out to the terminal
18. `tail`
19. `head`
20. `cat somefile.txt > anotherfile.txt`
21. It redirects the standard input (Ex. `command < somefile.txt` would pass the contents of `somefile.txt` instead of the file itself. Some commands like `cat` can take in the filename OR the contents, but some can only take in the contents)
22. `cat < somefile.txt`
23. Appends the text `"Some text"` to `somefile.txt`
24. 

### Part 2 (LO1 Lab 2)
