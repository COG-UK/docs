---
layout: docpost
title: Accessing and using CLIMB data
date_published: 2020-03-29 23:20:00 +0000
date_modified:  2020-03-29 23:20:00 +0000
author: samstudio8
maintainer: samstudio8
---

# Basics
## The CLIMB QC pipeline

Data uploaded by users to CLIMB with sufficient metadata is periodically pulled through the [`elan` nextflow pipeline](https://github.com/SamStudio8/elan-nextflow).
`elan` is responsible for basic quality checking including the following:

* Filtering unmapped reads and sorting uploaded BAMs (to ensure this step is done)
* Ensuring the BAM is valid with `samtools quickcheck`
* Counting the proportion of non-ambiguous, ambigious and invalid bases in the consensus FASTA
* Counting the proportion of positions in the aligned BAM that are above certain coverage thresholds
* Where applicable, checks the depth of tiles amplified by the ARTIC protocol

Once `elan` has finished, the following artifacts are automatically published with a version number:

* `fasta`: All consensus FASTA with the naming strategy `<coguk_id>.fasta`
* `alignment`: Each filtered, sorted and checked BAM with the naming strategy `<coguk_id>.climb.bam`
* `qc`: A basic quality report for each COGUK ID.

## Pulling your own copy of the CLIMB data

You need a CLIMB account to upload or access data. If you haven't got one, [see instructions on registering and uploading to CLIMB](upload-instructions).

You can grab a copy of artifacts that meet some basic quality thresholds of your choosing with the [`elan-pull` nextflow pipeline](https://github.com/SamStudio8/elan-pull-nextflow).
You can use the pipeline directly from GitHub:

```
nextflow run samstudio8/elan-pull-nextflow --location DATA_DIR
```

You must run this command on CLIMB.
