---
title: Exercise solutions
---

Exercise
--------

* Create the following directory tree in your home directory (```~```):

```
    work
    work/input_data/
    work/results/
    work/program/
```

* Create the file "input.txt" with a text editor and put some text in it.

* Move the file to work/input_data and rename it in the same command to control01.txt

* Create this directory tree in one line only: work/experiment/results/report

* Delete the work directory and all of its contents with one single command.

Solution
--------

```
[user@host ~]$ mkdir work work/input_data work/results work/program
[user@host ~]$ nano input.txt
[user@host ~]$ mv input.txt work/input_data/control01.txt
[user@host ~]$ mkdir -p work/experiment/results/report
[user@host ~]$ ls -R work
work:
experiment  input_data  program  results

work/experiment:
results

work/experiment/results:
report

work/experiment/results/report:

work/input_data:
control01.txt

work/program:

work/results:
[user@host ~]$ rm -r work
```

Exercise
--------
Two new commands:

* The ```sort``` command will sort lines alphabetically
* You can use the ```cut``` command to split lines of text based on a given character
	* e.g. ```cut -d ',' -f 2``` will split lines around the comma and give you the second part
	
1. Combine cat, cut, and sort to print out the Latin names from birds.txt in alphabetical order
2. Save the output to a new file

Solution
--------

```
[user@host IOM-animals]$ cat birds.txt | sort | cut -d ',' -f 2
```

```
[user@host IOM-animals]$ cat birds.txt | sort | cut -d ',' -f 2 > sorted-birds.txt
```

Exercise
--------

List all the animals on the Isle of Mann alphabetically and find the 50th item in that list

Solution
--------

```
[user@host IOM-animals]$ sort *.txt | head -50 | tail -1
coot, fulica atra
```

* To get the 50th line, use head to get the first 50 lines and pipe it to tail to get the last one

Exercise
--------
```shell-training/data/``` contains 300 data files, each of which *should* contain 100 values.
One of these files is missing some data though...

* Use a series of commands connected by pipes to identify the file with missing data
* **hint** ```wc -w``` will tell you the number of values in a file, ```sort -n``` will sort numerically

Solution
--------

```
[user@host data]$ wc -w values* | sort -n | head -1
    99 values44
```

* 'wc -w' tells you how many values are in each file
* sort this output to put the files in order of the number of values
* use head to select the first line, which contains the name of the file with the smallest number of values

Exercise
--------
* Use a for loop to create five directories called calculation_?, where ? is a number.
* Use a loop to create five directories, each one the parent of the next.

Solution
--------

```
[user@host ~]$ for (( i=1 ; i<=5 ; i++ ))
> do
> mkdir calculation_$i
> done
[user@host ~]$
```

```
[user@host ~]$ for (( i=1 ; i<=5 ; i++ ))
> do
> mkdir calculation_$i
> cd calculation_$i
> done
[user@host calculation_5]$
```

* In the second case, two commands are executed each time you go through the loop.
* A new directory is created and then the working directory is changed to the new directory.
* On the next iteration, the new directory is then created inside the previous one.


Exercise
--------

* In the wildcards directory, create a variable called *files* listing all of the text files.
* Loop through this list and print out the first line from each file.

Solution
--------

```
[user@host wildcards]$ files=$( ls *.txt )
[user@host wildcards]$ for f in $files
> do
> head -1 $f
> done
```

Or

```
[user@host wildcards]$ for f in $( ls *.txt )
> do
> head -1 $f
> done
```

Exercise
--------

* What will this command print to the screen?

```
[user@host wildcards]$ for filename in *.txt
> do
> echo $filename
> cat $filename > new-file.txt
> done
```

* What will the contents of new-file.txt be and why?

Solution
--------

* What will this command print to the screen?
  + The name of each .txt file in the current directory
  + On each iteration the echo command prints a different file name

