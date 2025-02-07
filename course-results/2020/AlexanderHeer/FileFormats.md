# File Formats

### The reference genomes

* Not a file format or standard per se but the key for many of them as they need a reference to be aligned against
* Describe the "consensus" DNA
* Multiple assemblies have been released
* GRCh = "Genome Reference Consortium"
 * E.g. GRCh38.p13, where the p13 stands for the version of the reference, as older versions are still accesible
 * Due to convention, the numebring is gapped
* Mitochondrial genome is a special case due to its high variability
 * Makes it hard to find a usefull reference
* Collection of contigs/scaffolds
 * contig = strech of DNA seq encoded as A,G,C,T,N
 * Typically in FASTA format
 * ">" contains scaffold name, other lines are the seq

### Primary assembly
* best known assembly of a haploid genome
 * chromosome assembly
 * Unlocalized seq &#8594; associated to a chromosome but whose order/orientation is unknown
 * Unplaced sequence &#8594; not linekd to any chromosome 
 
### Alternate loci

* Alternate representation of a locus
 * usually highly polimorphic regions, e.g. MHC region
 
### Patches

* Contig seq released outside of the full assembly release
 * Fix/error correction
 * Novel/ne seq that will be included into the next full assembly release
 
### Reprodcability

There is a need for standardizing data analysis using reproducible workflows:
* Scripts for data retreival
* Keeping track of analysis steps
* Avoiding manual editing
* Data storage standards &#8594; Standardized **file formats**

**From slides (some info repeated):**
How do we do this in a reproducible manner?
* Scripting: We store an up-to-date reference genome in our
computer (once)
* use specific file standards to specify the genome annotation (i.e. GTF, BED files)

## alignments

