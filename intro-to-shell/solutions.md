---
title: Exercise solutions
---

Exercise
--------

The shell-training folder has the following structure:

~/shell-training
|--animals
|--data
|--docs
|--scripts

1. What is the absolute path to the docs directory? Use the absolute path to change into this directory
2. From there, list the contents of the animals directory using a relative path

Solution
--------

1. ```cd /home/<username>/shell-training/docs```
2. ```ls ../animals```

Exercise
--------

Write a script that will do the following steps: a. Create a new directory called cake inside your home directory b. Use an absolute path to create a directory inside cake called "Cheesecake" c. Change into the Cheesecake directory d. Use a relative path to create another directory inside cake called "Battenberg" e. Return to the home directory and list the contents of cake

The final set of directories should look like this:
```
~/cake 
|--Cheesecake
|--Battenberg
```

Solution
--------

The script:
```
mkdir ~/cake
mkdir /home/<username>/cake/Cheesecake
cd /home/<username>/cake/Cheesecake
mkdir ../Battenberg
cd ~
ls cake
```

Exercise
--------

Read the man page for mkdir to find out what the -p option does. Use it to create the following set of directories with a single command:
```
~/bread
|--focaccia
|--naan 
```

Solution
--------

The -p option will make parent directories as needed. Use two arguments to make the two sub directories, and the -p option creates the bread directory automatically.

```
mkdir -p ~/bread/focaccia ~/bread/naan
```

Exercise
--------

Use grep to search through all of the files in the animal directory to find animals with the word red in their name. Read the man page to find out how to make grep only select the word red, and not just any word containing r-e-d.

Solution
--------

The man page for grep says the -w option will select only those lines containing matches that form whole words.

```
grep -w red *.txt
```

Exercise
--------

The docs directory contains several files ending in ".txt". Write a backup script that will create a backups folder and copy each of these files there.

* Run the script
* Delete two of the original text files and use nano to edit another
* Use sdiff to compare the file you've changed with the backed up version
* Read the cp man page to find out how to restore the deleted files from the backup folder without overwriting the changes you have made to the other files

Solution
--------

The script (backup.sh):

```
mkdir -p ~/shell-training/docs/backup
cp ~/shell-training/docs/*.txt ~/shell-training/docs/backup
```

Restore deleted files without overwriting:

```
cp -n ~/shell-training/docs/backup/* ~/shell-training/docs/
```

Exercise
--------

1. Use the wget command to download Alice's Adventures in Wonderland: https://www.gutenberg.org/files/11/11.txt
2. Use less to read the file, search for specific words, and step through the results
3. Use grep to print lines containing a specific word or phrase to the screen; e.g. how many times is the Cheshire Cat mentioned?
4. Use sed to replace every instance of Alice with your own name, and redirect the result to a new file.
5. Using a combination of head and tail, find lines 325-335

Solution
--------

```
wget https://www.gutenberg.org/files/11/11.txt
less 11.txt
grep "Cheshire Cat" 11.txt
sed 's/Alice/YourName/g' 11.txt > YourName.txt
head -n 335 11.txt | tail
```

Exercise
--------

* In the docs directory, create a variable called files listing all of the text files.
* Loop through this list and print out the first line from each file.

Solution
--------

```
cd ~/shell-training/docs
files=$(ls)
for file in $files; do head -n 1 $file; done
```

Exercise
--------

* Use a for loop to create five directories called calculation_?, where ? is a number.
* Use a loop to create five directories, each one the parent of the next.

Solution
--------

```
for ((i=1;i<=5;i++)); do mkdir calculation_$i; done
```

```
for ((i=1;i<=5;i++)); do mkdir calculation_$i; cd calculation_$i; done
```

Exercise
--------

* Find a partner who is in the same group as you. Use the groups command to check.
* In your home directory, create a new directory and give members of your group write access to it, but take away read access.
* Tell your partner the absolute path to the directory you've given them write access to.
* Share files by copying them to each other's shared directories.

Solution
--------

```
mkdir ~/group
chmod g+w-r ~/group
cp <file> /home/<username>/group
```

Exercise
--------

The data folder contains 200 files. Each file is named according to a type of measurement (A or B), and a location (1-100) e.g. A21, B56 etc. The scripts folder contains a python script which takes the names of an A and a B file as arguments e.g. scripts/calculatescore.py data/A_1 data/B_1 This will calculate a score based on the data in the two files and print it to standard output along with the name of the files used.

1. Make calculate_score.py executable
2. Use a for loop to run through the data files corresponding to each location and generate a score
3. Modify the for loop to save the scores to a file
4. Use the sort command to find the location with the highest score

Solution
--------

```
cd ~/shell-training
chmod u+x scripts/calculate_score.py
for ((i=1;i<=100;i++))
do
scripts/calculate_score.py data/A_$i data/B_$i >> results
done
sort results
```

Location 80 has the highest score with 0.18

Exercise
--------

You can now control the number of times a for loop iterates by including a number as an argument when you call it. Write a script which will create as many numbered directories as you want when you run it.

Solution
--------

The script (n-dirs.sh):

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
[user@host docs]$ chmod +x mid.sh
[user@host docs]$ ./mid.sh 5 8 cake.txt
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