* What will the contents of new-file.txt be and why?
  + The content of new-file.txt will be the same as xyz.txt
  + On each iteration the contents of a different file are written to new-file.txt, overwriting whatever was written on the previous iteration
  + This is because we used '>' to write the output of cat to new-file.txt
  + Using '>>' instead would result in each file's content being appended to the end of new-file.txt

Exercise:
---------

* Recreate the ```a_directory/inside/the_other``` tree if you deleted it.

* Add write permission for users from your group for the full directory tree with one single **chmod** command (look in the man pages for more information).

* What happens if you can read but not execute a directory?

Solution
--------

```
[user@host ~]$ mkdir -p a_directory/inside/the_other
[user@host ~]$ ls -Rl a_directory/
a_directory/:
total 0
drwxr-xr-x 3 cceaxxx cceas0 256 Nov  6 10:09 inside

a_directory/inside:
total 0
drwxr-xr-x 2 cceaxxx cceas0 256 Nov  6 10:09 the_other

a_directory/inside/the_other:
total 0
[user@host ~]$ chmod -R g+w a_directory
[user@host ~]$ ls -Rl a_directory/
a_directory/:
total 0
drwxrwxr-x 3 cceaxxx cceas0 256 Nov  6 10:13 inside

a_directory/inside:
total 0
drwxrwxr-x 2 cceaxxx cceas0 256 Nov  6 10:13 the_other

a_directory/inside/the_other:
total 0
```

* 'ls -Rl' shows us the permissions set for each directory
* The permissions list for each directory changes from drwxr-xr-x to drwxrwxr-x

Exercise:
--------

* Create a "Hello world"-like script using a text editor and execute it.

* Redirect the output from your script to a file or another program.

Solution
--------

A hello world script:

```
#!/bin/bash

echo "Hello world!"
```

Make it executable:

```
[user@host ~]$ chmod +x hello-world.sh
```

Run the script:

```
[user@host ~]$ ./hello-world.sh
Hello World!
```

Send the output to a file:

```
[user@host ~]$ ./hello-world.sh > hello.txt
[user@host ~]$ cat hello.txt
Hello World!
```

Send the output to another program:

```
[user@host ~]$ ./hello-world.sh | wc -w
2
```

Exercise
--------

* Write a script which will create as many numbered directories as you want when you run it.

Solution
--------

The script:

```
#!/bin/bash

echo Creating $1 directories...

for (( i=1 ; i<=$1 ; i++ ))
do
mkdir directory_$i
done

echo Finished!
```

Running the script:

```
[user@host ~]$ chmod +x n-dirs.sh
[user@host ~]$ ./n-dirs.sh 8
Creating 8 directories...
Finished!
```


Exercise
--------

* Write your own **mid** command which will print a selection of lines from the middle of a file depending on the arguments you pass to it.

Solution
--------

The script:

```
#!/bin/bash

head -$2 $3 | tail -$(($2 - $1 + 1))
```

Running the script:

```
[user@host wildcards]$ chmod +x mid.sh
[user@host wildcards]$ ./mid.sh 5 8 cake.txt
such as pastries, meringues, custards and pies.

Typical cake ingredients are flour, sugar, eggs, and butter
or oil, with some recipes also requiring additional liquid
```

* In this example \$1 is the first line, \$2 is the second, and \$3 is the name of the file

A more complete solution using getopts to handle named options:

```
#!/bin/bash

if ( ! getopts ":s:e:f:" opt); then
        echo "Usage: `basename $0` options (-s value) (-e value) (-f filename)";
        exit $E_OPTERROR;
fi

while getopts ":s:e:f:" opt; do
    case $opt in
        s)
          start=$OPTARG >&2
          ;;
        e)
          end=$OPTARG >&2
          ;;
        f)
          filename=$OPTARG >&2
          ;;
        \?)
          echo "Invalid option: -$OPTARG" >&2
          exit 1
          ;;
        :)
          echo "Option -$OPTARG requires an argument." >&2
          exit 1
          ;;
    esac
done

head -$end $filename | tail -$(($end - $start + 1))
```

