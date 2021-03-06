# fastablasta
Python blastn wrapper

## Author
Jason Kwong (@kwongjc)  
GitHub: [kwongj](https://github.com/kwongj)  

## Dependencies
* [Python 3.x](https://www.python.org/downloads/)
* [BioPython](http://biopython.org/wiki/Main_Page)
* [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download)

## Usage
```
$ fastablasta -h

usage: 
  fastablasta --query QUERY [OPTIONS] FASTA1 FASTA2 FASTA3 ... FASTAN > results.txt

Searches a FASTA file for a specified query sequence using BLASTN

positional arguments:
  FASTA            FASTA file to search (required)

optional arguments:
  -h, --help       show this help message and exit
  --query QUERY    query sequence to search for in FASTA format eg. rpoB, KPC-2 (required)
  --id %ID         percentage identity cutoff (default=99)
  --cov %COVERAGE  percentage coverage cutoff (default=99)
  --evalue EVALUE  evalue cutoff (default=1e-1)
  --wordsize SIZE  length of initial match (default=32)
  --short          allow searching for short sequences
  --outfmt FORMAT  specify BLAST output format (default='6 qseqid qlen sseqid sstrand pident length qcovs mismatch gapopen qstart qend sstart send evalue bitscore')
  --cpus CPUS      number of CPUS to use (default=1)
  --version        show program's version number and exit
```


**Basic Usage:**  

`$ fastablasta --query [QUERY] FASTA1 FASTA2 FASTA3`  


**To save output to file:**  

`$ fastablasta --query [QUERY] FASTA1 FASTA2 FASTA3 > results.txt`  


**To use 100% identity cutoff:**  

`$ fastablasta --query [QUERY] --id 100 FASTA1 FASTA2 FASTA3`  


**To use high Evalue cutoff:**  

`$ fastablasta --query [QUERY] --evalue 1e-2 FASTA1 FASTA2 FASTA3`  

See [here](http://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=FAQ#expect) for more information on expect(E) values.  


**To change length of initial match (default = 32):**  

`$ fastablasta --query [QUERY] --wordsize 11 FASTA1 FASTA2 FASTA3`  


**To search for short nucleotide sequences <30bp:**  

`$ fastablasta --query [QUERY] --short FASTA1 FASTA2 FASTA3`  

This optimises the parameters to search for short sequences (blastn-short). The main changes are:  

| Program                             |     Task     | Word Size | Filter Setting | Expect Value |  
|:----------------------------------- |:------------:|:---------:|:--------------:|:------------:|  
| Standard Nucleotide BLAST           |    blastn    |    32     |   On (DUST)    |     1e-99    |  
| Search for short/near exact matches | blastn-short |     7     |      Off       |      1e-2    |  

See [here](http://www.ncbi.nlm.nih.gov/BLAST/Why.shtml) for more information.  


**To set output format:**  

`$ fastablasta --query [QUERY] --outfmt 6 FASTA1 FASTA2 FASTA3`  

***alignment view options:***  
0 = pairwise  
1 = query-anchored showing identities  
2 = query-anchored no identities  
3 = flat query-anchored, show identities  
4 = flat query-anchored, no identities  
5 = XML Blast output  
6 = tabular  
7 = tabular with comment lines  
8 = Text ASN.1  
9 = Binary ASN.1  
10 = Comma-separated values  
11 = BLAST archive format (ASN.1)  
12 = JSON Seqalign output  
13 = JSON Blast output  
14 = XML2 Blast output  


*NB. This version uses* `-subject` *instead of* `-db` *due to issues with directing BLAST to a custom database. This was not recommended by some previously due to issues with different 
expect-values from the traditional* `-db`, *although if looking for exact or near exact matches, it probably won't affect the results significantly. However, please check your results.
See this [blog post](http://blastedbio.blogspot.com.au/2012/05/blast-ingoring-search-space-size-for-e.html) for more information.*

## Bugs
Please submit via the GitHub issues page: [https://github.com/kwongj/fastablasta/issues](https://github.com/kwongj/fastablasta/issues)  

## Software Licence
GPLv2: [https://github.com/kwongj/fastablasta/blob/master/LICENSE](https://github.com/kwongj/fastablasta/blob/master/LICENSE)

## Other links
* [NCBI BLAST](http://blast.ncbi.nlm.nih.gov/Blast.cgi)
* [BLAST Manual](http://www.ncbi.nlm.nih.gov/books/NBK279690/)
