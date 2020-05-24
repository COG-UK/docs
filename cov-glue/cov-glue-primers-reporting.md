---
layout: docpost
title: Reporting primer and probe mismatches using CoV-GLUE
date_published: 2020-05-24 11:45:00 +0000
date_modified:  2020-05-24 11:45:00 +0000
author: joshsinger
maintainer: joshsinger
---

# Overview 

This bioinformatics procedure analyses a SARS-CoV-2 sequence to compare it 
with a range of published primer/probe designs for sequencing and diagnostics assays. 

## Getting started

Follow the instructions for [Accessing CoV-GLUE on CLIMB](climb-glue.md) to ensure sure you have your own
personal instance of offline CoV-GLUE on CLIMB. You can use either the `cov_glue` or `coguk_cov_glue` project installations for this analysis, it does not matter which.

## Input data
As input, you need to supply consensus FASTA sequences.

From the CLIMB-GLUE server you should be able to access data on the path: `/cephfs/covid/`

You could copy FASTA files you want to analyse from here to your home directory on this server. Or, you can upload your own data, e.g. using the `scp` command. You will need to have write access in the directory where these FASTA sequences are located.

## Generate an HTML report for a FASTA file containing a single sequence

This is similar to the functionality available on the [CoV-GLUE web application](http://cov-glue.cvr.gla.ac.uk). Start GLUE using `gluetools.sh` in the the directory containing your FASTA sequence.
Then do:

```
GLUE> project cov
GLUE> module covPrimerProbeMismatch invoke-function reportSingleFasta <fastaFileName>
```

This will output an HTML report with the suffix `ppReport.html` in the same directory as the FASTA file. To quit out of GLUE just use the `quit` command.

## Tabular reports for FASTA files containing multiple sequences

This entry point, only available with offline CoV-GLUE, is more convenient for generating reports for large sets of sequences. Start GLUE using `gluetools.sh` in the the directory containing your multi-FASTA file.
Then do:

```
GLUE> project cov
GLUE> module covPrimerProbeMismatch invoke-function reportMultiFasta <fastaFileName>
```

This will output two tab-delimited text files in the same directory as the FASTA file.
1. The file with the suffix `ppReport_summary.txt` summarises the number of issues in each sequence.
1. The file with the suffix `ppReport_issues.txt` gives details on each of the detected issues.



