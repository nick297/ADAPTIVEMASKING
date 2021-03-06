# ADAPTIVEMASKING

We describe tools to examine NGS-mapped output to identify regions of high minor variant frequencies,
as [described](https://www.biorxiv.org/content/early/2018/01/23/252460).
The rationale of doing this is the identification of regions where
consensus basecalling may be unreliable.  The process is 'adaptive' in
the sense that it models variation which arises during the entire
laboratory, sequencing and mapping process and can be used to identify
regions of variation resulting anywhere in the process followed.
In [our case](https://www.biorxiv.org/content/early/2018/01/23/252460), increased variation occurred in regions of homology
between Mycobacteria and other bacterial species, and was detected when laboratory processes started to use broth-culture derived DNA extracts, rather than extracts from pure cultures.  Use of the technique described here allowed identification and masking of the problem regions.

__Obtain software and test data__   
The software needed, and instructions on how to obtain test data, is described [here](doc/Prerequisites.md).  

__Overview of the process followed__  
1. Mapping and VCF generation  
Our approach is designed to operate on the output from multiple mappers, with different settings, and with different kinds of input data.
The objective of the project is quantify the variation associated with the totality of laboratory process, input DNA, sequencing, and mapping.
Many pipelines will have already optimised mapping tools and settings; the process we describe will operate on their output.  
As input it expects VCF/BCF files, which are typically generated by samtools/bcftools mpileup commands following mapping.  In particular, it expects a tag in the VCF INFO section which contains the high quality base counts at each position: it is these which are the input to the algorithm.
For more detail on this, see [here](doc/extractmaf.md).  
Please see example code [illustrating of mapping and vcf generation](doc/map2vcf.md) operations on a test dataset.
2. Estimating the amount of extraneous bacterial DNA present    
One of the key findings from our paper is that mapping accuracy for some regions is determined by the amount of 'non-target' bacteria DNA present, in our case from species other than *Mycobacteria*.
We estimated this using Kraken.  Newer [tools](https://ccb.jhu.edu/software/bracken/) producing data in a similar format can also be used. 
Please see example code [illustrating the use of Kraken](doc/kraken.md), including the *KrakenReportReader* class from the *KrakenReportReader* module. 
3. Determining the minor variant frequencies for genomic regions  
We measured the minor variant frequencies, - that is, the read depth accounted for by calls other than the most common nucleotide - across genomic regions.
Please see [here](doc/extractmaf.md), which describes use of the *regionScan_from_genbank* class, which is in the *vcfScan* module.
4. Modelling minor variant frequencies in reads mapped to genomic regions     
Subsequently, we fitted Poisson models, region-by_region, estimating the relationship between the
minor variant call depth (~ amount of mixture ) detected and an estimate of the amount of non-bacterial DNA present.
A python class, *AdaptiveMasking*, in the *AdaptiveMasking* module, is provided to do this.  Its use is described [in detail](doc/model_maf.md)
5. Depicting the results of the modelling  
Methods in the *AdaptiveMasking* class allow depiction of model output, as [described](doc/depict.md).
6. Masking based on the results  
[What to do next](doc/next.md) 

