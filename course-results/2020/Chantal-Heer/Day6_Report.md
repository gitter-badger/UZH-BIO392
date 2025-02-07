# Report  
* Which are the advantageous of BED/coordinate files as compared to storing just sequences?  
> BED files are simpler data representations. They are smaller and easier to handle. All the information (when not even more) of a FASTA file is stored in only one line per sequence.
* Which QC values are tracked during a bioinformatic variant calling NGS workflow? (from sequencing to variant calling)?     
> QC values stand for quality control values. We have QC values for read quality, mapping quality and variant calling quality.   

We'd like to store the following information. You can decide to encode them counting by 0,1 and closed/open at your convenience (but please specify).  
> I use 0-based and half-open. This is the encoding normally used for BED format files.  

We have 3 genomic intervalls. All intervalls are 1'000 nt long. They are continguous (head to tail). All in the plus strand. The first one starts (we'd like to include the start nucleotide too) in position 1'000 of chr2. We don't have reads nor alignments, just scores (integers). Intervals A and B have score of 0 and interval C has a score of 1'000.  
* Can we store this in SAM file? Why / why not?  
> We can't store this information because the sequences are available as scores. The SAM file format stores the sequences information as alignment to the reference genome. 
* Can we store this in a BED3? How (please write down the BED file)? Are we losing any information?  
> The information can be stored in a BED3 file. However, we lose some informtaion (BED3 has only three columns).  
>
>     chr2  1000   1999       
>     chr2  2000   2999  
>     chr2  3000   3999
* And in BED6? How? Are we losing any information?  
> The BED6 format with six column is a good way to store all our information. We will lost nothing.  
>
>     chr2  1000   1999   A      0   +  
>     chr2  2000   2999   B      0   +  
>     chr2  3000   3999   C   1000   +
* And in BED12? How? Are we losing any information?  
> The storage of the information in a BED12 file (twelve columns) would be useless. We only have information for the first six columns, like a BED6 file. When we would use a BED12 file the last six columns would be empty. However, we would not lost any information.  
>
>     chr2  1000   1999   A      0   +    .   .   .   .   .   .  
>     chr2  2000   2999   B      0   +    .   .   .   .   .   .  
>     chr2  3000   3999   C   1000   +    .   .   .   .   .   . 
* And in the most compact Wiggle as possible? How? Are we losing any information?  
> We can store the information also in a Wig file (Wiggle) but we will lost the information about the strand.   
>
>     fixedStep   chrom=2   start=1000    step=1000   span=1000  
>        0  
>        0  
>     1000
