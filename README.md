# Align2FASTAs

Align two FASTA files. The function needs one source file and one target file, and each element of the target is aligned with all the elements in the source file, and the maximum alignment score is selected as match. Usually not all amino acid sequences will have a good match, and therefore the function returns the matching score so that the user can judge which alignments to keep. 

Example:

```
aligned_example <- align2FASTAs(

FASTA_target_directory = "Input/uniprot-hordeum+vulgare-filtered-reviewed_yes+AND+organism__Hordeum+vulgar--.fasta", 
FASTA_source_directory = "Input/160517_Hv_IBSC_PGSB_r1_proteins_HighConf_REPR_annotation.fasta"

                                )
```


In the provided example we aligned Swiss-prot/Uniprot sequence targets with proteogenomics predicted *Hordeum vulgare* ORFs as source.

Source FASTA was obtained from the 2017 Barley genome release (ftp://ftpmips.helmholtz-muenchen.de/plants/barley/genome_release2017/)

Targets are all the *Hv* Swiss-prot sequences from UniProt.


If we plot the matching scores across alignments, it becomes evident that not all alignements are high quality

```
plot(sort(x = as.numeric(Swiss_Prot351_Hv[,2]), decreasing = F)) + abline(h = 0, col = "red")
```


