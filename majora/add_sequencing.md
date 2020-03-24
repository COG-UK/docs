---
layout: docpost
title: api.process.sequencing.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-24 17:35:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example

```json
{
    "library_name": "BIRM-LIBRARY-20200322",
    "library_strategy": "AMPLICON",
    "library_source": "VIRAL RNA",
    "library_selection": "PCR",
    
    "biosamples": [
        "BIRM-XXXXX",
        "BIRM-YYYYY",
        "BIRM-ZZZZZ",
    ],
    
    "sequencing_id": "09ef4b3a-1bad-453a-a291-029ac9bd705d",
    "instrument_make": "OXFORD_NANOPORE",
}
```

### Reference

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| biosamples              |                               | **Yes**      | list[str] | The `central_sample_id` of each biosample in the library |
| instrument_make        |                               | **Yes**      | str        | **Options** `ILLUMINA`, `OXFORD_NANOPORE` |
| library_layout_config*        |                               | **Yes**      | str        | **Options** `SINGLE`, `PAIRED` |
| library_name    |                                    | **Yes**      | str, unique        | A unique, somewhat memorable name for your library. |
| library_selection*        |                               | **Yes**      | str        | **Options** `RANDOM`, `PCR` `RANDOM_PCR`, `OTHER` |
| library_source*        |                               | **Yes**      | str        | **Options** `GENOMIC`, `TRANSCRIPTOMIC`, `METAGENOMIC`, `METATRANSCRIPTOMIC`, `VIRAL_RNA`, `OTHER` |
| library_strategy*        |                               | **Yes**      | str        | **Options** `WGA`, `WGS`, `AMPLICON`, `OTHER` |
| library_seq_kit    |                                    | **Yes**      | str        | e.g. `LSK109` |
| library_seq_protocl    |                                    | **Yes**      | str   | e.g. `LIGATION`|
| library_sop_name    |                                    | **Yes**      | str   | e.g. `ARTIC nCov` |
| library_sop_version    |                                    | **Yes**      | str   | e.g. `v2`|
| sequencing_id        |                               | **Yes**      | uuid        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |
| library_layout_nominal_length*        |                               | No      | int        | Nominal length of sequencing library. Illumina runs only. |


* These fields are for ENA submission and use a subset of the valid options available. If a valid ENA option is not listed here but you need it, please contact `Sam Nicholls` to have it added.
