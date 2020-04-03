# Align2FASTAs

Align two FASTA files. The function needs one source file and one target file, and each element of the target is aligned with all the elements in the source file, and the maximum alignment score is selected as match. Usually not all amino acid sequences will have a good match, and therefore the function returns the matching score so that the user can judge which alignments to keep. 

The alignment that this function performs is a dependency of the pairwiseAlignment R function and the details can be found in https://www.rdocumentation.org/packages/Biostrings/versions/2.40.2/topics/pairwiseAlignment

Example:

```
aligned_example <- align2FASTAs(

FASTA_target_directory = "uniprot-hordeum+vulgare-filtered-reviewed_yes+AND+organism__Hordeum+vulgar--.fasta", 
FASTA_source_directory = "160517_Hv_IBSC_PGSB_r1_proteins_HighConf_REPR_annotation.fasta"

                                )
```


In the provided example we aligned Swiss-prot/Uniprot sequence targets with proteogenomics predicted *Hordeum vulgare* ORFs as source.

Source FASTA sequences was obtained from the 2017 Barley genome release (ftp://ftpmips.helmholtz-muenchen.de/plants/barley/genome_release2017/)

Target FASTA sequences are all the *Hv* Swiss-prot sequences from UniProt.


If we plot the matching scores across alignments, it becomes evident that not all alignements are high quality

```
plot(sort(x = as.numeric(aligned_example[,2]), decreasing = F)) + abline(h = 0, col = "red")
```

![Matching_Scores](/plot_zoom.png)


