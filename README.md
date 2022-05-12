# Align2FASTAs

Align two FASTA files. The function needs one source file and one target file, and each element of the target is aligned with all the elements in the source file, and the maximum alignment score is selected as match. Usually not all amino acid sequences will have a good match, and therefore the function returns the matching score so that the user can judge which alignments to keep. 

The alignment that this function performs is a dependency of the pairwiseAlignment R function and the details can be found in https://www.rdocumentation.org/packages/Biostrings/versions/2.40.2/topics/pairwiseAlignment

Example:

```
## dependencies

if(!require(seqinr)){install.packages("seqinr"); require(seqinr)}
library(seqinr)
  
if(!require(Biostrings)){BiocManager::install("Biostrings"); require(Biostrings)}
library(Biostrings)

## example

aligned_example <- align2FASTAs(

FASTA_target_directory = "uniprot-hordeum+vulgare-filtered-reviewed_yes+AND+organism__Hordeum+vulgar--.fasta", 
FASTA_source_directory = "160517_Hv_IBSC_PGSB_r1_proteins_HighConf_REPR_annotation.fasta"

                                )
                                
## mining out a results table

FASTA_target <- seqinr::read.fasta("uniprot-hordeum+vulgare-filtered-reviewed_yes+AND+organism__Hordeum+vulgar--.fasta")

FASTA_Header_runner <- c()

FASTA_sequence_runner <- c()

for (i in 1:length(FASTA_target)) {
    
    FASTA_Header_runner[i] <- seqinr::getAnnot.SeqFastaAA(FASTA_target[[i]])
    
    FASTA_sequence_runner[i] <- paste0(seqinr::getSequence(FASTA_target[[1]]), collapse = "")
    
}

out_mat <- cbind(FASTA_Header = FASTA_Header_runner,
                 FASTA_Sequence = FASTA_sequence_runner,
                 aligned_example)

write.table(x = out_mat, file = "aligned_AT_HV.txt", sep = "\t",
            row.names = F, quote = F)

```


In the provided example we aligned Swiss-prot/Uniprot sequence targets with proteogenomics predicted *Hordeum vulgare* ORFs as source.

Source FASTA sequences were obtained from the 2017 Barley genome release (ftp://ftpmips.helmholtz-muenchen.de/plants/barley/genome_release2017/)

Target FASTA sequences are all the *Hv* Swiss-prot sequences from UniProt.


If we plot the matching scores across alignments, it becomes evident that not all alignements are high quality

```
plot(sort(x = as.numeric(aligned_example[,2]), decreasing = F),xlab = "Swiss-Prot FASTA Sequences", ylab = "Matching Scores") + abline(h = 0, col = "red")

```

![Matching_Scores](/plot_zoom.png)


