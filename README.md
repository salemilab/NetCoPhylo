# NetCoPhylo

This is a novel computational tool that integrates Bayesian methods into a phylogenetic framework to identify significant co-evolving sites across branches among pre-defined subgroups of sequences. It consist of one R script.

The input of the tool includes a phylogenetic tree in nexus format (from BEAST¹) and a .json file generated in Nexstrain².

## Basic Usage

Using the command:
```sh
Rscript coevol_tool.R -h 
```
or 
```sh
Rscript coevol_tool.R -help
```
the following message message is printed with the parameters required for the run.
```sh
Usage: coevol_tool.R [options]


Options:
	-t TREE, --tree=TREE
		Load phylogenetic tree rescaled in time (nexus format)

	-a ANCESTRAL, --ancestral=ANCESTRAL
		Load ancestral state reconstruction .json file

	-d NUMBER, --days=NUMBER
		Most recent time point in days

	-w WINDOW, --window=WINDOW
		Length of time windows in days [default 30]

	-o OUTPUT, --output=OUTPUT
		Name for the output file
		
	-m MODE, --mode=MODE
		In the event that a branch covers more than one time window, choose if analysis will be done by assigning these branches to their minimum or maximum window. Choose 1 for minimum window or 2 for maximum window.

	-h, --help
		Show this help message and exit
```				

Example:
```sh
Rscript coevol_tool.R -t N01_SIVmac251.tre -a SIVmac251_ancestral_sequences.json -d 300 -w 50 -o N01_sites
```
```sh
Rscript coevol_tool.R -t N07_SIV.tre -a N07_SIV.json -d 75 -o N07
```
```-o``` is used as part of the name of several output files. These refer to:

1) A comma separated file that includes the sample name with its mutations, assigned window, origin and final dpi, origin and final tissue, and deletions present (if any).
2) A strength distribution plot that shows a view of the number of pairs of sites with their respective posterior probability (.png format).
3) An image with the networks of significant pairs of sites that are coevolving together. These networks have arrows to indicate the directionality of the coevolution (.png format).

For example, ```-o``` N01_sites will generate files named *N01_sites_branch-site_mutations_min.win.csv, N01_sites_strength_distribution.png, N01_sites_sites.png*.

## Dependencies

Libraries required to be installed in R to run the script: optparse, treeio, tidyverse, tidytree, plyr, dplyr, tidyr, jsonlite, parallel, ape, data.table, Rgraphviz, bnlearn, ggplot2, igraph, RColorBrewer.







¹ Suchard MA, Lemey P, Baele G, Ayres DL, Drummond AJ & Rambaut A (2018) Bayesian phylogenetic and phylodynamic data integration using BEAST 1.10 Virus Evolution 4, vey016. DOI:10.1093/ve/vey016.
² Hadfield et al., Nextstrain: real-time tracking of pathogen evolution, Bioinformatics (2018).		
