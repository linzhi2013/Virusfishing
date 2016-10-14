Virusfishing version 1.0 (201604)

###1. DESCRIPTION

Virusfishing is a virus screening pipeline for 1000 Insect Transcriptome Evolution (1KITE) project to search viruses, construct viral genomes and screen for the expressed virus genes and discover viral splicing patterns. Virusfishing also can be used in other next generation sequencing data. 

Include 3 steps: 

1. **Search**:   search known virus sequences from assembly
2. **Assemble**: do virus assembly based on reference
3. **Splicing**: identify splicing pattern of assembly

###2. DOWNLOAD
Virusfishing version 1.0 201604

###3. INSTALLATION
`tar -zxvf Virusfishing.V1.0.tar.gz`

###4. Source code
####Wrappper script

**`Virusfishing.py`**: the wrapper script to run other Perl scripts to do the work you choose.

Eight Perl scripts in folder `Virusfishing.V1.0/bin/`, including:
####Search known virus:
`Virus_Search.pl`: search viruses in assemblies     
`Virus_false_removal.pl`: removal false positive according to the taxonomy   

####Assemble viral gnome:
`Ref_Based_Genome_Assemble.pl`: assemble viral genomes based on viral reference    
`fq2fa.pl`: change fastq files into fasta files
		
####Detect splicing junctions:
`Splicing_Search.pl`: find introns and exon-exon splice junctions from the clean alignments and give out summaries

####Summarize:
`Virus_Coverage.pl`: obtain the best-hit related sequences, and calculate the coverage of assembled sequences and viral sequences from the blast results.     
`Alignmentout_Sum.pl`: filter multiple alignment file (support sam, bam, soap or map type) and make a summary for it.
		
####Classify:
`Find_NCBItax_from_name.pl`: obtain the NCBI classification

###5. Pre-requisites
####Software
You need to install following programs and add the software directories to your `$PATH`:
	
	export PATH=:$PATH:$softwaredir # for sh or bash users
	setenv PATH .:$PATH:$softwaredir # for csh users

| softwares | URL |
|----------- | --- |
| Blastall 2.2.26 | ftp://ftp.ncbi.nih.gov/blast/executables/blast+/2.2.26 |
| BWA 0.7.10 | http://bio-bwa.sourceforge.net |
| Bowtie2 (bowtie2-2.1.0 or higher) | https://sourceforge.net/projects/bowtie-bio/files/bowtie2/ |
| TopHat2 (tophat-2.0.7 or higher) | http://ccb.jhu.edu/software/tophat/index.shtml |
| SAMtools-0.1.19 (include vcfutils.pl & bcftools) | https://sourceforge.net/projects/samtools/files/samtools/0.1.19/ |
| RefTools | https://github.com/BGI-shenzhen/Reseqtools |
| Python version 3 or higher | www.python.org |

####Library
You need to install following libraries directories to your `$LD_LIBRARY_PATH`: `export LD_LIBRARY_PATH=.:$boostdir`

| library | URL |
| -------- | --- |
| Boost | www.boost.org/ |
| PerlIO::gzip |http://search.cpan.org/~nwclark/PerlIO-gzip-0.19/gzip.pm |
|ParseFasta.pm & ParseFastq.pm | (already in `Virusfishing.V1.0/lib/`) |

####Database
1. **Virus database**

	`ftp://ftp.ncbi.nih.gov/blast/db/FASTA/`   
	Or NCBI viral gene annotation    
	`ftp://ftp.ncbi.nih.gov/refseq/release/viral/`   
	Or Your own virus database
2. **Nt database**
	
	`ftp://ftp.ncbi.nih.gov/blast/db/FASTA/`   
	If Nt database is too large for you, you can do the 2nd blastn in step 1 and step 2 online (`https://blast.ncbi.nlm.nih.gov/Blast.cgi`)
	
3. **Taxonomy database**   
	(gi_taxid_nucl.dmp.gz, names.dmp & nodes.dmp)   
	`ftp://ftp.ncbi.nih.gov/pub/taxonomy/taxdump.tar.gz`  
	`ftp://ftp.ncbi.nih.gov/pub/taxonomy/gi_taxid_nucl.dmp.gz`   
*Note*: Creat symbolic links for databases in `/Virusfishing.V1.0/database`, 
	so that you can use the default parameter in some steps:
	`ln -s /dir/names.dmp /Virusfishing.V1.0/database/tax/names.dmp`

###6. EXAMPLES
Virus search: 
	
	python Virusfishing.V1.0/Virusfishing.py search 

Viral genome assemble:
	
	python Virusfishing.V1.0/Virusfishing.py assemble

Splice junction detection using raw data:
	
	python Virusfishing.V1.0/Virusfishing.py splicing

Only create a shell script for summarizing the alignment file:
	
	perl Virusfishing.V1.0/bin/Alignmentout_Stat.pl -in in.map -ref ref.fa -type map
	
Virus search without a NT database:
	
	perl Virusfishing.V1.0/bin/Virus_Search.pl -i assemble.fa -v virus.db -outpre candidateviral
	
Then, use the candidate viral sequences to blastn against NT database online

###7. CONTRIBUTORS
Chengran Zhou; Guanliang Meng; Songwen Hui; Jinmin Ma

###8. CONTACT US
Email:    
zhouchengran at genomics dot cn   
mengguanliang at genomics dot cn   
songwenhui at genomics dot cn   
majinmin at genomics dot cn

###9. CITATION
Chengran Zhou, Shanlin Liu, Wenhui Song, Guanliang Meng, Chentao Yang, Jinmin Ma, Liang Wang, Shan Gao, Yun Zhao, Hui Wang, Xin Zhou (2016) *Revealing RNA splicing diversity of insect host from co-expressed virus genes*. Unpublished.

###10. LATEST RELEASE
Version 1.0 201604

