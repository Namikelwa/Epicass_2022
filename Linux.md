 # Introduction to Linux
 ## Data setup and navigation
 Type the following command to get your working directory
``` 
 pwd
```
Create a directory called data
```
mkdir data
```
The files for this tutorial are located in /EpiCass_workshop/day1/data,  list (ls) the elements in the specific path to see them/it:
```
ls /EpiCass_workshop/day1/data
```
Copy (cp) the file to your home directory (~/)
```
cp /EpiCass_workshop/day1/data/day1.tgz ~/
```
Move the file to the data directory
```
mv day1.tgz data/
```
Change from your current working directory to the directory you have created in point 2
```
cd data/
```
Get the path to your new working directory and the list of files in your current directory (2 different commands)

Extract all the files used in this tutorial from the zip archive
```
tar -xzvf day1.tgz
```
List the files in your current directory.

Go in the UNIX directory

List, permission, manual and preview of content

Check the permissions of the files using
```
ls -l
```
change the permissions on the files using:
```
chmod 700
```
What do you see if you use ls -l ?

repeat the command with 755 – what do you see if you use a ls-l, any differences?

Check the size of the file using the human-readable parameter
```
ls -lh
```
If you do not know a parameter you can use one of the following to have more information about a command
```
man ls
ls --help
```
View the contents of both the files using the head and tail commands
```
head FILE
tail FILE
```
Piping and Word count
Instead of printing the result of head and tail to your screen you can use a pipe ( | ) to redirect the output in another command.

Pipe the output of the head and tail command to the wc -l command, how many lines do you count?

wc -l is the wordcount command using the line parameter

```
head file | wc -l
tail file | wc -l
```
Repeat the head and tail command, but use the -n parameter set to 15 and then repeat the pipe in wc -l
```
head -n 15 file
tail -n 15 file | wc -l
```
There is many methods to see a complete file, whether you print it to your screen (cat), you open a software that display a file one page at a time (less, more).

View the file called PlasmoDB-9.0_Pfalciparum_BarcodeIsolates.fasta using the cat command, the more command and the less command. To quit less and more press the letter Q

Use the wc -l command to count how many lines both the files contain in total

Use the grep command to print out the fasta headers from both files to the screen

Reminder the fasta header always start with > so you can use this symbol as your filter in grep
```
grep ">" FILE
```
Use the grep -c parameter to count the number of fasta headers (and by extension the number of sequences) in both files.

Sort, Uniq and redirected output

Repeat question 18 and send the output to a file called fasta_headers

To redirect the output that appear on your screen (stdout) to a file you can use the > symbol followed by the name of the file you will create
```
grep ">" FILE > fasta_headers
```
You can  also append the information on the bottom of a file using >> ( just one bigger than will erase the existing file replacing the content with the new output while the double bigger than will append in the end of the file)

Count the number of lines in the new file called fasta_headers

Use the sort on the file called fasta_headers

```
sort fasta_headers
```

Pipe the output of the sort command the uniq command
```
sort fasta_headers | uniq
```
Type the command history to see the list of commands you have used

history
Redirect the output of the history command to a new file called practical_1_commands.txt
```
history > practical_1_commands.txt
```
Look at the contents of the file practical_1_commands.txt using the less command



**Some useful Unix commands Command and What it does**

Command |	What it does
---------  --------------
ls |	Lists the contents of the current directory
mkdir |	Creates a new directory
mv |	Moves or renames a file
cp |	Copies a file
rm |	Removes a file
cat |	Concatenates files
less |	Displays the contents of a file one page at a time
head |	Displays the first ten lines of a file
tail |	Displays the last ten lines of a file
cd |	Changes current working directory
pwd |	Prints working directory
find |	Finds files matching an expression
grep |	Searches a file for patterns
wc |	Counts the lines, words, characters, and bytes in a file
kill |	Stops a process
jobs |	Lists the processes that are running  


*reference of concepts and commands seen during the lesson.

shell commands explained - a website that shows the help text of any command
awesome bash - an awesome list of resources about the bash shell
tldp - the Linux documentation project (the books can be hard to digest but are very thorough)


Here you find additional resources to train your skills in UNIX

UNIX for genomics:

https://datacarpentry.org/shell-genomics/

A broader UNIX tutorial:
https://swcarpentry.github.io/shell-novice/
