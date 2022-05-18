1. Introduction to Linux
1.1. Data setup and naviguation
1.    Type the following command to get your working directory

pwd
2.    Create a directory called data

mkdir data
3.    The files for this tutorial are located in /EpiCass_workshop/day1/data,  list (ls) the elements in the specific path to see them/it:
ls /EpiCass_workshop/day1/data
4.    Copy (cp) the file to your home directory (~/)

cp /EpiCass_workshop/day1/data/day1.tgz ~/
5.    Move the file to the data directory

mv day1.tgz data/
6.    Change from your current working directory to the directory you have created in point 2

cd data/
7.    Get the path to your new working directory and the list of files in your current directory (2 different commands)

8.    Extract all the files used in this tutorial from the zip archive

tar -xzvf day1.tgz
9. List the files in your current directory.

10. Go in the UNIX directory

 List, permission, manual and preview of content
8.     Check the permissions of the files using

ls -l
9.    change the permissions on the files using:

chmod 700
What do you see if you use ls -l ?

10.  repeat the command with 755 – what do you see if you use a ls-l, any differences?

12.  Check the size of the file using the human-readable parameter

ls -lh
If you do not know a parameter you can use one of the following to have more information about a command

man ls
ls --help
13.  View the contents of both the files using the head and tail commands

head FILE
tail FILE

 Piping and Word count
Instead of printing the result of head and tail to your screen you can use a pipe ( | ) to redirect the output in another command.

14.  Pipe the output of the head and tail command to the wc -l command, how many lines do you count?

wc -l is the wordcount command using the line parameter

head file | wc -l
tail file | wc -l
15.  Repeat the head and tail command, but use the -n parameter set to 15 and then repeat the pipe in wc -l

head -n 15 file
tail -n 15 file | wc -l

There is many methods to see a complete file, whether you print it to your screen (cat), you open a software that display a file one page at a time (less, more).

16.  View the file called PlasmoDB-9.0_Pfalciparum_BarcodeIsolates.fasta using the cat command, the more command and the less command. To quit less and more press the letter Q

17.  Use the wc -l command to count how many lines both the files contain in total

18.  Use the grep command to print out the fasta headers from both files to the screen

Reminder the fasta header always start with > so you can use this symbol as your filter in grep

grep ">" FILE
19.  Use the grep -c parameter to count the number of fasta headers (and by extension the number of sequences) in both files.

 Sort, Uniq and redirected output
20.  Repeat question 18 and send the output to a file called fasta_headers

To redirect the output that appear on your screen (stdout) to a file you can use the > symbol followed by the name of the file you will create

grep ">" FILE > fasta_headers
You can  also append the information on the bottom of a file using >> ( just one bigger than will erase the existing file replacing the content with the new output while the double bigger than will append in the end of the file)
21.  Count the number of lines in the new file called fasta_headers

22.  Use the sort on the file called fasta_headers

sort fasta_headers
23.  Pipe the output of the sort command the uniq command

sort fasta_headers | uniq
24.  Type the command history to see the list of commands you have used

history
25. Redirect the output of the history command to a new file called practical_1_commands.txt

history > practical_1_commands.txt
26.  Look at the contents of the file practical_1_commands.txt using the less command

Introduction to SED
Instructions:

Change the directory to Epicass_workshop/Day1 which contains the files for the sed tutorial.
They are called sed_practical, awk_practical, bash_practical

File content and odd line retrieval
1.Type sed on the command line and look at the options provided. What option is required to obtain the sed version number?

2. Inspect the file called exercises.fasta using less. How many sequences with fasta headers are in the exercises.fa file?

3. Examine the sequences.fasta file – what do you notice

a. Are all the sequence characters the same case? 

b. The sequence characters are in a mixture of cases? 

 

4. From examining the sequences.fasta file, we know that each fasta header and sequence sit on a new line, with the fasta headers being on odd numbered lines. Let us try and print out the fasta header lines only using sed:


5.What command would you use to print out only the even number lines with the actual sequence? 

 Pattern modification and global and piping
6.  Change the character cases to make them uppercase using sed

 

7. Not all the characters were changed to upper case – what would I need to add to the sed command to change everything to upper case?


8. Look at the gene.gff file copied to the sed_practical directory

a. How many entries / lines are there? 

 

9. Convert the pattern chrm to Chromosome in the genes.gff file 

 

10. Convert the gene.gff file into a comma separated file:

 

11. The command above only worked for the first tab character (if you didn’t use the global flag). Use the global flag (g):


12. From the sequences.fasta file, add the organism p_falciprium to the start of the fasta headers:

 

