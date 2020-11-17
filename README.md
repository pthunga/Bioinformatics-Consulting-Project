**Client**: Dr. Christina Zakas
  
**Project description as provided by the client:**
We have pool-seq data from pooled individuals in 2 populations and we want to map it to our new genome assembly and pull out markers that exhibit a signature of selection, ie FST outliers. In the past I've used programs like Poppoolation2 but I'm sure there are others. Ideally we could add these markers to a track in our Jbrowser genome site. 

## Overview

Two different populations of a marine species : one from New Jersey and one from California. These populations exhibit developmental dimorphism. 

### Data handed to us 
25 individuals/ population.
4 libraries of pooled DNA from these 25 individals/ population.
2 repeated libraries for each population 
Think of it as 4 samples (bay1, bay2, lb1, lb2), 2 runs; so 8 samples in total. Data for each sample is split across the two runs. 

![data](https://github.com/pthunga/Bioinformatics-Consulting-Project/blob/master/data.PNG)

Data: Trimmed, barcode sorted. <everything was run on the same lane> 
 
Goal: Use Wright's F-statistic to identify alleles/sites that differ in frequency due to population substructure. 

### Bioinformatics Pipeline

![pipeline](https://github.com/pthunga/Bioinformatics-Consulting-Project/blob/master/pipeline.PNG)

### Quality Control

The raw reads from each sample were first checked for QC using FastQC v0.11.9. Multiqc was used to combine reports from all samples together. 
The samples passed all QC tests except for Adapter Content, Per base Sequence content and Per base GC content. 

TrimGalore was used to trim Nextera sequence contamination and fastp was used to trim for polyG tails that can occur as a consequence of NextSeq's two dye chemistry. QC reports have been added to drive. 


### Results

Histogram showing the distribution of Fst in all loci. The zoomed-in figure on the top right shows the top 1% of the Fst estimates. 

![hist](https://github.com/pthunga/Bioinformatics-Consulting-Project/blob/master/histogram.PNG)

The manhattan plot below helps visualize the distribution of Fst across the chromosomes.  Fst is shown on the Y axis and the genomic location on the X axis. Points plotted above the blue horizontal line correspond to the top 1% of the Fst estimates. Region on the chromosome 3 appears to carry several outlier loci.

![manhattan](https://github.com/pthunga/Bioinformatics-Consulting-Project/blob/master/manhattanplot.PNG)
