# Shell_Scripts

# Instructions for creating a phylogenetic tree
# 1. index reference genome 
bwa index NTUHK2044.fasta
samtools faidx NTUHK2044.fasta

# 2. align to reference-- I use NTUH-K2044 as a reference genome - run on quest
perl batch.pl

# 3. combine consensus sequence run in Travis_Assemblies/Alignment/#
cat *.fasta > consensus.fasta

# 4. filter to 95% core run on quest
perl ksnp_matrix_filter_v0.3.3.pl -m 0.95 consensus.fasta > consensus_filtered0.95.fasta

# 5. Make phylogenetic tree 
FastTreeMP -nt -gtr -gamma -pseudo consensus_filtered0.95.fasta > consensus_filtered0.95.tre
