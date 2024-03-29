---
layout: docpost
title: Accessing data
date_published: 2020-03-29 23:20:00 +0000
date_modified:  2021-09-22 14:00:00 +0000
author: samstudio8, BioWilko
maintainer: samstudio8, BioWilko
---

## Using public sources to access samples that have passed high-quality QC

* FASTA are routinely uploaded to  [GISAID](https://gisaid.org/), and are also downloadable from the [consortium data page](https://www.cogconsortium.uk/data/).
* Aligned BAMs are further purged of potential human reads and uploaded to [ENA Project PRJEB37886](https://www.ebi.ac.uk/ena/data/view/PRJEB37886)

## Using CLIMB to access FASTA, BAM and metadata for samples that have passed basic QC

You need a CLIMB account to upload or access data. If you haven't got one, [see instructions on registering](register).
You will need to SSH into the CLIMB-COVID server.

* Sequences are concatenated together each day and can be found at `/cephfs/covid/bham/artifacts/published/elan.latest.consensus.matched.fasta`. The daily consensus FASTA is indexed to make sequence extraction quick, a simple script which allows you to do so using a list (or file) of either `central_sample_id`, `run_name`, `pag_name` or `central_sample_id, run_name` pairs is available from the [CLIMB-COVID/utilities repository](https://github.com/CLIMB-COVID/utilities).
* Individual `bam` / their associated `bam.bai` locations must be resolve via a the lookup table (`/cephfs/covid/artifacts/elan/latest/majora.pag_lookup.tsv`) which will be updated by Elan daily.
* Basic metadata is provided in the table `/cephfs/covid/bham/artifacts/published/majora.latest.metadata.matched.tsv`
* COG-ID to public accession mappings are provided in `/cephfs/covid/bham/artifacts/published/latest.accessions.tsv`
* Datapipe output can be found in `/cephfs/covid/bham/results/msa/latest/alignments/` which consists of:
    * `cog_<date>_all.fa` : all unaligned sequences after deduplication
    * `cog_<date>_all_alignment.fa` : all aligned sequences after deduplication
    * `cog_<date>_all_metadata.csv` : all corresponding metadata
    * `cog_<date>_alignment.fa` : filtered, trimmed alignment with sequences matching those in the corresponding metadata
    * `cog_<date>_metadata.csv` : corresponding metadata for filtered, trimmed alignment
* Asklepian output can be found in `/cephfs/covid/bham/results/variants/YYYYMMDD/` (only the latest run is kept, this may be the current date or yesterdays date depending on time) this contains:
    * `naive_variants_table.csv`: A long format table containing all variant information (SNPS / indels) on every COG ID within `best_refs.paired.ls`
    * `naive_msa.fasta`: The MSA used to generate `naive_variants_table.csv` 
    * `best_refs.paired.ls`: A summary file containing the filename for the source fasta file included in the MSA and its original fasta header

The FASTA consensus and metadata table are perfectly paired. The sequence records in the FASTA and metadata rows in the table are in the same order.
Additionally, the table contains a `fasta_header` column that can be used to map the records in the FASTA file. Note that the order is not guaranteed between different runs of the pipeline (i.e., the FASTA will not be in the same order each time the inbound pipeline finishes).

Note also that the merged consensus FASTA will also include resequencing. That is, a biosample may have more than one genome in the consensus FASTA.

## Accessing restricted metadata through the controlled Majora data view API

See [accessing dataviews](accessing-dataviews).
