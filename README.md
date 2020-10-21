# S-conLSH-2.0
Spaced-context based Locality Sensitive hashing for Alignment-free gapped mapping of Noisy Long Reads. This is an upgrade of S-conLSH which can handle multiple simultaneous threads to achieve a better run-time performance.


### Installation
```

Current version of S-conLSH needs to be run on Linux operating system. 

The source code is written in C++. 

The makefile is attached. Use make command to generate the executables.
The binary 'S-conLSH' performs indexing of the reference genome and then aligns the long and noisy PacBio reads to it.

OpenMP support is required to execute S-conLSH in multiple threads. (Run "sudo apt-get install libomp-dev" in Linux terminal to install it)
The default setting of the method works in a single-threaded version. The tool may be run in multiple threads using the option "--thread" (Please see Parameters section). Multi-threaded execution incurs higher CPU and memory load. A good choice of selecting the number of threads would be equal to the number of CPU-cores available. 

```
### Synopsis
```

S-conLSH <PathOfSourceFiles> <ReferenceGenome> <ReadFile>  [-K concatenationFactor] [-L NumberOfHashTables] [--lambda contextFactor] [--zero spacesInPatterns] [-w windowsHits] [-m candidates] [-x match] [-y mismatch] [-q gapOpen] [-r gapExtension] [-a alignInSAM] > <OutputFile>


```
### Parameters (could be updated in the future for adding new functions)
```
------------------------------------------------------------------------------------------------------
-K, --K                <int>           Concatenation factor of locality sensitive hashing [Default=2]
-L, --L                <int>           Number of hash tables in conLSH framework [Default=2]
--lambda               <int>           The context factor [Default=3]
--zero                 <int>           The number of don't cares or zeros in the S-conLSH pattern [Default=5]
-w, --window-hits      <int>           The max allowed number of windows hitting by a k-mer [Default=1000] 
-m, --candidates       <int>           The number of candidates for extension [Default=400]
-x, --match            <int>           Score of match for the alignments in extension phase [Default=2]
-y, --mismatch         <int>           Mismatch penalty for the alignments in extension phase [Default=5]
-q, --gap-open         <int>           Gap open penalty for the alignments in extension phase [Default=2]
-r, --gap-extension    <int>           Gap extension penalty for the alignments in extension phase [Default=1]
-a, --align	           <int>           Value=1, outputs alignment in SAM format [Default=0, Alignment-free PAF format output]
--thread               <int>           Number of threads to be forked in a multi-threaded system [Default=1].     
-h, --help                             Help
-------------------------------------------------------------------------------------------------------


```
### Quick start
```
The package includes sample reference genome and SMRT reads to demonstrate the quick start guide. 

``` For alignment free mapping in PAF format

./S-conLSH ../src/ ../sample_data/ecoli_AE005174v2.fas ../sample_data/SRR801638.fasta > sample.paf

``` For SMRT alignment in SAM format

``` ./S-conLSH ../src/ ../sample_data/ecoli_AE005174v2.fas ../sample_data/SRR801638.fasta --align 1 > sample.sam


```
### Reference

[1] rHAT: Liu, B., Guan, D., Teng, M. & Wang, Y. rHAT: fast alignment of noisy long reads with regional hashing. 
Bioinformatics 32, 1625–1631 (2015).

[2] conLSH: conLSH:Context based Locality Sensitive Hashing for Mapping of noisy SMRT Reads. Computational Biology and Chemistry, Elsevier [Accepted]

[3] S-conLSH: Alignment-free gapped mapping of noisy long reads
Angana Chakraborty, Burkhard Morgenstern, Sanghamitra Bandyopadhyay
bioRxiv 801118; doi: https://doi.org/10.1101/801118


### Contact

For advising, bug reporting and requiring help, please contact angana_r@isical.ac.in
