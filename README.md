# DifCover 

**_Description_**

The DifCover pipeline aims to identify regions in a reference genome for which the read coverage of one sample (sample1) is significantly different from the read coverage of another sample (sample2) when aligned to a common reference genome. “Significantly different” is determined by user-defined thresholds. The pipeline allows exclusion of regions from consideration based on read coverage. These include regions with low sequence coverage in both samples (regions that are undersampled due to nucleotide content) and regions with exceedingly high sequence coverage (i.e. repetitive sequences). Both cases can be misleading with respect to coverage analyses. The DifCover pipeline is specifically oriented to the analysis of large genomes and can handle very fragmented assemblies. 

# Method
The alignment of short reads to a reference genome can be characterized by the depth of coverage computed for each genomic position as number of reads mapped over it. Fluctuations of coverage can often yield variable coverage ratios and may interfere with the identification of regions that differ between samples. In many cases, calculating average coverage ratios over windows can more accurately reflect differences in copy number of the underlying fragments. In practice, the locations and sizes of the windows can be defined in a various ways. Traditional tools already offer solutions that allow computing average coverage over intervals of a fixed size (Sambamba, http://lomereiter.github.io/sambamba/) or splitting contig into separate intervals consisting of bases with the same coverage (bedtools, https://github.com/arq5x/bedtools2). However these tools are not, in and of themselves, well suited in practice for the analysis of large complex genomes with large numbers of gaps and repeats. DifCover addresses these issues by introducing the notion of window “stretching”. Essentially each genomic scaffold is scanned sequentially to form windows of variable size, but with predefined number of bases that have coverage within user-defined limits. These stretched windows allow bridging across under- and over-represented fragments permitting more precise analyses. For each window an average coverage is reported and compared to the coverage of another sample. For highly contiguous genomes, adjacent windows with similar coverage ratios can be combined to generate consensus estimates for larger continuous regions. Finally regions with significant difference in coverage can be extracted for downstream analyses.
