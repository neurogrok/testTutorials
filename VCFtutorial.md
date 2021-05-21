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

That looks promising! We can see some useful information, like what version of the variant format this data adheres to (line 1), when the file was generated (line 3), what software was used to make the variant calls (line 4), and what species and version of the genome was used as a reference (line 5). But maybe we aren't seeing the whole header? Think about how you might discover this information, and we'll do an exercise to answer that question soon. 

2. A second strategy to view the header might be to pull out the lines beginning with '##'. We know that 'grep' will help us pull out specific data. Let's try that. 

```console
foo@bar:~$ grep # myVCF.vcf


```
Oops! This didn't do exactly what we wanted. We need to specify that the character starts the line. Remember, you can find help with regular expressions by referring to the cheatsheet in this repository (or our favorite friend, Google). 

```console
foo@bar:~$ grep # myVCF.vcf


```

### Exercise 1

How many lines are in the header? 

Will this always be the same in every VCF file? Why or why not? Which strategy do you think is a better way to view the header based on your answer? 



**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/neurogrok/testTutorials/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
