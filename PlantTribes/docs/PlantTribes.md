# PlantTribes
## Overview
PlantTribes is a collection of automated modular analysis pipelines that utilize objective classifications of complete protein sequences from sequenced plant genomes to perform comparative evolutionary studies. It post-processes *de novo* assembly transcripts into putative coding sequences and their corresponding amino acid translations, locally assembles targeted gene families, estimates paralogous/orthologous pairwise synonymous/non-synonymous substitution rates for a set of gene sequences, classifies gene sequences into pre-computed orthologous plant gene family clusters, and builds gene family multiple sequence alignments and their corresponding phylogenies. A user provides *de novo* assembly transcripts, and PlantTribes produces predicted coding sequences and their corresponding translations, a table of pairwise synonymous/non-synonymous substitution rates for reciprocal best blast transcript pairs, results of significant duplication components in the distribution of Ks (synonymous substitutions) values, a summary table for transcripts classified into orthologous plant gene family clusters with their corresponding functional annotations, gene family amino acid and nucleotide fasta sequences, multiple sequence alignments, and inferred maximum likelihood phylogenies. Optionally, a user can provide externally predicted coding sequences and their corresponding amino acid translations derived from a transcriptome assembly or gene predictions from a sequenced genome. 

Please submit all questions, inquires, and bugs using the PlantTribes repository [issues](https://github.com/dePamphilis/PlantTribes/issues) tab.

## Installation
PlantTribes pipeline scripts have many external dependencies that need to be installed and available on the environment's $PATH before the pipelines can be used.
#### Pipelines dependencies
- **AssemblyPostProcessor pipeline**:  
[ESTScan (version 2.1)](http://estscan.sourceforge.net/), [TransDecoder (version 5.5.0)](https://github.com/TransDecoder/TransDecoder/releases), [HMMSearch (HMMER version 3.1b1)](http://hmmer.janelia.org/),  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/), and [GenomeTools (version 1.5.4)](http://genometools.org/).
- **GeneFamilyClassifier pipeline**:  
[BLASTP (NCBI BLAST version 2.2.29+)](http://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download), and [HMMScan (HMMER version 3.1b1)](http://hmmer.janelia.org/).
- **PhylogenomicsAnalysis pipeline (legacy pipeline)**:  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PASTA](https://github.com/smirarab/pasta), [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/), [RAxML (version 8.1.16)](http://sco.h-its.org/exelixis/web/software/raxml/index.html),  
and [FastTreeMP (version 2.1.7 SSE3)](http://meta.microbesonline.org/fasttree/).
- **GeneFamilyIntegrator**:  
No external dependencies required.
- **GeneFamilyAligner pipeline**:  
[MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PASTA](https://github.com/smirarab/pasta), and [trimAl (version 1.4.rev8)](http://trimal.cgenomics.org/).
- **GeneFamilyPhylogenyBuilder pipeline**:  
[RAxML (version 8.1.16)](http://sco.h-its.org/exelixis/web/software/raxml/index.html), and [FastTreeMP (version 2.1.7 SSE3)](http://meta.microbesonline.org/fasttree/).
- **KaKsAnalysis pipeline**:   
[MAKEBLASTDB/BLASTN (NCBI BLAST version 2.2.29+)](http://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download), [CRB-BLAST (version 0.6.9)](https://github.com/cboursnell/crb-blast), [MAFFT (version 7.215 )](http://mafft.cbrc.jp/alignment/software/), [PAML (version 4.8)](http://abacus.gene.ucl.ac.uk/software/paml.html#download),  
and [EMMIX (version 1.3)](https://people.smp.uq.edu.au/GeoffMcLachlan/emmix/emmix.html).

#### PlantTribes scaffolds data 
[PlantTribes gene family scaffolds download website](http://bigdata.bx.psu.edu/PlantTribes_scaffolds/)

#### Install PlantTribes
1. Open a terminal and change to the location where you would to keep PlantTribes. 
  - Example: `cd ~/softwares`
2. Clone the [PlantTribes](https://github.com/dePamphilis/PlantTribes) GitHub repository or download the [zip archive](https://github.com/dePamphilis/PlantTribes/archive/master.zip) and decompress it in your desired location.   
  - Examples: `git clone https://github.com/dePamphilis/PlantTribes.git` or `unzip https://github.com/dePamphilis/PlantTribes/archive/master.zip`
3. Download the scaffold data set(s) that you would like to use into the PlantTribes' [data](../data) subdirectory and decompress them.
  - Examples: `cd PlantTribes/data`, `md5sum 22Gv1.1.tar.bz` (should match the provided MD5 checksum for the data archive), followed by `tar -xjvf 22Gv1.1.tar.bz2`

## Using PlantTribes
The execulables for the PlantTribes pipelines are in the [pipelines](../pipelines) subdrectory of the installation. You can either add them to your PATH environment variable or execute directly from the PlantTribes installation.

- **AssemblyPostProcessor pipeline**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/AssemblyPostProcessor`
  - Basic run using ESTScan prediction method:
    - `PlantTribes/pipelines/AssemblyPostProcessor  --transcripts transcripts.fasta --prediction_method estscan --score_matrices /path/to/score/matrices/Arabidopsis_thaliana.smat`
- **GeneFamilyClassifier pipeline**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyClassifier`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and blastp classifier:
    - `PlantTribes/pipelines/GeneFamilyClassifier --proteins proteins.fasta --scaffold 22Gv1.1 --method orthomcl --classifier blastp`
- **PhylogenomicsAnalysis pipeline (legacy pipeline)**: 
  - Display all usage options: 
    - `PlantTribes/legacy/PhylogenomicsAnalysis`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and raxml Phylogenetic trees inference method:
    - `PlantTribes/pipelines/PhylogenomicsAnalysis --orthogroup_faa geneFamilyClassification_dir/orthogroups_fasta --scaffold 22Gv1.1  --method orthomcl  --add_alignments  --tree_inference raxml`
- **GeneFamilyIntegrator**: 
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyIntegrator`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method:
    - `GeneFamilyIntegrator --orthogroup_faa geneFamilyClassification_dir/orthogroups_fasta --scaffold 22Gv1.1  --method orthomcl`
- **GeneFamilyAligner pipeline**:  
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyAligner`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and mafft alignment method:
    - `GeneFamilyAligner --orthogroup_faa integratedGeneFamilies_dir --alignment_method mafft`
- **GeneFamilyPhylogenyBuilder pipeline**:  
  - Display all usage options: 
    - `PlantTribes/pipelines/GeneFamilyPhylogenyBuilder`
  - Basic run using 22Gv1.1 scaffolds, orthomcl clustering method, and fastree Phylogenetic trees inference method:
    - `GeneFamilyPhylogenyBuilder --orthogroup_aln geneFamilyAlignments_dir/orthogroups_aln --tree_inference fasttree`     
- **KaKsAnalysis pipeline**
  - Display all usage options:
    - `PlantTribes/pipelines/KaKsAnalysis`
  - Basic run using for paralogous analysis:
    - `KaKsAnalysis --coding_sequences_species_1 species1.fna --proteins_species_1 species1.faa --comparison paralogs --num_threads 4`

## Pipeline options

#### AssemblyPostProcessor pipeline
```
Required Options:

--transcripts <string>          : de novo transcriptome assembly fasta file (transcripts.fasta)

--prediction_method <string>    : The prediction method for coding regions
                                  If ESTScan: estscan
                                  If TransDecoder: transdecoder

--score_matrices <string>       : Required if the coding regions prediction method is ESTScan
                                  (i.e. Arabidopsis_thaliana.smat, Oryza_sativa.smat, Zea_mays.smat)
                                  
Target Gene Family Assembly:

--gene_family_search <string>   : File with a list of orthogroup identifiers for target gene families to assemble
                                  Orthogroup identifiers can be obtained from the scaffold function annotation table -
                                  "Orthogroup ID" field of .summary file in the config directory of the installation.
                                  - requires "--scaffold" and "--method" 
                                  
--scaffold <string>             : Orthogroups or gene families proteins scaffold.  This can either be an absolute
                                  path to the directory containing the scaffolds (e.g., /home/scaffolds/22Gv1.1)
                                  or just the scaffold (e.g., 22Gv1.1).  If the latter, ~home/data is prepended to
                                  the scaffold to create the absolute path.
                                  If Monocots clusters (version 1.0): 12Gv1.0
                                  If Angiosperms clusters (version 1.0): 22Gv1.0
                                  If Angiosperms clusters (version 1.1): 22Gv1.1
                                  If Green plants clusters (version 1.0): 31Gv1.0
                                  If Other non PlantTribes clusters: XGvY.Z, where "X" is the number species in the scaffold,
                                  and "Y.Z" version number such as 12Gv1.0. Please look at one of the PlantTribes scaffold
                                  data on how data files and directories are named, formated, and organized.

--method <string>               : Protein clustering method - required by "--gene_family_search"
                                  If GFam: gfam
                                  If OrthoFinder: orthofinder
                                  If OrthoMCL: orthomcl
                                  If Other non PlantTribes method: methodname, where "methodname" a nonempty string of
                                  word characters (alphanumeric or "_"). No embedded special charaters or white spaces.

--gap_trimming <float>          : Removes gappy sites in alignments (i.e. 0.1 removes sites with 90% gaps): [0.0 to 1.0]
                                  Default: 0.1

--min_coverage <float>          : Minimum sequence coverage in the orthogroup trimmed protein multiple sequence alignment
                                  Selecting transcripts with coverage of at least the average of the backbone orthogroup gene
                                  models is recommended. Details in targeted gene family assembly summary statistics output file.
                                  Default: 0.0 - [0.0 to 1.0]

Others Options:

--strand_specific               : If de novo transcriptome assembly was performed with strand-specific library
                                  Default: not strand-specific 

--dereplicate                   : Remove reapeated sequences in predicted coding regions

--min_length <int>              : Minimum sequence length of predicted coding regions

--num_threads <int>             : number of threads (CPUs) - only required for targeted gene family assembly                          
                                  Default: 1
```
#### GeneFamilyClassifier Pipeline
```
Required Options:

--proteins <string>             : Amino acids (proteins) sequences fasta file (proteins.fasta)

--scaffold <string>             : Orthogroups or gene families proteins scaffold.  This can either be an absolute
                                  path to the directory containing the scaffolds (e.g., /home/scaffolds/22Gv1.1)
                                  or just the scaffold (e.g., 22Gv1.1).  If the latter, ~home/data is prepended to
                                  the scaffold to create the absolute path.
                                  If Monocots clusters (version 1.0): 12Gv1.0
                                  If Angiosperms clusters (version 1.0): 22Gv1.0
                                  If Angiosperms clusters (version 1.1): 22Gv1.1
                                  If Green plants clusters (version 1.0): 30Gv1.0
                                  If Other non PlantTribes clusters: XGvY.Z, where "X" is the number species in the scaffold,
                                  and "Y.Z" version number such as 12Gv1.0. Please look at one of the PlantTribes scaffold
                                  data on how data files and directories are named, formated, and organized.

--method <string>               : Protein clustering method
                                  If GFam: gfam
                                  If OrthoFinder: orthofinder
                                  If OrthoMCL: orthomcl
                                  If Other non PlantTribes method: methodname, where "methodname" a nonempty string of
                                  word characters (alphanumeric or "_"). No embedded special charaters or white spaces.
                                  
--classifier <string>           : Protein classification method 
                                  If BLASTP: blastp
                                  If HMMScan: hmmscan
                                  If BLASTP and HMMScan: both
                  
Others Options:

--config_dir <string>           : (Optional) Absolute path to the directory containing the default configuration files
                                  for the selected scaffold defined by the value of the --scaffold parameter (e.g.,
                                  /home/configs/22Gv1.1). If this parameter is not used, the directory containing the
                                  default configuration files is set to ~home/config.

--num_threads <int>             : number of threads (CPUs) to used for HMMScan, BLASTP, and MAFFT
                                  Default: 1 

--super_orthogroups <string>    : SuperOrthogroups MCL clustering - blastp e-value matrix between all pairs of orthogroups
                                  If minimum e-value: min_evalue (default) 
                                  If average e-value: avg_evalue

--single_copy_custom <string>   : Configuration file for single copy orthogroup custom selection - incompatible with
                                  "--single_copy_taxa".  This must be an absolute path to the configuration file
                                  (e.g., '~/home/scaffolds/22Gv1.1.singleCopy.config') or the string 'default'.   If the
                                  latter, the config is defined to be ~/config_dir/~scaffold.singleCopy.config.  See the
                                  single copy configuration files the config sub-directory of the installation on how to
                                  customize the single copy selection.	
                                    
--single_copy_taxa <int>        : Minimum single copy taxa required in orthogroup - incompatible with "--single_copy_custom"

--taxa_present <int>            : Minimum taxa required in single copy orthogroup - requires "--single_copy_taxa"

--orthogroup_fasta              : Create orthogroup fasta files - requires "--coding_sequences" for CDS orthogroup fasta
                                    
--coding_sequences <string>     : Corresponding coding sequences (CDS) fasta file (cds.fasta)
```
#### PhylogenomicsAnalysis pipeline (legacy pipeline)
```
Required Options:

--orthogroup_faa <string>       : Directory containing gene family classification orthogroups protein fasta files

--scaffold <string>             : Orthogroups or gene families proteins scaffold.  This can either be an absolute
                                  path to the directory containing the scaffolds (e.g., /home/scaffolds/22Gv1.1)
                                  or just the scaffold (e.g., 22Gv1.1).  If the latter, ~home/data is prepended to
                                  the scaffold to create the absolute path.
                                  If Monocots clusters (version 1.0): 12Gv1.0
                                  If Angiosperms clusters (version 1.0): 22Gv1.0
                                  If Angiosperms clusters (version 1.1): 22Gv1.1
                                  If Green plants clusters (version 1.0): 30Gv1.0
                                  If Other non PlantTribes clusters: XGvY.Z, where "X" is the number species in the scaffold,
                                  and "Y.Z" version number such as 12Gv1.0. Please look at one of the PlantTribes scaffold
                                  data on how data files and directories are named, formated, and organized.	

--method <string>               : Protein clustering method
                                  If GFam: gfam
                                  If OrthoFinder: orthofinder
                                  If OrthoMCL: orthomcl
                                  If Other non PlantTribes method: methodname, where "methodname" a nonempty string of
                                  word characters (alphanumeric or "_"). No embedded special charaters or white spaces.

Multiple Sequence Alignments:

--create_alignments             : Create orthogroup protein multiple sequence alignments including scaffold backbone proteins
                                  (MAFFT algorithm, incompatible with "--add_alignments" and "--pasta_alignments") 	
                                  
--add_alignments                : Add unaligned orthogroup proteins to scaffold backbone multiple sequence alignments
                                  (MAFFT algorithm, incompatible with "--create_alignments" and "--pasta_alignments")

--pasta_alignments              : Create orthogroup protein multiple sequence alignments including scaffold backbone proteins
                                  (PASTA algorithm, incompatible with "--create_alignments" and "--add_alignments") 

--codon_alignments              : Construct orthogroup multiple codon alignments - requires "--orthogroup_fna"

--iterative_realignment <int>   : Iterative orthogroups realignment, trimming and fitering - requires "--remove_sequences"
                                  (maximum number of iterations) 

Phylogenetic Trees:

--tree_inference <string>       : Phylogenetic trees inference method
                                  If RAxML: raxml
                                  If FastTree: fasttree

--max_orthogroup_size <int>     : Maximum number of sequences in orthogroup alignments
                                  Default: 100  

--min_orthogroup_size <int>     : Minimum number of sequences in orthogroup alignments
                                  Default: 4

--sequence_type <string>        : Sequence type used in the phylogenetic inference - "dna" requires "--codon_alignments"
                                  If amino acid based: protein (default)
                                  If nucleotide based: dna

--rooting_order <string>        : File with a list of string fragments matching sequences identifiers of species in the 
                                  classification (including scaffold taxa) to be used for determining the most basal taxa in
                                  the orthogroups for rooting trees. Should be listed in decreasing order from older to younger
                                  lineages. If the file is not provided, trees will be rooted using the most distant taxon
                                  present in the orthogroup (see example rooting order configuration files in config sub-directory
                                  of the installation). 
                                  - requires "--tree_inference" with RAxML
                                  
--bootstrap_replicates <int>    : Number of replicates for rapid bootstrap analysis and search for the best-scoring ML tree
                                  - requires "--tree_inference" with RAxML
                                  Default: 100

MSA Quality Control Options:

--automated_trimming            : Trims alignments using trimAl's ML heuristic trimming approach - incompatible "--gap_trimming"  
                                  
--gap_trimming <float>          : Removes gappy sites in alignments (i.e. 0.1 removes sites with 90% gaps): [0.0 to 1.0]

--remove_sequences <float>      : Removes gappy sequences in alignments (i.e. 0.5 removes sequences with 50% gaps): [0.1 to 1.0]
                                  - requires either "--automated_trimming" or "--gap_trimming"

Others Options:

--config_dir <string>           : (Optional) Absolute path to the directory containing the default configuration files
                                  for the selected scaffold defined by the value of the --scaffold parameter (e.g.,
                                  /home/configs/22Gv1.1). If this parameter is not used, the directory containing the
                                  default configuration files is set to ~home/config.

--num_threads <int>             : number of threads (CPUs) to assign to external utilities (MAFFT, PASTA, and RAxML)
                                  Default: 1 

--max_memory <int>              : maximum memory (in mb) available to PASTA's java tools - requires "--pasta_alignments" 
                                  Default: 256
 
--pasta_iter_limit <int>        : Maximum number of iteration that the PASTA algorithm will run - requires "--pasta_alignments" 
                                  Default: 3
                                 
--orthogroup_fna                : Corresponding gene family classification orthogroups CDS fasta files. Files should be in the
                                  same directory with input orthogroups protein fasta files.
```
#### GeneFamilyIntegrator
```
Required Options:

--orthogroup_fasta <string>     : Directory containing gene family classification orthogroups fasta files

--scaffold <string>             : Orthogroups or gene families proteins scaffold.  This can either be an absolute
                                  path to the directory containing the scaffolds (e.g., /home/scaffolds/22Gv1.1)
                                  or just the scaffold (e.g., 22Gv1.1).  If the latter, ~home/data is prepended to
                                  If Monocots clusters (version 1.0): 12Gv1.0
                                  If Angiosperms clusters (version 1.0): 22Gv1.0
                                  If Angiosperms clusters (version 1.1): 22Gv1.1
                                  If Green plants clusters (version 1.0): 30Gv1.0
                                  If Other non PlantTribes clusters: XGvY.Z, where "X" is the number species in the scaffold,
                                  and "Y.Z" version number such as 12Gv1.0. Please look at one of the PlantTribes scaffold
                                  data on how data files and directories are named, formated, and organized.

--method <string>               : Protein clustering method for the classification scaffold
                                  If GFam: gfam
                                  If OrthoFinder: orthofinder
                                  If OrthoMCL: orthomcl
                                  If Other non PlantTribes method: methodname, where "methodname" a nonempty string of
                                  word characters (alphanumeric or "_"). No embedded special charaters or white spaces.        
```
#### GeneFamilyAligner
```
Required Options:

--orthogroup_faa <string>       : Directory containing gene family classification orthogroup protein fasta files

--alignment_method <string>     : Multiple sequence alignment method:
                                  If MAFFT algorithm: mafft
                                  If PASTA algorithm: pasta 


Codon Alignments:

--codon_alignments              : Construct orthogroup multiple codon alignments - corresponding gene family classification
                                  orthogroups CDS fasta files should be in the same directory with input orthogroups protein
                                  fasta files.

MSA Quality Control Options:

--automated_trimming            : Trims alignments using trimAl's ML heuristic trimming approach - incompatible "--gap_trimming"  
                                   
--gap_trimming <float>          : Removes gappy sites in alignments (i.e. 0.1 removes sites with 90% gaps): [0.0 to 1.0]

--remove_sequences <float>      : Removes gappy sequences in alignments (i.e. 0.7 removes sequences with more than 30% gaps): [0.1 to 1.0]
                                  - requires either "--automated_trimming" or "--gap_trimming"

--iterative_realignment <int>   : Iterative orthogroups realignment, trimming and fitering - requires "--remove_sequences"
                                  (maximum number of iterations)    
Others Options:

--config_dir <string>           : (Optional) Absolute path to the directory containing the default configuration files
                                  for the selected scaffold defined by the value of the --scaffold parameter (e.g.,

--num_threads <int>             : number of threads (CPUs) to assign to external utilities (MAFFT and PASTA)
                                  Default: 1 

--max_memory <int>              : maximum memory (in mb) available to PASTA's java tools - requires "--alignment_method = pasta" 
                                   Default: 256
 
--pasta_iter_limit <int>        : Maximum number of iteration that the PASTA algorithm will run - requires "--alignment_method = pasta"  
                                  Default: 3

--pasta_script_path <string>    : Optional path to the location of the run_pasta.py script. which is used for running PASTA
                                  from the command line (useful since the script is a .py file).  Using this will override
                                  the default defined in ~home/config/plantTribes.
```
#### GeneFamilyPhylogenyBuilder
```
Required Options:

--orthogroup_aln <string>       : Directory containing gene family orthogroup alignment file

--tree_inference <string>       : Phylogenetic trees inference method
                                  If RAxML: raxml
                                  If FastTree: fasttree
                                    
 Others Options:

--scaffold <string>             : Orthogroups or gene families proteins scaffold.  This can either be an absolute
                                  path to the directory containing the scaffolds (e.g., /home/scaffolds/22Gv1.1)
                                  or just the scaffold (e.g., 22Gv1.1).  If the latter, ~home/data is prepended to
                                  the scaffold to create the absolute path.
                                  If Monocots clusters (version 1.0): 12Gv1.0
                                  If Angiosperms clusters (version 1.0): 22Gv1.0
                                  If Angiosperms clusters (version 1.1): 22Gv1.1
                                  If Green plants clusters (version 1.0): 30Gv1.0
                                  If Other non PlantTribes clusters: XGvY.Z, where "X" is the number species in the scaffold,
                                  and "Y.Z" version number such as 12Gv1.0. Please look at one of the PlantTribes scaffold
                                  data on how data files and directories are named, formated, and organized.

--method <string>               : Protein clustering method for the classification scaffold
                                  If GFam: gfam
                                  If OrthoFinder: orthofinder
                                  If OrthoMCL: orthomcl
                                  If Other non PlantTribes method: methodname, where "methodname" a nonempty string of
                                  word characters (alphanumeric or "_"). No embedded special charaters or white spaces.
                                  
--config_dir <string>           : (Optional) Absolute path to the directory containing the default configuration files
                                  for the selected scaffold defined by the value of the --scaffold parameter (e.g.,
                                  /home/configs/22Gv1.1). If this parameter is not used, the directory containing the
                                  default configuration files is set to ~home/config.

--max_orthogroup_size <int>     : Maximum number of sequences in orthogroup alignments
                                  Default: 100  

--min_orthogroup_size <int>     : Minimum number of sequences in orthogroup alignments
                                  Default: 4

--rooting_order <string>        : File with a list of string fragments matching sequences identifiers of species in the 
                                  classification (including scaffold taxa) to be used for determining the most basal taxa in
                                  the orthogroups for rooting trees. Should be listed in decreasing order from older to younger
                                  lineages. If the file is not provided, trees will be rooted using the most distant taxon
                                  present in the orthogroup (see example rooting order configuration files in config sub-directory
                                  of the installation). 
                                  - requires "--tree_inference" with RAxML

--bootstrap_replicates <int>    : Number of replicates for rapid bootstrap analysis and search for the best-scoring ML tree
                                  - requires "--tree_inference" with RAxML
                                  Default: 100

--num_threads <int>             : number of threads (CPUs) to assign to external utilities (RAxML)
                                  Default: 1 
```
#### KaKsAnalysis pipeline
```
Required Options:

--coding_sequences_species_1 <string>   : Coding sequences (CDS) fasta file for the first species (species1.fna)

--proteins_species_1 <string>           : Amino acids (proteins) sequences fasta file for the first species (species1.faa) 

--comparison <string>                   : pairwise sequence comparison to determine homolgous pairs
                                          If self species comparison: paralogs
                                          If cross species comparison: orthologs (requires second species data)
                                          
Others Options:

--coding_sequences_species_2 <string>   : Coding sequences (CDS) fasta file for the first species (species2.fna)
                                          requires "--comparison" to be set to "orthologs" 

--proteins_species_2 <string>           : Amino acids (proteins) sequences fasta file for the first species (species2.faa)
                                          requires "--comparison" to be set to "orthologs"
                                          
--crb_blast <string>                    : Use conditional reciprocal best BLAST to determine for cross-species orthologs
                                          instead of the default reciprocal best BLAST - requires "--comparison" to be set to "orthologs

--min_coverage <float>                  : Minimum sequence pairwise coverage length between homologous pairs
                                          Default: 0.5 (50% coverage) - [0.3 to 1.0]

--recalibration_rate <float>            : Recalibrate synonymous substitution (ks) rates of a species using a predetermined evolutionary 
                                          rate that can be determined from a species tree inferred from a collection single copy genes
                                          from taxa of interest (Cui et al., 2006) - applies only paralogous ks

--codeml_ctl_file <string>              : PAML's codeml control file to carry out ML analysis of protein-coding DNA sequences using codon
                                          substitution models. The defaults in the "codeml.ctl.args" template in the config directory 
                                          of the installation will be used if not provided. NOTE: input (seqfile, treefile) and output 
                                          (outfile) parameters of codeml are not included in the template.

--fit_components                        : Fit a mixture model of multivariate normal components to synonymous (ks) distribution to
                                          identify significant duplication event(s) in a genome
                                          
--num_of_components <int>               : Number components to fit to synonymous substitutions (ks) distribution - required if 
                                          "--fit_components"

--min_ks <float>                        : Lower limit of synonymous substitutions (ks) - necessary if fitting components to the
                                          distribution to reduce background noise from young paralogous pairs due to normal gene births
                                          and deaths in a genome.  
                                           
--max_ks <float>                        : Upper limit of synonymous substitutions (ks) - necessary if fitting components to the
                                          distribution to exclude likey ancient paralogous pairs.
                                          
--num_threads <int>                     : number of threads (CPUs)   
                                          Default: 1
```

## License
PlantTribes is distributed under the GNU GPL v3. For more information, see [license](../LICENSE).

