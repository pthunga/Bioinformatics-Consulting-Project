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