* local alignments: identify regions of similarity within long sequences that are often widely divergent overall
 * often prefere but can be more dfficult to calculate (difficulty of identifying regions of similarity
* global alignments: global optimization that "forces" the alignment to span the entire length of all query sequences
* more info: https://www.majordifferences.com/2016/05/difference-between-global-and-local.html#.X3c6oGgzZnI
* Semi-global alignment: mix?

### Annotations
Genomic annotations are layers to genomic coordinates specifying their nature (e.g. exon, intron, untranslated region, open reading frame, ...). They are commonly stored in GFF or GTF files files


## Whih genomic file formats exist & what are thei use cases?
Access to the same data and tools is necessary but not enough: there is also a need for data standards

### Overview of common formats and their intended use
* Fasta and FastQ
* SAM/BAM (Alignments)
* BED (Genomic ranges)
* GFF/GTF (Gene annotation)
* BEDgraphs (Genomic ranges)
* Wiggle files, BEDgraphs and BigWigs (Genomic scores).
* Indexed BEDgraphs/Wiggles
* VCFs (variants)



### VCF Files


VCF stands for __Variant Call Format__. This text format is used for storing sequence variants (e.g. SNPs).
It consists of:
* meta information lines (starting with '##'):
  * a 'fileformat' filed is always required. It gives information on the version of the VCF format
  * Informationlines about the INFO, FILTER and FORMAT entries used in the body of the VCF file
  * Infomration on Date, source, reference sequence, etc.
* header line: Each header represents one column in the VCF. There are 8 fixed, mandatory columns:
  * #CHROM : identifier from the reference genome
  * POS: reference position, with the 1st base having position 1
  * ID: semi-colon separated list of unique identifiers where available
  * REF: reference base(s)
  * ALT: comma separated list of alternate non-reference alleles called on at least one of the samples
  * QUAL: phred-scaled quality score for the assertion made in ALT
  * FILTER: PASS if this position has passed all filters, i.e. a call is made at this position. Otherwise, if the site has not passed all filters, a semicolon-separated list of codes for filters that fai
  * INFO: additional information
* data line: Each of these lines contains information (see header) about a position in the genome.

The advantage using the VCF format is that only variations have to be stored together with a reference sequence.
Therefore, it is one of the most commonly used file format when studying genetic variants.


### HGVS-nomenclature
The HGVS is used to report and exchange information  about variants in DNA, RNA and protein sequences. It is authorised by the Human Genome Variation Society (HGVS), Human Variome Project (HVP) and the HUman Genome Organization (HUGO) and serves an an international standard. The extensive nomenclature defines the basic variant types as stricly as possible to enhance clarity and facilitate computational analysis and descrition of the sequence variants. Detailed information on the nomenclature and its definitions can be found in [Dunnen et al.(2016)](https://onlinelibrary.wiley.com/doi/full/10.1002/humu.22981).

From slides:
It allows the annotation of sequence variants of DNA, RNA & proteins with relation to a genomic ("g") or protein ("c") reference

### BEDTools

In genomics it is a fundamental task to deternmine wether distinct sets of genomic features (e.g. aligned seq reads, gene annotation, ESTs, genetic polymorphisms, mobile elements, etc.) overlap or are associated with one another. 
Genomic features are often represented by Browser Extensible Data (BED, below) or General Feature Format (GFF, below). Comparisons are often performed using the UCSC Genome Browser (among others). While these tools are conveniant and reliable, they need an interaction with a remote or local web site installation. Thus, they are not amenable to large datasets. BedTools was developed to adrress the need for fatser and more felxible tools to conduct a greater number and more diverse set of experiments. 

Possible problem that can be approached:
if genomic features of two distinct sets share at least one base pair they are defined as *intersecting* or *overlapping*, thereofre a typical question would be ‘Which of my novel genetic variants overlap with exons?’. 
 &#8594; BEDTools efficiently addresses such questions without requiring an installation of the UCSC or Galaxy browsers
 
Advantages:
* Can read data from standard input and write to standard output
 * Allows complex set operatins to be perfomred (combination of operations form BEDTools among each other and with UNIX utilities)
* Most tools distinguish DNA strands when searching for overlaps
 * Allows orientaton to be considered when interpreting paired-end mapping or RNA-seq data
* Mitigates the need to interact with local or public instances of the UCSC Genome Browser or Galaxy
 * Avoinding a major bottleneck when working with large genomics datasets
* Speed and functionallity allow greater flexibility in defining and refinig genomic comparisons access to the same data and tools is not enough: the
need for data standards
Izaskun
 * Allows for diverse and complex comparisons between ever-larger genomic datasets


#### BED

* Browser Extensible Data
* provides flexible way to define data lines that are displayed in an annotation track
* BED lines have three required fields and nine additional options:
 * **chrom** : name of the chromosome or scaffold
 * **chromStat** : starting position of the feature in the chromosome scaffold
  * First base is numbered 0
 * **chromEnd** : ending posiiton of the feature in th chromosome or scaffold. chromEnd base is not included in the display of the feature BUT the numebr in posiiton format will be represented 
 * name, score, strand, thickStart, thickEnd, itemRgb, blockCount (exons), blockSize, blockStarts
* Number of fields has to be consistent throughout any single set of data in an annotation track
* order of the optional fields is binding &#8594; lower fields must be populated if higher fields are used
* If field content has to be empty: "."
* BED fields in custom tracks can be whitespace-delimited or tab-delimited

Formating compared to UCSC Genome Browser (web interface):
 
BED | UCSC
--- | ---
"0-start, half-open” system | "1-start, fully-closed" system (as coordinates are “positioned” in the browser)
Written as Written as: chr1 127140000 127140001: <ul><li>Spaces between chromosome, start coordinate, and end coordinate</li><li>no punctuation</li></ul> | Written as: chr1:127140001-127140001<ul><li>No spaces</li><li>Includes punctuation: a colon after the chromosome, and a dash between the start and end coordinates</li></ul>
More efficient method | Needs one more step in the calculation but is more intuitive
Used for database tables in UCSC | Used in the UCSC web browser to be more humanly readable

From slides:
* BED files are simpler data representations, usually the next
step after getting the SAM files
 * smaller and essier to handle
* Come in different flavors:
 * **BED3:** 3 tab separated columns, chromosome (scaffold), start, end
 * **BED6:** BED3 plus name, score, strand
 * **BED12**

 
#### BEDgraph
* To display continuous-valued data in track format
* useful for probability scores
* Advantages: the coordinates are specied, so sparsity is
allowed
*

#### GFF 

* Originally for the intechange of time-series data between analysis systems
* Extended for storage of processed acoustic data, nonacoustic dasa & event data
* Employs the chunk concept to provide extendability while providing a measure of backwards compatibility
* Includes .txt, .csv, .doc, .pdf, .jp[e]g, .png, ... (?)

#### GFF3

* Generic Feature Format Version 3
* addresses the most common extensions to GFF, while preserving backward compatibility with previous formats
* Adds a mechanism for representing more than one level of hierarchical grouping of features and subfeatures
* Separates the ideas of group membership and feature name/id
* Constrains the feature type field to be taken from a controlled vocabulary
* Allows a single feature, such as an exon, to belong to more than one group at a time
* Provides an explicit convention for pairwise alignments
* Provides an explicit convention for features that occupy disjunct regions
* tab-delimited
* plain text file
* use of UTF-8 recomended 
* nine-columns
 * seqiq
 * source 
 * type
 * start
 * end
 * score
 * strand
 * phase
 * attributes
* tab (%09)
* newline (%0A)
* carriage return (%0D)
* % percent (%25)
* control characters (%00 through %1F, %7F)
* reversed meaning in column 9:
 * ; semicolon (%3B)
 * = equals (%3D)
 * & ampersand (%26)
 * , comma (%2C)

#### GTF
Stands for gene transfer format. It is a format used to hold information about gene structure. It is a tab-delimited text format based on the general feature format (GFF), but contains some additional conventions specific to gene information


### SAM & BAM

#### SAM

SAM stands for __Sequence Alignment Map__ and is a tab-delimited text format. 
It is commonly used to store nucleotide sequences, generated by next generation sequencing technologies.
Most often it is generated as a human readable version of its sister BAM format.
The format can store short as well as long reads, making it more versatile.

SAM files consists of:
* header section: must be prior to alignments and starts with @
* alignment section: contains 11 mandatoory fields s for
essential alignment information:
  * QNAME: Query template name. Reads/segments having identical QNAME are regarded to come from
the same template
  * FLAG: combination of bitwise flags &#8594; [detailed info](https://samtools.github.io/hts-specs/SAMv1.pdf)
  * RNAME: Reference sequence name of the alignment
  * POS: 1-based leftmost mapping Position of the first CIGAR operation that “consumes” a reference
base  &#8594; [detailed info](https://samtools.github.io/hts-specs/SAMv1.pdf)
  * MAPQ: Mapping Quality
  * CIGAR: CIGAR string  &#8594; [detailed info](https://samtools.github.io/hts-specs/SAMv1.pdf)
  * RNEXT:  Reference sequence name of the primary alignment of the next read in the template
  * PNEXT:  1-based Position of the primary alignment of the next read in the template
  * TLEN:  signed observed Template length
  * SEQ: segment sequence
  * QUAL: Quality score, phred-scaled

More info: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2723002/
#### BAM

BAM stands for __Binary Alignment Map__. It contains the same information as a SAM file but as binary infomration.
Due to its binary fomrat it is used when working on the file on computer while the SAM format is there to make the file readable for us.


### CRAM

Like BAM files, CRAM files are compressed alignment files. It was designed as an efficient refernce-based alternative to SAM and BAM files. Due to the improved compression of CRAM files, they are between 30% to 60% smaller than BAM files (depends on the data), thus reducing storage costs.


### FASTA & FASTQ


#### FASTA
 The FASTA format is a text-based format for representing either nucleotide or
amino acid sequences using single-letter codes (standard IUB/IUPA amino acid and nucleic acid codes, with a few [exceptions](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=BlastHelp)) for **nucleotides** or amino acid codes. The sequences are **not aligned** to a reference sequecne as in other formats. Blank lines are not allowed in the middle of FASTA input. A FASTA file is structured as follows:
* Begins with a single-line descrition, the **defline**
 * distinguished from sequences by the '>' symbol
 * usualy with uinque Sequence ID
* Followed by lines of sequence data

Compared to other file formats the FASTA fomrat is simple and easily readable, making it easy to maipulate and parse sequences using text-processing tools and scripting languages. The trade-off for its simplicity is that it contains less information than other formats and it is not optimised for size

#### FASTQ
The FASTQ file format can be looked at as an extension to the FASTAn format. Additionally to the same information of a FASTA file, it also includes a quality score (Phred) for each base, represented as a ASCII character. A problem with the format is, that it is not standardized. This means that different variants are in common use, which are not possible to reliably automatically be destinguished. NEvertheless it has become the de facto standard for storing high throughput sequening instrument (e.g. Illumina Genome Analyzer) outputs.

Sequencing short reads is common practice. We get hundereds of millions of reads and instead of assembling them, we align them to a reference. Sequencers provide sequence and error rates assessment, therefore thefasta format is not suitable, but fastq is
 &#8594; Standard de facto for short read, high-throughput sequencing instruments such (i.e. Illumina)
 
From slides:
Plain text files with chunks of four lines:
* @ identifier line
* Sequence
* "+" (sometimes the sequence name, again)
* Quality scores (diferent encodings exist)
 
##### Phred

* The sequencing quality score of a given base Q is defined by as Q = -10 log10 P
* Logaritimically linked to error probabilities
 * score of 10 = 90% base call accuracy
 * score of 20 = 99% base call accuracy
 * score of 30 = 99.9% base call accuracy
 * score of 40 = 99.99% base call accuracy
 * ...
 




### MPEG-G
MPEG-G stands for Moving Picture Experts Group and is a project that by proiding new compression and transport technologies and a family if standard specifications which aims to efficiently process, transport and share large scale genomic data. The possibility to implement leading-edge compression technology that can achieve an improvement of more than 10x over the BAM format. A more detailed introduction to MPEG-G can be found in the paper of [Alberti et al. (2018)](https://www.biorxiv.org/content/10.1101/426353v1).

### ISCN

* Stands for International System for Human Cytogenetic Nomenclature
* Annotation format for chromosomal aberrations
 * i.e. traditional microscopically visible structrual and quantitative abnormalities in karyotypes
* Extension for "molecular cytogenetics" 
 * e.g. M-FISH, SKY, genomic arrays
 * Aims to prevent confusion in reporting research cytogenetic results. 
 
 ### dbVar
 
 * NCBI's database of human genomic structural variation
  * idels
  * dulpications
  * inversions
  * mobile elements
  * translocations
 * structural genome variations are still not completely solved with respect to unambiguous annotation
 
### Sequence Ontology (SO)

* describes types of biological sequence alterations (or normal status)
* by itslef not suitable for complete variant description
 * e.g. lacking the localisation &#8594; has to be attached to a sequence or functional element
 
 
### GA4GH Transitional model

* object model for the representation of genomic variants in the context of an experimental read-out (callset)
* based on VCF principles 
* allows to place variants into intervals with "fuzzy ends"
not yet suitable for genotype reconstruction 
* https://schemablocks.org/schemas/blocks/Variant.html

### Wig files
* To display continuos-value data
* GC percent, probability scores, and transcriptome data.
* Data is not sparse! Wiggle data elements must be equally sized (step)
* Basic Wig file: specifies the chromosome (once), the nucleotide, and the score.
* Improved Wig: add the span if the score applies to several nucleotides
* Improved Wig: how to represent the scores of 300 nucleotides from chr3, starting from 400601, where the first 100 nt are scored 11, the next 100 nt 22, and the last 33?

General structure:
Wiggle format is line-oriented. For wiggle custom tracks, the first line must be a track definition line (i.e., track type=wiggle_0), which designates the track as a wiggle track and adds a number of options for controlling the default display.

Wiggle format is composed of declaration lines and data lines, and require a separate wiggle track definition line. There are two options for formatting wiggle data: variableStep and fixedStep. These formats were developed to allow the file to be written as compactly as possible.


Data values:
Wiggle track data values can be integer or real, positive or negative values. Only positions specified have data. Positions not specified do not have data and will not be graphed. All positions specified in the input data must be in numerical order. NaN values are not supported by the browser and, if included, may have unforeseen effects.
