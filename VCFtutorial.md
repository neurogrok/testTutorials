# What's New in My Genome? 

Explain VCF files here (variant call format) 

## Exploring the VCF header 

The first few lines of a VCF file are called the 'header'. The header contains useful information about what the data in the file looks like and how it was generated. All of the lines in the header start with the character '##'. 

Use two different command line methods to view the information in the header for the file 'myVCF.vcf'. 

First, make sure you can see the file using the command 
```console
foo@bar:~$ ls -l 
myVCF.vcf 
```

1. Our first strategy might be to look at the first few lines of the file. We know the 'head' command will give us the first 10 by default. Let's take a look. 

```console
foo@bar:~$ head myVCF.vcf

##fileformat=VCFv4.2
##FILTER=<ID=PASS,Description="All filters passed">
##fileDate=20191015
##source=freeBayes v1.3.1-dirty
##reference=/projects/sequence_analysis/exome-pipeline/human/GRCh38.refseqids.fna
##contig=<ID=1,length=248956422>
##contig=<ID=2,length=242193529>
##contig=<ID=3,length=198295559>
##contig=<ID=4,length=190214555>
##contig=<ID=5,length=181538259>
```

That looks promising! 

We can see some useful information, like what version of the variant format this data adheres to (line 1), when the file was generated (line 3), what software was used to make the variant calls (line 4), and what species and version of the genome was used as a reference (line 5). 

But maybe we aren't seeing the whole header? Think about how you might discover this information, and we'll do an exercise to answer that question soon. 

2. A second strategy to view the header might be to pull out the lines beginning with '#'. We know that 'grep' will help us pull out specific data. Let's try that. 

