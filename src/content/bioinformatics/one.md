# Bioinformatics

## DNA sequencing/DNA测序
Is is the process of determing the nucleic sequence -- the order of nucleotides in DNA

- the order of 4 bases:
    - Adenine,
    - Thymine,
    - Cytosine,
    - Guanine.

## 全基因组测序（WGS, Whole Genome Sequencing）

### BLAST
basci local alignment search tool

Expect/ E-value
the number of BLAST hits you expect to see by chance, with the observed score or higher
A hit, is an alignment

Example:
you expect to see that alignment 1x10-44 --> one times ten to the minus fourty-four, in other words, it is not random.

if the alignment is not due to chance, then it may be due to a biologically meaningful relationship between two sequences,

BLAST doesn't measure the homology directly,

we can infer the homology from the alignments

how low an E-value do i need to say that two seqs are related biologically

In part because the E-value depend on query and database lengths

At NCBI, use a cutoff 1x10-6 , 

the cutoff could be either too restrictive or too inclusive



AlgorithmQuick BLASTP (Accelerated protein-protein BLAST)
Algorithmblastp (protein-protein BLAST)
AlgorithmPSI-BLAST (Position-Specific Iterated BLAST)
AlgorithmPHI-BLAST (Pattern Hit Initiated BLAST)
AlgorithmDELTA-BLAST (Domain Enhanced Lookup Time Accelerated BLAST)
Choose a BLAST algorithm 
