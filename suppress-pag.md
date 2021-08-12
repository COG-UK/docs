---
layout: docpost
title: Suppressing sequences inside COG
date_published: 2020-12-09 15:30:00 +0000
date_modified:  2021-08-11 11:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

## When to suppress sequences through the API

You should use the Ocarina client to suppress sequences from the COG data set if:

* You think the sequence is contaminated or should not have passed QC
* The sequence is labelled with the wrong barcode or should not have been uploaded at all

## What happens when sequences are suppressed through the API

Sequences marked as suppressed will effectively disappear from the downstream data set. The sequence on Majora will be marked as suppressed.
**Currently, suppressing a sequence with the API will not remove it from either GISAID nor ENA. You must arrange for sequences to be removed from GISAID by contacting them directly.** 
This will forever mark a (central_sample_id, run_name) pair as suppressed. If you want to replace a sequence without re-sequencing, you will need to upload a new run, and alter the run_name slightly.

## How to suppress a sequence

### 0. Install Ocarina

Set up Ocarina by following [these instructions](setting-up-ocarina)

### 1. Work out which Published Artifact Groups to suppress

When a sequence and biosample are united by Elan, the result is pushed to Majora and called a "Published Artifact Group" (PAG, for short).
PAGs are used to help distinguish sequences generated from the same sample, whether by multiple sequencing centres, multiple runs, or both.
PAGs are named in a predictable format, and you'll need to specify the exact PAG name to suppress your sequence. The format is as follows:

```
COG-UK/<SAMPLE_NAME>/<SEQUENCING_CENTRE>:<RUN_NAME>
```

For example: `COG-UK/BIRM-655FB/BIRM:20201012_1249_X1_FAO87316_8ae32d4f`.

You can use the Groups tab on your [Majora profile](https://majora.covid19.climb.ac.uk/accounts/profile/) to help locate the PAG name (or names).
Once identified, you can suppress the PAGs using the Ocarina client.

### 3. Suppress

Using the `ocarina pag suppress` command, pass your list of PAGs to suppress:

```
ocarina pag suppress --oauth --reason XXXX --publish-group 'COGUK\SAMPLE1\SITE:MY_FIRST_RUN' 'COGUK/SAMPLE2/SITE:MY_FIRST_RUN'
```

You must choose a reason to suppress with `--reason`, which can be one of the following: `WRONG_BARCODE`, `WRONG_METADATA`, `WRONG_SEQUENCE`, `CONTROL_FAIL`.

The API will respond with any problems inside the `messages` list. If you're using Ocarina, this will automatically be printed to your terminal.
You can verify the PAG has been suppressed via the Majora web interface.

### Further Reading

For more information see the [Majora documentation on the PAG suppress interface](https://samstudio8.github.io/majora-docs/#published-artifact-group)