13. For the command above,don’t use the global flag. Are all the fasta sequence headers modified, if so why?

14.Change all the characters in the sequences.fasta file to upper case and add p_falciprium to the start of the fasta headers and then convert the uppercase fasta headers to lowercase using a series of sed pipes:

 

15. What would you need to do to the above command to send the output into a new file?

 

16. Using the genes.gff file, print out only lines 1, 3 to 5, 7 and 9:

Reformating BED files
17. Use the exercises.bed for this next set of exercises. Inspect the bed file:

 

18. How many lines / rows are in the exercises.bed file?

 

19. For questions 19 to 22, pipe the output to less. Using sed, substitute the all the terms contig- with contig_ in the exercises.bed file using the global flag

 

20. Using sed, substitute gene- with Gene_ in the exercises.bed file using the global flag

 

21.Using sed, substitute the term repeat with REPEAT in the exercises.bed file using the global flag


22. Repeat questions 21, 22, and 23, but without using the global flag substitution flag.

 

23.  Is there a difference between using the global substitution flag Yes / No?

 

24.  What would the explanation be?

 

25. Combine sed pipes to substitute contig- with contig_ gene- with gene_ and repeat with REPEAT and pipe the output to less to check if the substitutions are working


26. Once you are happy that your sed command is working, send the output to a file called formatted_exercises.bed

Check if awk is installed by typing awk and should get some output about options and usage on the screen.
Have a quick look at the files copied into the awk directory, they should be familiar from the sed practical.
They both seem to have a table type of structure with rows and columns.
Visualisation, filters and calculations
1. Using awk, print out the first column of the genes.gff file:

 

2. Print out column 9 of the genes.gff file using awk:

  

4. Change the awk command slightly to take into account a default delimiter, a \t in this case

 

5. How many columns are in the dataset genes.gff, use the awk NF function

 

6.Do you get the differences between 8 to 10 columns which is not correct as a general feature format file should have 9 columns that should be split by tabs (see the url below for an explanation of a gff file: https://www.ensembl.org/info/website/upload/gff.html Try again to the get the correct number of fields by splitting on the correct delimiter which is tab-seperated. Just in case you never used “\t” for the previous question. 


 

7.  Find out how many unique chromosomes are contained in our gene.gff file using awk and sort:

 

8. Extract columns 1, 3, 6 and 9 from the genes.gff file while keeping the formatting


9. Use awk’s BEGIN and OFS functions to get the output in tab delimited format of columns 1,3,6 and 9:

 

10.Extract all genes that map to chromosome 1 within the genes.gff file and redirect it to a file named chromosome_1_genes.gff

 

11. Filter the genes.gff file to get all entries with chromosome 1 and annotations as genes using the && operator:

 

12.  Print out a specific column using the filtering criteria above e.g. column 9

 

13. Pull out all the rows where the column is equal to chromosome 1, or the column 3 is equal to a gene using the || operator


14. modify the previous awk construct to also filter on numerical values

 

15.change the values in the source field to H_sapiens and print out a new gff file using awk

 

16. Using awk, get the length of repeats from genes.gff file keeping in mind the offset +1

 

17. get the total length of repeats from the genes.gff file

 

18. calculate the mean of the scores in the gene.gff file using a count as well

 

19. Extract all genes that map to chromosome 2 within the genes.gff file

 

20. Print out columns 1, 2, 4 and 8 using awk and insert a tab delimiter

 

21. Sum up the total length of genes in the genes.gff file

 

22.  Calculate the mean gene length in the genes.gff file using awk 

23. Find all the entries labelled as gene in column 3 and have a score greater than 0.55 in column

Here you find additional resources to train your skills in UNIX

UNIX for genomics:

https://datacarpentry.org/shell-genomics/

A broader UNIX tutorial:
https://swcarpentry.github.io/shell-novice/

Some useful Unix commands Command and What it does
Command	What it does
ls	Lists the contents of the current directory
mkdir	Creates a new directory
mv	Moves or renames a file
cp	Copies a file
rm	Removes a file
cat	Concatenates files
less	Displays the contents of a file one page at a time
head	Displays the first ten lines of a file
tail	Displays the last ten lines of a file
cd	Changes current working directory
pwd	Prints working directory
find	Finds files matching an expression
grep	Searches a file for patterns
wc	Counts the lines, words, characters, and bytes in a file
kill	Stops a process
jobs	Lists the processes that are running  

reference of concepts and commands seen during the lesson.

shell commands explained - a website that shows the help text of any command
awesome bash - an awesome list of resources about the bash shell
tldp - the Linux documentation project (the books can be hard to digest but are very thorough)



