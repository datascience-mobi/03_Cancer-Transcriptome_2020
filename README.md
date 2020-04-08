Project 3: Cancer Transcriptome Analysis
========================================

- [Project: Cancer Transcriptome Analysis](#project-cancer-transcriptome-analysis)
  - [Introduction](#introduction)
  - [Objectives](#objectives)
  - [Datasets](#datasets)
  - [Recommended Literature](#recommended-literature)
    - [NGS/RNA-seq](#ngsrna-seq)
    - [The ICGC project](#the-icgc-project)
  - [How to structure your project](#how-to-structure-your-project)
    - [Project proposal](#project-proposal)
    - [Project](#project)
  - [Resources for programming (aka. what to do while stuck at home)](#resources-for-programming-aka-what-to-do-while-stuck-at-home)
    - [General resources for R](#general-resources-for-r)
    - [General resources for Git](#general-resources-for-git)
  - [Organization](#organization)

Supervisors:

- Matthias Schlesner (m.schlesne@dkfz-heidelberg.de)
- **Christian Heyer** (c.heyer@dkfz-heidelberg.de)
- **Dina ElHarouni** (d.elharouni@dkfz-heidelberg.de)

Tutor:
- TBD

## Introduction

High-throughput sequencing technologies have enabled the widespread analysis in many omics fields, providing an
unprecedented wealth of data for statistical analysis. However, once exception still remains in proteomics, where 
high-throughput techniques are still in the early stages of development. This makes the analysis of the RNA the closest 
point to protein biosynthesis which can be analyzed efficiently in a high throughput manner.

In cancer, it is essential to identify changes in the transcriptome to deduce the impact of cancer driver mutations and
identify upregulated signaling pathways playing a role in carcinogenesis. Understanding transcriptional processes in these
tumors is essential in bridging the gap between functional and molecular characterization of tumor diseases.

In this project, we will use the wealth of data provided by large tumor consortia (ICGC/TCGA) to identify deregulated genes
in tumor RNA-sequencing data and use statistical analysis to characterize and compare these data from healthy individuals using a public database.

## Objectives

Start off by getting used to R. The first steps have some concrete things to do, but you are expected to show some initiative in the later analysis steps once you get used to the data. 

- Start by getting used to R
  - Load the gene expression matrix into R and inspect it
  - Generate gene/sample level statistics using R
  - Load the metadata csv files into R. You will need them to:
    - Find out which Donor ID (DO....) is associated to which sample ID (SA...)
    - To get metadata and other clinical information for your samples.
  - Load and filter the GTEX data of healthy tissues fitting your data.
- Prepare your data for analysis. necessary steps including:
  - feature reduction/selection: Some features are more of interest to us than others. Find and apply an approach to reduce the number of features in your data.    
  - normalization
    - can you work directly on the read count data?
    - visualize basic statistics of your data
    - search for confounding features in your samples
- Dimensionality reduction to identify sources of variance in your data
  - Use dimensionality reduction to visualize your data and identify global trends. What are your expectations. Use the metadata to add information to your dimensionality reduction approach. 
    - Identify potential confounding factors in your data and discuss if there is any way to mitigate their impact.
- Differential expression analysis
  - identify differentially expressed genes in between tumor and control samples (not using a precompiled package)
    - Consider which pitfalls you need to correct for in order to avoid to many false positives/negatives. 
    - (optional) How could you get functional information out of your list of differentially expressed genes?
- Clustering/Classification
  - Discuss whether  you believe that different subgroups of samples are present in your data based on the analyses you have performed. 
  - How could you attempt to define subgroups in your data and identify them? What methods could be used based on which features. (Regression/Clustering etc.) 
  - If time allows. 
- Make a coherent report of your complete analysis and results using R markdown.



## Datasets

We will prepare a dataset for each group to analyze. Before the projects starts i will write a small wiki page for getting started with the data. Each dataset is a zip file uploaded to 
figshare. Download and unzip the data for your project + the GTEX data

- Breast [Figshare](https://figshare.com/s/4287b42869882bad7831)
- Lung [Figshare](https://figshare.com/s/708c7f05f99ed2d9099f)
- Colon/rectum [Figshare](https://figshare.com/s/34f62bb2ec511e6154f9)
- Skin [Figshare](https://figshare.com/s/a5963d1e5f133fe86bea)
- Liver [Figshare](https://figshare.com/s/f6b76e20845c5355c68c)
- GTEX tissue Reference data [Figshare](https://figshare.com/s/b63c7cf3b515772b711d)

The GTEX tissue reference data will function as a normal tissue sample baseline for differential expression analysis.

Structure of the zip file:

- (tissue)_exp.tsv.gz: 
  - Matrix of raw gene expression read counts for your samples + the gene name.
- donor.tsv.gz
  - Clinical information of the samples from ICGC.
- sample.tsv.gz
  - Sample information for the samples liste in the gene expression matrix
- simple_somatic_mutation_open.tsv.gz
  - Information on simple somatic mutations found in the samples/donors
- specimen.tsv.gz
  - Specimen information from ICGC.


Donors are linked to samples via: DonorID(DO...)-SpecimenID(SP...)-SampleID(SA..)
More information can be found at the [ICGC DCC documentation website](https://docs.icgc.org/).The breast cancer dataset has a few extra files, which you can use but don't have to. 

## Recommended Literature

Note: This is not a mandatory reading list!! I will link some introductory reading and i will not start quizzing you on the details
of these. See these as suggestions.

Instead, make sure you have a general understanding of high-throughput transcriptome analysis, starting from the 
how high-throughput sequencing works, what some of the problems/pitfalls are in RNA-sequencing and the statistical
basics of differential expression analysis. 

Each group should do some research on the tumor entity they are looking
at so make sure to read up on that as well.
You should check for:
 - Tumor subgroups that exist
 - known driver genes that can be upregulated
 - Basic knowledge about the tumor disease

### NGS/RNA-seq

If you need a refresher on NGS: [Coming of age: ten years of next-generation sequencing technologies](https://www.nature.com/articles/nrg.2016.49) 

[RNA sequencing: the teenage years](https://www.nature.com/articles/s41576-019-0150-2)

Technical review on RNA-seq data processing: [Computational methods for transcriptome annotation and quantification using RNA-seq](https://www.nature.com/articles/nmeth.1613)

Differential Expression analysis using bioconductor R packages: [Count-based differential expression analysis of RNA sequencing data using R and Bioconductor](http://www.nature.com/nprot/journal/v8/n9/full/nprot.2013.099.html)
Note: For your own analysis you are expected to write your own methods and not simply use those from a finished package.
However, it helps to see how differential expression analysis is done in general. 


### The ICGC project

All the data here was downloaded from the [ICGC Data Control Center](https://dcc.icgc.org). Each tumor sample used here has a specific donor id (DO...), a specimen ID (SP...)
and a sample ID (SA...) you will need to link these to each other in order to work with
the data. 

The ICGC is structured into projects based on location and tumor entity. Remember to 
consider the heterogeneity of the samples in your analysis. 

[Initial ICGC publication](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2902243/) 

## How to structure your project

### Project proposal

You first task will we to define a **project proposal**, which should
include

-   summary of literature on this dataset
-   questions you want to address
-   approximate timetable

Due to the ongoing stay at home order, we will provide information on how exactly we plan to implement this at a later time when the project launches. 

### Project

At a minimum, we expect you to cover the objectives listed in [objectives](#objectives).
For the R-markdown reports, do not create more than **30** A4 pdf pages. In case your report is 
getting to long, code can be omitted and saved in a separate file to be called
upon in the report. 

You project **MUST** contain/discuss the following elements:
- **descriptive statistics** about the datasets
- **graphical representations**
- **dimension reduction** analysis (PCA and related methods)
- **statistical tests** (t-test, proportion tests etc.)
- **clustering/classification analysis** (clustering/regression etc.) 


## Resources for programming (aka. what to do while stuck at home)

### General resources for R

- [R for Data Science](https://r4ds.had.co.nz/) (Combines R basics and introduction to statistical techniques in R/R Markdown)
- [Style Guidelines for R](http://adv-r.had.co.nz/Style.html) (Keep your code in a consistent format. Here is a short style guide you can consider using.)
- [Bioconductor](https://bioconductor.org/) (Large R bioinformatics software repository. While you are supposed to do the analysis yourself and not have package to it for you, there are also a bunch of useful packages for working with sequencing data f.e. for annotating the genome.)

In general you should now some R-basics. There is a ton options to learn R (or 
programming in general) and there is no one solution that works for everyone. In case 
you are having
trouble finding something, feel free to ask us ways to get started with R. 

### General resources for Git

- [Excellent git(hub) tutorial](https://github.com/jlord/git-it-electron) (Covers installation and working with github. If in a hurry to learn git basics do this.)
- [Long but comprehensive (and a little entertaining) step by step guide: git for userRs](https://happygitwithr.com/)
- [Git learning resources from Github](https://try.github.io/)
- [Git "flight rules"](https://github.com/k88hudson/git-flight-rules) (Compendium of git problems and how to solve them)
- [Quick setup for using git with Rstudio](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN)

## Organization

Due to the special situation due to the COVID-19 pandemic, personal meetings will not be 
possible for the time being. For organization, we plan to setup a Slack or Microsoft Teams workspace for communicating with 
us and the tutor. Feel free to use it for organizing yourselves also. 

I also heavily stress quickly getting used to working with Github and the Github workflow. Since you should not be meeting up in person, being able to collaborate on 
,the same project using git will be essential for success here. Take your time getting used to the git workflow and feel free to ask us in case you run into unsolvable problems.

How exactly we 
will do video conferencing will depend on what works but using skype,zoom etc. should be 
fine in any way. This will probably be something that will be organizing across all five 
projects so keep in eye for information there. Also how the presentations will be done 
is a question that will be decide for all groups together. As soon as we now we will communicate this to you.