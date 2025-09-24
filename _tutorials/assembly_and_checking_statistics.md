---
layout: archive
title: "Assembly and Checking Statistics"
permalink: /tutorials/assembly_and_checking_statistics/
---



## Overview

Simply put, assembly refers to taking all of our short read sequences and attempts to put them together into longer **contiguous sequences** - also called **contigs**. These programs are trying to find overlapping segments between these different sequences to string together as long a contig as possible. A perfect circular genome would be considered 1 complete contig, however, this is incredibly rare in "shotgun" metagenomic sequencing because of how broken apart the reads become. Instead, our goal is to aim for as large contigs as possible and limiting the overall number of contigs we observe. So it is likely that our reconstructed genomes may be made out of many contigs and likely with some gaps that lead to a nearly complete genome.

There is no perfect strategy for assembly. It is usually best to try out a few methods and then see which results in the most successful assembly for your study's purposes. We are going to try assembling with two different assemblers: `SPAdes` and `megahit`. We will also feed each program the non-error and error-corrected reads to see how they compare. So in total, we will compare 4 different assembly strategies and then assess which method worked best with `QUAST`. 


Another way to think about this is the book analogy: if we broke a book down into all of the individual words you might be able to string some sentences together but may not be able to complete the book in the correct order. By taking portions of each sentence or letters and finding overlap, we can more successfully string together full sentences, pages, and eventually the whole book (genome)!


## K-mers and de Brjuin Graphs

The main concept for understanding how these assemblers work is using k-mer overlaps. A k-mer just represents the length of the base pair sequence we are interested in. For instance, a 33-mer would represent sequence length of 33 base pairs, while a 121-mer would mean a length of 121 base pairs. Each of our assemblers will use a different length set of k-mers to better understand overlap between our sequences.

The other tool assemblers typically use is a de Brujin graph. We will not deep dive on this topic, but it is a sophisticated algorithm to make non-dimensional graphs to understand the relationship of different sequences and how they may string together to form different contigs. Both `SPAdes` and `megahit` use de Brujin graphs, but `megahit` uses a simplified model that allows it to be less memory intensive (sometimes at the cost of being less advantageous in the final assembly metrics). We will run both assemblers to see if there is a difference when assembling our sequences!


## Assembly Statistics

We can use the tool `QUAST` to assess how our different assembly methods worked. It is important to keep in mind different features such as the number of contigs, largest contig, number of contigs above given sizes, and other metrics that are shown from the program. Two specific metrics we would like you to think about when assessing your assemblies are:


**N50** = the minimum contig length that makes up 50% of the assembly. (At least half of the nucleotides in the assembly belong to this contig length or longer).

**L50** = the smallest number of contigs needed to reach this N50 value


It can be tricky to try and understand how the assembly statistics might indicate which program's outcome is better suited for your study. With that in mind, here are some guiding questions:

*1 - Are you assembling an isolate or a mixed/enrichment community? How might this affect the number of contigs you observe and also the N50 or L50 values?*

*2 - Are the majority of your contigs long or short?*

*3 - What is the average gene length for bacteria or archaea?*
