---
title: Quick reference
---

General tips
------------

* Uppercase and lowercase letters are different:
	* A file called thesis.txt is different from Thesis.txt and tHeSiS.tXt
* Highlight text in the terminal and right click to paste text
	* Right clicking also works for pasting from the Windows clipboard
* Press the up arrow on your keyboard to cycle through previous commands
* Tab will autocomplete file/directory names when typing commands
* Be careful with spaces when writing commands - spaces should separate each option or argument

##Basic navigation

|   |   |
|:----------------- |:--------|
| ls | list contents of the current directory (except hidden files) |
| ls -a | list *all* contents of the current directory |
| ls -l | long-form list of contents, showing file properties |
| ls \<path\> | list contents of specified directory |
| pwd | print working directory (full path) |
| cd \<path\> | go to specified directory |
| cd .. | go up one level to parent directory |
| cd ~ | go to current user's home directory |

##Files and directories

|   |   |
|:----------------- |:--------|
| mkdir \<new-directory\> | create a new directory |
| mkdir -p abc/123 | create two directories: one called *123* inside another called *abc* |
| cp \<file-name\> \<new-file-name\> | create a copy of a file with a new name |
| cp \<file-name\> \<path\> | copy a file to another folder |
| cp \<file-name\> \<path\>/\<new-file-name\> | create a copy with a new name in another folder | 
| mv \<file-name\> \<new-file-name\> | rename a file |
| mv \<file-name\> \<path\> | move a file to another folder |
| rm \<file-name\> | delete a file |
| rm -r \<directory\> | delete a directory and all of its contents |
| nano \<file-name\> | open a new or existing file in a simple text editor |
| chmod ug+x \<file-name\> | give user and group execute permission for a file |

##Inspecting file contents

|   |   |
|:----------------- |:--------|
| cat \<file-name\> | print the contents of a file to the screen |
| less \<file-name\> | opens file contents for inspection, allows scrolling, type q to quit |
| head -5 \<file-name\> | prints first 5 lines of a file |
| tail -3 \<file-name\> | prints last 3 lines of a file |
| sdiff \<file-name\> \<file-name\> | visualise and compare two files side by side |

##Wildcards

|   |   |
|:----------------- |:--------|
| ls \*.txt | list all files ending in *.txt* |
| ls ??? | list all files with names exactly three characters long |
| ls [abc]* | list all files beginning with a, b or c |

##Output redirection and pipiing

|   |   |
|:----------------- |:--------|
| echo "Some text" > a-file | send standard output of a command to a file (overwrites existing content) |
| echo "Some text" >> a-file | append standard output of a command to the end of a file (no overwrite) |
| ls &#124; sort | pipe standard output of a command to another command |


##Variables, sequences and loops

|   |   |
|:----------------- |:--------|
| VAR1=hello | create a variable and set its value |
| echo \$VAR1 | print the value of VAR1 |
| FILENAMES=\$(ls) | save the output of a command as a variable |
| SUM=\$((2 + \$TWO)) | perform integer arithmetic with variables |
| seq 5 10 | print a sequence from 5 to 10 |
| seq 1 2 9 | print a sequence from 1 to 9 with a stride of 2 |
| seq -f %03g 1 2 9 | print a sequence padded with zeroes to the left |
| for i in \$(seq 1 5); do echo iteration$i; done | loop through a sequence and repeat the same instruction for each value |
| for ((i=1; i<=5; i++)); do echo iteration$i; done | alternative method for looping through a sequence |