```console
foo@bar:~$ grep '#' myVCF.vcf

##fileformat=VCFv4.2
##FILTER=<ID=PASS,Description="All filters passed">
##fileDate=20191015
##source=freeBayes v1.3.1-dirty
##reference=/projects/sequence_analysis/exome-pipeline/human/GRCh38.refseqids.fna
##contig=<ID=1,length=248956422>
##contig=<ID=2,length=242193529>
##contig=<ID=3,length=198295559>
##contig=<ID=4,length=190214555>
##contig=<ID=5,length=181538259>
...
##phasing=none
##commandline="freebayes -f /projects/sequence_analysis/exome-pipeline/human/GRCh38.refseqids.fna -t /projects/sequence_analysis/agilent-sureselect-v7-hg38/agilent.v7.padded.bed --cnv-map jointcalls/samp1.cnv_map.bed --genotype-qualities --strict-vcf --bam-list jointcalls/samp1.bamlist"
...
##FORMAT=<ID=GT,Number=1,Type=String,Description="Genotype">
##FORMAT=<ID=GQ,Number=1,Type=Integer,Description="Genotype Quality, the Phred-scaled marginal (or unconditional) probability of the called genotype">
##FORMAT=<ID=GL,Number=G,Type=Float,Description="Genotype Likelihood, log10-scaled likelihoods of the data given the called genotype for each possible genotype generated from the reference and alternate alleles given the sample ploidy">
##FORMAT=<ID=DP,Number=1,Type=Integer,Description="Read Depth">
##FORMAT=<ID=AD,Number=R,Type=Integer,Description="Number of observation for each allele">
##FORMAT=<ID=MIN_DP,Number=1,Type=Integer,Description="Minimum depth in gVCF output block.">
...
##SnpEffVersion="4.3t (build 2017-11-24 10:18), by Pablo Cingolani"
##SnpEffCmd="SnpEff  -no PROTEIN_PROTEIN_INTERACTION_LOCUS -no PROTEIN_STRUCTURAL_INTERACTION_LOCUS GRCh38.p7.RefSeq "
##INFO=<ID=ANN,Number=.,Type=String,Description="Functional annotations: 'Allele | Annotation | Annotation_Impact | Gene_Name | Gene_ID | Feature_Type | Feature_ID | Transcript_BioType | Rank | HGVS.c | HGVS.p | cDNA.pos / cDNA.length | CDS.pos / CDS.length | AA.pos / AA.length | Distance | ERRORS / WARNINGS / INFO'">
##INFO=<ID=LOF,Number=.,Type=String,Description="Predicted loss of function effects for this variant. Format: 'Gene_Name | Gene_ID | Number_of_transcripts_in_gene | Percent_of_transcripts_affected'">
##INFO=<ID=NMD,Number=.,Type=String,Description="Predicted nonsense mediated decay effects for this variant. Format: 'Gene_Name | Gene_ID | Number_of_transcripts_in_gene | Percent_of_transcripts_affected'">
...
##INFO=<ID=clinvar_variation_id,Number=1,Type=String,Description="ClinVar VariationID">
##INFO=<ID=clinvar_asserted_pathogenic,Number=1,Type=String,Description="Whether at least one submitter using criteria asserted this variant as pathogenic or likely pathogenic">
##INFO=<ID=scv_with_criteria,Number=1,Type=String,Description="List of assertions using criteria (SCV_accession|assertion)">
##bcftools_annotateVersion=1.9+htslib-1.9
##bcftools_annotateCommand=annotate -x FORMAT/AO,FORMAT/RO,FORMAT/QA,FORMAT/QR,INFO/AN,INFO/AO,INFO/RO,INFO/AB,INFO/ABP,INFO/AC,INFO/AF,INFO/CIGAR,INFO/DP,INFO/DPB,INFO/DPRA,INFO/MEANALT,INFO/MIN_DP,INFO/NS,INFO/NUMALT,INFO/TYPE,INFO/technology.Illumina -a /projects/sequence_analysis/exome-pipeline/clinvar-vcf-grch38/ClinVar.GRCh38.vcf.gz -c INFO/clinvar_variation_id,INFO/clinvar_asserted_pathogenic,INFO/scv_with_criteria -Ob -o annotated-filtered/FES-0109.fb.splitmulti.clinvar.bcf snpeff/samp1.fb.splitmulti.bcf; Date=Tue Oct 15 19:11:33 2019
##INFO=<ID=GNOMAD_AC,Number=A,Type=Integer,Description="Alternate allele count for samples">
##INFO=<ID=GNOMAD_AC_popmax,Number=A,Type=Integer,Description="Allele count in the population with the maximum AF">
##INFO=<ID=GNOMAD_AF,Number=A,Type=Float,Description="Alternate allele frequency in samples">
##INFO=<ID=GNOMAD_AF_popmax,Number=A,Type=Float,Description="Maximum allele frequency across populations (excluding samples of Ashkenazi, Finnish, and indeterminate ancestry)">
##INFO=<ID=GNOMAD_popmax,Number=A,Type=String,Description="Population with maximum AF">
##bcftools_annotateCommand=annotate -e 'DP<11 || QUAL<10' -a /projects/sequence_analysis/exome-pipeline/gnomad-grch38/gnomad.exomes.r2.1.1.sites.slim.refseq38.vcf.gz -c INFO/GNOMAD_AC:=INFO/AC,INFO/GNOMAD_AC_popmax:=INFO/AC_popmax,INFO/GNOMAD_AF:=INFO/AF,INFO/GNOMAD_AF_popmax:=INFO/AF_popmax,INFO/GNOMAD_popmax:=INFO/popmax -Ob -o annotated-filtered/samp1.fb.splitmulti.clinvar.gnomad.bcf annotated-filtered/samp1.fb.splitmulti.clinvar.bcf; Date=Tue Oct 15 19:11:51 2019
...
#CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  samp1-2      samp1-0      samp1-1

```
Now we have a lot more information (though I haven't shown it all here)! Let's go to some exercises to think about what we're seeing here. 


### Exercise 1

How many lines are in the header? 

Will this always be the same in every VCF file? Why or why not? Which strategy do you think is a better way to view the header based on your answer? 

What would happen if our variant file has a '#' character somewhere other than the header? Somewhere other than the beginning of the line? Re-write the command to make sure we only retrieve entries with a '#' character at the beginning of the line. 

_Remember, you can refer to the regular expression cheatsheet in this repository for help, or turn to our friend Google._





```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
**Bold** _Italic_ `Code` text

[Link](url) and ![Image](src)

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
