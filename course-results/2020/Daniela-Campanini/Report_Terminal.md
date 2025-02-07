## Report Unix Terminal & file formats

### Why do we use the terminal in bioinformatics?
With the Terminal several file types can be easily created, stored, accessed, analysed and reformatted to other file formats. 

### What is a plain text file? 
A plain text contains only characters, so no styles like fonts and bolds. 
The command-line and output text are for example given in plain text.

### In bioinformatics, most of the data are stored in plain text files with added syntax/structure (and commonly compressed afterwards). For instance, fasta or fastq files we have discussed them today, but also SAM, BED, GTF, VCF and others (to be discussed next week). Why is that? 
Plain text files are very useful, because they are universal and can be read by any ubiquitous text editor. 

### How can we list files are in a directory? Please provide the command(s).
To list the files in a directory, we have first to open the directory with the command line `cd \~directory` and then print the file-names in the directory with the command line "ls". Or also: `ls directory`. The command ‘ls -l’ gives more informations about the files (last modification date, access rights, file dimension and more)<br>
As example: <br>
`dacamp@DESKTOP-RBF9NBP:\~$ ls course/data` <br>
`dacamp@DESKTOP-RBF9NBP:\~$ ls \~/course/data` <br>
`dacamp@DESKTOP-RBF9NBP:\~$ cd \~/course/data | ls -l` <br>

### What | and > do in a terminal?
The pipe symbol “|” is used to take the output of the first command (at left side of “|”) and give it as input to the command on the right side of the pipe.<br>
a.g. `dacamp@DESKTOP-RBF9NBP:\~$ awk ‘NR % 4 == 2’ file_name.fq | wc -l` <br>(This command takes all sequence lines out of the FASTQ file and count the number of lines, which is the same as the number of sequences contained in the file)
<br><br> The symbol “>” is used to write and save the output of a command line into a text file.<br>
a.g. `dacamp@DESKTOP-RBF9NBP:\~$ awk ‘NR % 4 == 1’ SP1.fq > headers.txt` <br>(it takes the header line for all sequences in the FASTQ file and saves them in the text file named headers.txt)

### How do we print the last 10 lines of the file named /mnt/test/test.txt? Please provide the command(s).
`dacamp@DESKTOP-RBF9NBP:\~$ tail -n10 /mnt/test/test.txt`

### How do we print the first column of the file named /mnt/test/test.txt whose columns are separated by tabs? Please provide the command(s).
`dacamp@DESKTOP-RBF9NBP:\~$ awk ‘{print $1}’ /mnt/test/test.txt` (tabs are the default column separator)<br>
To work with text files we can use 'awk' to go trough the lines.

### How can we print every third line of a text file? Please provide the command(s), and discuss what they do.
`dacamp@DESKTOP-RBF9NBP:\~$ awk ‘NR % 3 == 0’ directory/name_file.txt` <br><br>
Each line number of name_file.txt gets divided by 3 (Text is composed of blocks of 3 lines). It will be checked if the rest of the division equals 0. If so, the line gets printed.

## How can we transform FASTQ into FASTA files using standard Unix tools (sed, awk, etc)? Please provide the command(s), and discuss what they do.
`dacamp@DESKTOP-RBF9NBP:\~$ awk ‘NR % 4 == 1 {print “>”$1}; NR % 4 == 2 {print}’ myFASTQ.fq | sed ’s/>@/>/g’ > myFASTA.fasta` <br><br>
FASTQ consists of a text of 4-lines blocks (header, sequence, + or comment, quality values). <br>
To work with the FASTQ lines we use the comand 'awk'. With 'awk' it is possible to go trough the lines. NR referse to the line number of all lines. With the statement `NR % 4 == 1` it chacked for which line number division by 4 gives the rest of 1. For all lines where it is true, the statement `{print ">"$1}` is carried out. It prints the header lines with in front of the line the symbol ‘>’. (In FASTA the header starts with ">")<br>
The Sequence line is the second line of the FASTQ blocks, it is found by `NR % 4 == 2' and printed with {print $1}`.<br>
The new header line and the sequence line are passed to the new command. ‘Sed’ exchanges all '>@' with '>'. It can be used here because we have no quality line (which can contain this symbols).
