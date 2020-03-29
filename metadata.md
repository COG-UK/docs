---
layout: docpost
title: Providing metadata
date_published: 2020-03-29 22:30:00 +0000
date_modified:  2020-03-29 22:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

# Basics and terminology

* A **biosample** refers to a single, physical sample taken from a patient or environment, such as a swab. It should be assigned a COGUK identifier as soon as possible.
* A **COGUK identifier** (alternatively known as a Heron barcode, or central sample ID) is a randomly generated string prefixed with a four letter site name. Where it is impractical for a site to use these identifiers, you may use your own, providing that you use those identifiers consistently.
* A **biosample source** refers to the physical patient or environment from where a sample was taken.
It is not possible (for various reasons) for a patient to be identified with a single, unique, shareable identifier when a sample is made available to the consortium.
It is our intention that working between the health agencies, the NHS and HDR-UK, that such identifiers can be made available to the project in the near future.

* To ensure a biosample can be correctly matched to its biosample source later, we must try to record:
    * If possible, the **PHx sample ID**: an identifier assigned to the sample by a health agency. For example, in this context, Public Health England samples IDs are prefixed with `H20`.
    * Otherwise, a **local lab ID**: this could be any identifier used at the hospital or point of origin. Ideally this identifier will be used by the hospital to submit information about positive samples to SGSS. You must ensure you have permission to use these identifiers in case they are considered personally identifiable.
* Providing these identifiers is not a requirement of the consortium, but consider that being unable to provide them will mean it is unlikely they will ever be linked back to their source.
* Where possible, the **local lab ID** should be an identifier that can be mapped quickly and securely. Sites should not be encouraged to hold this linkage information themselves.

* Where a patient or environment has been **sampled multiple times**: each biosample should have its own COGUK identifier. You can use the *first* COGUK identifier for that patient or environment as the **biosample source** as a means to link them together in the interim.
* Where a biosample is split into **multiple aliquots** or **shared with other sequencing centres**, that biosample **should not be relabelled** by the receiving site. This ambiguity can be resolved later by providing a library and sequencing run name that corresponds to your site.

* A **library** is a collection of extracted and processed **biosamples** that have been prepared for simultaneous sequencing.
* A **sequencing run** corresponds to the sequencing of a single library. *e.g.* A flowcell.

* Insufficient metadata will preclude the use of your sample in downstream analyses and project reports. It may also prevent automated uploading of your data to ENA and GISAID.

## Reporting standards for the consortium

### Biosamples

For a sample to be accepted for upload to CLIMB, and used in downstream analyses, you must provide the following:

* A single, unique, shareable identifier the "COGUK ID" (either a Heron barcode, or a suitable barcode from your own lab)
* Country of origin (UK-ENG, UK-SCT, UK-WLS, UK-NIR)
* Either a sample collection date (YYYY-MM-DD) **or** a sample `received_date` (YYYY-MM-DD). Do not attempt to impute the collection date. You must provide the day of the month.
* A GISAID strain ID and strain identifier **if** you have already made the sequence available on GISAID yourself

You should aim to provide as much information as possible about a sample to the consortium. 
[See a full list of fields that have been deemed acceptable for the consortium to collect](majora/add_sample).

### Libraries

For a library to be listed on CLIMB, you must provide the following:

* A unique library name
* One or more COGUK IDs that refer to the biosamples that were pooled into the library
    * Additionally, for each biosample you must provide the library source, selection and strategy.
* The sequencing kit
* The sequencing protocol
* Whether the run has single or paired reads

You *should* also provide information pertinent to performing QC and filtering on your downstream analyses here, such as the version of the ARTIC protocol and primer pools (if used).

[See more information on library metadata](majora/add_library).

### Sequencing Runs

* A unique run name
* The corresponding library name
* The sequencing instrument make and model

The API will allow you to tag your sequencing runs with arbitrary key value pairs if you wish to provide more information about your sequencing run, or the downstream bioinformatics.

[See more information on run metadata](majora/add_sequencing).


## Metadata storage

Metadata is stored by `Majora`. [You can log into Majora](https://majora.covid19.climb.ac.uk/) with your CLIMB unified account. New users [should register](https://majora.covid19.climb.ac.uk/forms/register) and wait to have their account approved by the system administrators.

## Methods for metadata submission

Metadata can be submitted in three ways:
* By uploading a spreadsheet, or CSV/TSV file to [cog-uk.io](https://docs.cog-uk.io/metadata/)
* Via our [`ocarina` command line tool](https://github.com/SamStudio8/ocarina/)
* By sending POST requests to our [JSON endpoints directly](https://docs.covid19.climb.ac.uk/majora-api)

We anticipate that sites will find using the CSV/TSV interface for uploading biosamples the most straightforward, and the `ocarina` command line tool for providing library and sequencing information. Advanced users are welcome to communicate with the API directly.
