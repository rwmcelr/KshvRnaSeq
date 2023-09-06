# KRS
An R based RNA sequencing analysis project focused on Kaposi's Sarcoma Herpes Virus.

KRS takes RNA-seq input in the form of a count table, in this case generated by featureCounts from the Subread package.  Data importing occurs in main.R, which will require modification for use with other inputted data (sample groups need to be manually input, and formatting needs to change if counts table is generated by another program).  Analysis of raw input data is done using the DESeq2 package.  Plots and downstream analysis are generated by a number of functions, described below.

<ins>**SGaP**</ins> serves as a container function for the rest of the downstream analysis.  Arguments passed into this function are as follows:
<br>name - String used for naming of output folder, as well as the base name for subsequent output files
<br>dds - DESeq object generated previously in main.R
<br>filterBy - Statistic used to filter out results; can choose between adjusted p-value and unadjusted p-value; defaults to adjusted p-value
<br>filterVal - Number value associated with the filter statistic, filters below input value; defaults to 0.05
<br>con1 - First comparison condition, needs to exist as a group in the dds object
<br>con2 - Second comparison condition, needs to exist as a group in the dds object
<br>GS - Optional geneset flag, if set to true the functions will look for a GeneSet.csv file in the data directory, which should have a single column of target genes, with "symbol" as the first entry.  When enabled, analysis will generate additional CSV containing only data for specified genes, and will highlight the same genes in all generated graphs.

<ins>**Output files:**</ins>
- Differentially expressed gene table (shrunken and non-shrunken) [from kshvSigGenes]
- Gene expression heatmap [from kshvSigGenes]
- .rnk file for downstream pathway expression analysis [from kshvSigGenes]
- MA Plot of gene expression (with optional highlighting of targeted genes) [from kshvMA]
- Volcano plot of gene expression (with optional highlighting of targeted genes) [from kshvVolc]
- (Optional) differentially expressed gene table containing information for targeted genes only [from kshvSigGenes]
