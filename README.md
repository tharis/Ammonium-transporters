# Ammonium-transporters
Attempting to deduce the evoultion of the Amt/Mep/Rh ammonium transporter family 

Full length sequences obtained from NCBI.

Helix sequences obtained by searching NCBI with the pdb IDs for each known ammonium transport structure

E.coli Amtb 3CIJ,
N.europaea Rh50 3B9W, 
H.sapiens RHCG 3HD6,
S.cerevisiae Mep2 5AEX,
Candidatus kuenenia stuttgertiensis Amt5 6EU6,
A.fulgidus Amt1 2B2I,
C.albicans Mep2 5AF1

Then clicking on the structure ID at the top left. This brings you to the PDB site. Click on sequence then view features in 3D and you can use this to get the helix sequence in relation to the protein structure.

Alignments done usig MAFFT in the command line

    MAFFT file.in > file.out

ncfp search was run using the command 

    ncfp -s filein fileout emial

Backthreading first needed the cached_nt.fasta headers to be changed to match their protein alignment files. This was done manually
Then backthreading was done using the command

    t_coffee -other_pg seq_reformat -in nt-file -in2 alignment-file -action +thread_dna_on_prot_aln -output fasta > outfile 

Concatenation was again needed headers to be identical so all information except sequence ID was deldeted manually 

    seqkit concat file1 file2.. > outfile

The partition file was created manually using the helix_lengths.ipynb notebook to find each helix length.

Raxml was used to create a tree using the alignment and partition files.

    raxml-ng -msa alignmentfile -model partitionfile


HMM PROFILES AND HMMER SEARCHING

Next profiles were made for each helix protein alignement]

    hmmbuild hmmfile alignmentfile
  
These were used to search pfam Uniprot file from: 
    https://pfam.xfam.org/family/PF00909.21#tabview=tab3
    
    hmmsearch -A alignmentfile hmmprofile database > searchresults
    
The results of this  are too big to upload for now and the alignment files generated come in stockhold format. These were converted to fasta format using a python script.

Hit numbers varied greatly for each helix. Helix 5 gave the lowest nuber of hits being only 2826. Since other helix searches returned many more hits it was decided that we could use these ~3000 sequences to creat a new profile. This was used to search again and increased hits to 8807. 
