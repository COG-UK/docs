---
layout: docpost
title: Consensus sequence uploads to ENA
date_published: 2021-05-17 10:50:00 +0000
date_modified:  2021-05-17 11:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

Following a huge effort from CLIMB-COVID, ENA and WSI; CLIMB-COVID can now automatically submit consensus sequences to ENA and the INSDC on your behalf.

## What do I need to do?

### Opt in
Previously users were required to opt-in to ENA assembly uploads, however as of 2023-04-27 this process is now automatic and users are automatically opted-in.

### Provide basic bioinformatics information
The metadata uploader and Ocarina now have optional fields for describing the bioinformatics pipeline used to process the sequence:

* `bioinfo_pipe_name`
* `bioinfo_pipe_version`

These fields do not (currently) use a controlled vocabulary -- please send your comments and concerns about this to `#metadata` and not DIPI or the Data Working Group.
We do however recommend using the following entries for commonly used pipelines:

| Pipeline                             | `bioinfo_pipe_name`                                         | `bioinfo_pipe_version`   |
| ------------------------------------ | ----------------------------------------------------------- | ------------------------ |
| ARTIC pipeline tools (ONT)           | ARTIC fieldbioinformatics (minimap2/nanopolish)             | X.Y.Z (nanopolish X.Y.Z) |
| ARTIC Connor Lab Nextflow (Illumina) | ncov2019-artic-nf (BWA/ivar)                                | X.Y.Z (ivar X.Y.Z)       |
| ARTIC Connor Lab Nextflow (ONT)      | ncov2019-artic-nf (fieldbioinformatics/minimap2/nanopolish) | X.Y.Z (nanopolish X.Y.Z) |

This list will be updated for additional pipelines as needed.

For further information see the [CGPS uploader documentation](https://metadata.docs.cog-uk.io/bulk-upload-1/samples-and-sequencing), or the [Majora/Ocarina documentation](https://samstudio8.github.io/majora-docs/#add-a-sequencing-run-to-majora).

## What will be uploaded?

Unlike GISAID which only receives High QC PASS seqeunces, ENA/INSDC will receive all Basic QC PASS sequences for deposition.

## What if I have bad data?

You should [use Ocarina to suppress any bad sequences](suppress-pag) before they are uploaded into public databases.

## When will this happen?

ENA consensus depositions occur daily in the working week (Monday - Friday) but sequences are not uploaded immediately to allow some time for errors to be corrected prior to upload to external databases where corrections are much harder. Samples are uploaded 3 days after they are ingested into the CLIMB-COVID dataset.

## CHANGELOG

* 2023-09-06: Upload lag changed to 3 days, down from >7 days.
* 2023-12-04: Consensus fasta sequences are now sanitised on upload to ENA to remove illegal characters (characters except: A, C, G, T, a, c, g, t, N)