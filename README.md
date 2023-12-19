Using Github as a place to show methods & resulting data for research paper:  <i>"Comparative genomics reveals diversification of therapeutic target LysR-type transcriptional regulators in the nosocomial pathogen Pseudomonas aeruginosa"<i>


- Recovery of P. aeruginosa LTTR protein sequences from IMG Database. <br>
**Programs used: cd-hit, command line ubuntu**<br>
LTTR protein sequences were retrieved from all of the 699 available permanent, draft and finished P. aeruginosa genomes in the Integrated Microbial Genomes (IMG). The following protein conserved domain families with accession numbers COG0583, Pfam00126 and Pfam03466 were applied to identify ~260k LTTR homologues. These LTTR amino acid sequences were then filtered by removing duplicate sequences and sequences less than 150 amino acids and larger than 350 amino acids using the Biolinux command line.  The LTTR proteins (~86,000) were clustered into groups using the CD Hit program v4.6 (+OpenMP)  which uses a greedy clustering algorithm to group sequences together based on their length and similarity. A sequence identity threshold of 95% was used to cluster the sequences into groups with one representative LTTR per group.
<i> biolinux@biolinux-VirtualBox[biolinux] cd-hit -i galaxy_no_duplicates.fa -o seqs -c 0.95 -n 5 -M 0 <i>
A high threshold (greater than the 80% threshold previously used to cluster LTTRs in P. aeruginosa
was used initially in order to ensure that each group represented a close homology set and that divergence of homologous LTTR proteins could be captured. Therefore, each of these groups represents a unique LTTR and its closest homologues.


- Construction of Representative LTTR Tree. <br>
**Programs used: muscle, Phyml online tool, itol web-based tool.**<br>
A sequence alignment was carried out on the representative LTTR proteins sequences using the default parameters of the multiple alignment tool MUSCLE v3.8.31.
<i> biolinux@biolinux-VirtualBox[Creating_Fig1]  muscle -in seqs -phyiout reps_muscle <i>
The MUSCLE output was then used to create a cluster tree. A Maximum-Likelihood tree was built with PhyML v3.0.1 <i> http://www.atgc-montpellier.fr/phyml/ <i> using the WAG amino acid substitution model of evolution and four categories of substitution rates. Branch supports were evaluated using the approximate likelihood-ratio test (aLRT). Phyml outputs a Newick file which was visualised and exported using the web-based tool Interactive Tree Of Life <i>https://itol.embl.de/ <i> (iTOL v4.4.2).


- Analysis of the distribution of LTTRs across the P. aeruginosa pangenome. <br>
**Programs used: cd-hit, muscle, Phyml online tool, R with Rstudio: dplyr & ggplot2 packages.**<br>
A CD hit of 80% was performed using the same parameters to ensure all of the LTTRs were captured by the correct representative sequence.
<i> biolinux@biolinux-VirtualBox[cd_hit_80]  cd-hit -i galaxy_no_duplicates.fa -o seqs -c 0.8 -n 5 -M 0 <i>
As the aim here was to ensure that all homologous of a particular LTTR were captured in the same group, the threshold for inclusion was relaxed to 80%. The distribution of the LTTRs was analysed across the genomes using RStudio (v1.1a) to manipulate the data from the CD Hit results using the dplyr package v0.8.3 and to create a histogram and scatter plot using the ggplot2 package v3.2.0 .

- Comparative genomic analysis of the LTTR diversification. <br>
**Programs used:cd-hit, R with Rstudio: tidyverse & ggplot2 packages.**<br>
A CD Hit using a sequence identity threshold of 100% using the same parameters as above was then used to analyse the variation of LTTRs across the genomes. The variation of each LTTR was calculated by dividing the number of clusters by the number of genomes the protein is present in. This number was then multiplied by 100 to give a unit of variance. The calculations were carried out in R and the top 10 most and least variable LTTR results were tabulated and formatted using the tidyverse package v1.3.0 and pie-charts were created using ggplot2.


- McDonald– Kreitman Analysis of Selective . <br>
**Programs used: BLASTn, MKT online tool.**<br>
The standard McDonald– Kreitman test was performed on full length LTTR nucleotide sequences of the most variable LTTRS in P. aeruginosa.
ID numbers from the AA sequences were extracted which made a list of IDs.
<i> biolinux@biolinux-VirtualBox[MKT] perl -ne 'if(/^>(\S+)/){print "$1\n"}' 112 > 112_ids <i>


DNA sequences with the ID numbers were then extracted from the fasta file containing all DNA sequences.
<i>biolinux@biolinux-VirtualBox[MKT] perl -ne 'if(/^>(\S+)/){$c=$i{$1}}$c?print:chomp;$i{$_}=1 if @ARGV' 0_ids all_dna_sequences > 0_reps<i>
The neutrality index (NI) was calculated based on the ratio of polymorphisms to substitutions as follows: NI = (Pn/Ps)/(Dn/Ds), where P signifies polymorphism within the species and D represents divergence between species. The sequences were obtained from the JGI IMG database, and the outliers used were P. fluorescens and Pseudomonas sp. AK6U.  Two housekeeping genes (rpoD, gyrB) were also selected as controls for this analysis and their sequences were obtained using the Pseudomonas database and BLASTn.

- Construction of the PqsR Cluster Tree with metadata. <br>
**Programs used:cd-hit, muscle, R with Rstudio: tidyverse package, itol web-based tool.**<br>
The available host and isolation information was obtained from the JGI IMG database for the 699 genomes. Data manipulation was performed using the tidyverse package in R. LTTR sequences from the 100% CD Hit output were aligned using MUSCLE with the default parameters. The tree was created using the Phyml software with the parameters outlined above and the trees were visualised using the web interface iTOL. The metadata scripts were manually created using the available iTOL templates as examples and uploaded through the web interface. 



