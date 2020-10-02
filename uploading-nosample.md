---
layout: docpost
title: Uploading library and run metadata with Ocarina
date_published: 2020-09-28 16:30:00 +0000
date_modified:  2020-10-02 13:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

In the case where a sample has been transferred from one site to another to be sequenced, the sequencing site should not need to upload any biosample metadata.
This document describes how to upload library and sequencing metadata with Ocarina on the command line. **If you want to use the web-based metadata uploader to do this, [see the documentation here](https://metadata.docs.cog-uk.io/bulk-upload-1/library-run-metadata-only)**.


## Notes

* Do not relabel the sample, use the `central_sample_id` that was provided to you 
* Sequencing metadata consists of two parts: a library pool and a sequencing run. You must provide both to register a valid sequencing run. The library must be registered before the sequencing run.
* If the sample has been sent to you from WSI for backlog sequencing, you **should never upload the biosample metadata**.

## Uploading metadata with Ocarina

### 0. Install Ocarina

Run the following command in your shell. You should be running python 3.7 and have `pip` installed.
Feel free to do this from a `virtualenv` or `conda` environment.

```
pip install git+https://github.com/samstudio8/ocarina.git
```

This will install the latest development version of Ocarina, which almost always works.

### 1. Configure Ocarina

[See the Ocarina README](https://github.com/SamStudio8/ocarina#configuration) for configuration instructions.
You will need your API key from your Majora profile.

### 2. Register a library

This `ocarina` command will register a sequencing library. You will need to replace the options with the relevant information.

```
ocarina put library --library-name "BIRM-20200326-1844" \
                --library-seq-kit "LSK109" \
                --library-seq-protocol "LIGATION" \
                --library-layout-config "SINGLE" \
                --biosamples HOOT-OCARINA-101 HOOT-OCARINA-102 \
                --apply-all-library VIRAL_RNA PCR AMPLICON MYPROTOCOL MYPRIMERS
```

* `library-name` is the name of the library pool, it needs to be unique and is only used to map sequencing runs to libraries
* `library-seq-kit` is the kit used for the library pooling
* `library-seq-protocol` is the protocol used for the library pooling
* `library-layout-config` should be `SINGLE` or `PAIRED`
* `biosamples` is a list of `central_sample_id` (COGIDs) that were pooled onto this sequencing library
* `apply-all-library` is an ordered set of properties applied to all samples, they must be filled in the following order:
    * `SOURCE` (e.g. VIRAL_RNA)
    * `SELECTION` (e.g. PCR)
    * `STRATEGY` (e.g. AMPLICON)
    * `PROTOCOL` the protocol you are using (e.g. `ARTIC`)
    * `PRIMERS` if you're using the ARTIC primer scheme, just enter the version number (e.g. `2` or `3`)
               

### 3. Register a sequencing run

This `ocarina` command will register a sequencing run. You will need to replace the options with the relevant information.

```
ocarina put sequencing --library-name BIRM-20200326-1844 \
                   --run-name "20200409-1840_MYRUN_000000_FAK12345" \
                   --instrument-make "OXFORD_NANOPORE" \
                   --instrument-model "GRIDION"
```

* `library-name` is the name of the library pool that you registered in the previous step (you must have registered the library first)
* `run-name` is the name of the sequencing run, as named by your sequencer
* `instrument-make` should be `OXFORD_NANOPORE` or `ILLUMINA`
* `instrument-model` is the model of your sequencer (e.g. `GRIDION`)

### Troubleshooting

* If `ocarina` reports a `STATUS CODE 400`, you have not authenticated correctly. Check the API key in your config file (`~/.ocarina`) has not expired.
* If you get the following message `At least one Biosample in your Library was not registered. No samples have been added to this Library. Register the missing samples, or remove them from your request and try again`, it indicates that your barcode is missing from Majora. **If the sample originated from WSI it is guaranteed they will exist, so this error indicates a barcode has been entered incorrectly in your request**.
* The library must be registered in order for the sequencing run to be registered.
* The order in which the `apply-all-library` parameter matters, any deviation from this will cause an error.
