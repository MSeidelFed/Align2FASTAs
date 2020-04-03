# Align2FASTAs

Align two FASTA files. The function needs one source file and one target file, and each element of the target is aligned with all the elements in the source file, and the maximum alignment score is selected as match. Usually not all amino acid sequences will have a good match, and therefore the function returns the matching score so that the user can judge which alignments to keep. 

Example:

```
aligned_example <- align2FASTAS(

FASTA_target_directory = "Input/uniprot-hordeum+vulgare-filtered-reviewed_yes+AND+organism__Hordeum+vulgar--.fasta", 
FASTA_source_directory = "Input/160517_Hv_IBSC_PGSB_r1_proteins_HighConf_REPR_annotation.fasta"

                                )
```
