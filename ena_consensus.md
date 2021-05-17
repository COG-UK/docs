---
layout: docpost
title: Consensus sequence uploads to ENA
date_published: 2021-05-17 10:50:00 +0000
date_modified:  2021-05-17 10:50:00 +0000
author: samstudio8
maintainer: samstudio8
---

Following a huge effort from CLIMB-COVID, ENA and WSI; CLIMB-COVID can now automatically submit consensus sequences to ENA and the INSDC on your behalf.

## What do I need to do?

### Opt in
As with GISAID uploads you must opt-in from your [Institute profile](https://majora.covid19.climb.ac.uk/forms/institute/).
You must fill in the lab name, lab address and lab authors (even though they are labelled for GISAID).

### Provide basic bioinformatics information
The metadata uploader and Ocarina now have optional fields for describing the bioinformatics pipeline used to process the sequence:

* `bioinfo_pipe_name`
* `bioinfo_pipe_version`

These fields do not (currently) use a controlled vocabulary -- please send your comments and concerns about this to `#metadata` and not DIPI or the Data Working Group.
We do however recommend using the following entries for commonly used pipelines:

| Pipeline | `bioinfo_pipe_name` | `bioinfo_pipe_version` |
|----------|---------------------|------------------------|
| ARTIC pipeline tools (ONT) | ARTIC fieldbioinformatics (minimap2/nanopolish) | X.Y.Z (nanopolish X.Y.Z) |
| ARTIC Connor Lab Nextflow (Illumina) | ncov2019-artic-nf (BWA/ivar) | X.Y.Z (ivar X.Y.Z) |
| ARTIC Connor Lab Nextflow (ONT) | ncov2019-artic-nf (fieldbioinformatics/minimap2/nanopolish) |  X.Y.Z (nanopolish X.Y.Z) |

This list will be updated for additional pipelines as needed.

For further information see the [CGPS uploader documentation](https://metadata.docs.cog-uk.io/bulk-upload-1/samples-and-sequencing), or the [Majora/Ocarina documentation](https://samstudio8.github.io/majora-docs/#add-a-sequencing-run-to-majora).

## What will be uploaded?

Unlike GISAID which only receives High QC PASS seqeunces, ENA/INSDC will receive all Basic QC PASS sequences for deposition.
Sequences will only be uploaded if:

* The site has opted-in and provided the relevant authorship information
* The sequence has non-empty, non-default entries for `bioinfo_pipe_name` and `bioinfo_pipe_version`
* The raw reads BAM has been deposited into ENA (this should happen but there are rare cases where the upload files that need manual intervention)

As of May 2021, we are currently uploading prospective data. Existing sequences will need the bioinformatics fields backfilled to be eligible for upload and we will work on a solution for this.

## What if I have bad data?

You should [use Ocarina to suppress any bad sequences](suppress-pag) before they are uploaded into public databases.

## When will this happen?

ENA consensus depositions will happen weekly after the ENA raw data has been accessioned to allow for linking.
