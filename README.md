IMAP
====================
Chromosome-level genome assembler combining multiple de novo assemblies


System requirements
-------------------
* Linux x64
* Perl >= 5.8.x or new
* Perl modules
  - Switch
  - Parallel::ForkManager
  - Bio::TreeIO
* System libraries
  - BOOST >= 1.46.0
  - zlib
  - libbz2
  - libncurses

Download source
-------------------
    git clone https://github.com/jkimlab/IMAP.git


Installing IMAP
-------------------
To install IMAP,
 
    1. Check & install the required perl libraries
      - Check the required perl libraries
        ./build.pl --check
    
      - Install the required perl libraries
    
    2. Install IMAP package
        ./build.pl --install
        
To uninstall IMAP,

        ./build.pl --uninstall


Running IMAP with example dataset
-------------------
        ./build.pl --example
        cd IMAP_EX
        bash CMD

Running IMAP
-------------------
To run IMAP, you need to prepare a parameter file. 

* parameter file

    You can use multiple sequencing read libraries, and one or more outgroup species.  
        
       ############################################################
       ## Sequencing read library information
       ############################################################
       ### Average insert sizes
       ### Standard deviation of insert sizes
       ### Path of read files (.fq(.gz))
       ##### [Paired-end reads] p1, p2
       ##### [Mate-pair reads] m1, m2
       [LIB]
       insertSize	[(integer) insert size]
       insertSizeSD	[(integer) SD of insert size]
       p1	path of forward read          (ex. [path]/read1.1.fq)
       p2	path of reverse read          (ex. [path]/read1.2.fq)
       p1	path of forward read          (ex. [path]/read2.1.fq)
       p2	path of reverse read          (ex. [path]/read2.2.fq)

       [LIB]
       insertSize	[(integer) insert size]
       insertSizeSD	[(integer) SD of insert size]
       m1	path of forward read          (ex. [path]/read3.1.fq.gz)
       m2	path of reverse read          (ex. [path]/read3.2.fq.gz)

       ############################################################
       ## General assembly parameters
       ############################################################
       ## Minimum length of contigs
       MinContigLength	[(integer) minimum length of contigs]
       ## Kmer size for de novo assembly
       Kmer	[(integer) kmer]
       ### Maximum read length for SOAPdenovo2
       MaxReadLength	[(integer) maximum read length]

       ############################################################
       ## RACA & DESCHRAMBLER parameters
       ############################################################
       ## You can use the outrgroup more than one, but the names must be different.
       Reference	[(string) name]	[path of sequence file (.fa)]          (ex. S288C  [path]/S288C.fa)
       Outgroup	[(string) name]	[path of sequence file (.fa)]          (ex. dairenensis [path]/Saccharomyces_dairenensis.fa)
       ### Tree must contain the names of a reference, target(s) and outgroup(s) (newick format)
       TREE	[path of tree (must be in newick format)]          (ex. [path]/tree.nwk)
       ### Synteny resolution
       Resolution	[(integer) synteny resolution]

       ############################################################
       ## Error correction parameters 
       ############################################################
       IterationNumber	[(integer) the number of iteration]


Then, you can use the 'IMAP' perl script.

    Usage:  ./IMAP.pl -t [threads] -p [parameter file] -o [out directory]

    Options:
        --threads|-t <integer> Number of threads (default: 1)
        --params|-p <filename> Parameter file
        --outdir|-o <filename> Output directory (default: ./IMAP_RESULT)
        --help|-h Print usages
        
    Simple examples:
        ./IMAP.pl -t 40 -p param.txt -o ./IMAP_RESULT
         
Included third party tools
-------------------
* BWA (http://bio-bwa.sourceforge.net/)
* LASTZ (http://www.bx.psu.edu/~rsharris/lastz/)
* MaSuRCA (http://www.genome.umd.edu/masurca.html)
* SPAdes (http://bioinf.spbau.ru/spades)
* SOAPdenovo2 (https://github.com/aquaskyline/SOAPdenovo2)
* GapCloser (http://soap.genomics.org.cn/soapdenovo.html)
* RACA (https://github.com/ma-compbio/RACA)
* DESCHRAMBLER (https://github.com/jkimlab/DESCHRAMBLER)
* Pilon (https://github.com/broadinstitute/pilon)
* GATK (https://software.broadinstitute.org/gatk/)
* Picard (https://github.com/broadinstitute/picard)
* SAMtools (http://samtools.sourceforge.net/)
* Kent utilities (http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/)


Contact
-------------------  
bioinfolabkr@gmail.com
