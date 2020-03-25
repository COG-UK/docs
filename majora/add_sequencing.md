---
layout: docpost
title: api.process.sequencing.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-25 10:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example

```json
{
    "library_name": "BIRM-LIBRARY-20200322",

    "library_seq_kit": "LSK109",
    "library_seq_protocol": "LIGATION",
    "library_layout_config": "SINGLE",
    "library_layout_read_length": 0,
    "library_layout_insert_length": 0,

    "metadata": {
        "sop": {
            "name": "ARTIC nCov-2019",
            "version": 2,
            "amplicons": 3,
        }
    }


    "biosamples": [
        {
            "central_sample_id": "BIRM-XXXXX",
            "barcode": "01",
            "library_selection": "PCR",
            "library_source": "VIRAL_RNA",
            "library_strategy": "AMPLICON",
        },
        {
            "central_sample_id": "BIRM-YYYYY",
            "barcode": "02",
            "library_selection": "PCR",
            "library_source": "VIRAL_RNA",
            "library_strategy": "AMPLICON",
        },
        {
            "central_sample_id": "BIRM-ZZZZZ",
            "barcode": "03",
            "library_selection": "PCR",
            "library_source": "VIRAL_RNA",
            "library_strategy": "AMPLICON",
        },
    ],

    "runs": [
        {
            "sequencing_id": "09ef4b3a-1bad-453a-a291-029ac9bd705d",
            "instrument_make": "OXFORD_NANOPORE",
            "instrument_model": "GridION",
            "flowcell_type": "R9.4.1D",
            "flowcell_id": "00000",
            "start_time": "YYYY-MM-DD HH:MM:SS",
            "end_time": "YYYY-MM-DD HH:MM:SS",

        },
        {
            "sequencing_id": "2f3b14e7-7f60-4442-a199-71eee0b52e6c",
            "instrument_make": "OXFORD_NANOPORE",
            "instrument_model": "GridION",
            "flowcell_type": "R9.4.1D",
            "flowcell_id": "00000",
            "start_time": "YYYY-MM-DD HH:MM:SS",
            "end_time": "YYYY-MM-DD HH:MM:SS",
        },
        {
            "sequencing_id": "82c9831c-fe2f-4c3c-9655-611ba1f13fec",
            "instrument_make": "OXFORD_NANOPORE",
            "instrument_model": "GridION",
            "flowcell_type": "R10.3",
            "flowcell_id": "00001"
            "start_time": "YYYY-MM-DD HH:MM:SS",
            "end_time": "YYYY-MM-DD HH:MM:SS",
        },
    ]
}
```

### Reference

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| biosamples              |                               | **Yes**      | list[ str: {}] |  |
| library_layout_config*        |                               | **Yes**      | str        | **Options** `SINGLE`, `PAIRED` |
| library_name    |                                    | **Yes**      | str, unique        | A unique, somewhat memorable name for your library. |
| library_seq_kit    |                                    | **Yes**      | str        | e.g. `LSK109` |
| library_seq_protocol    |                                    | **Yes**      | str   | e.g. `LIGATION`|
| runs              |                               | **Yes**      | list[ str: {}] |  |
| library_layout_insert_length*        |                               | No      | int        | Nominal length of sequencing library insert. Illumina runs only. If left blank we will try and infer it from uploaded data. |
| library_layout_read_length*        |                               | No      | int        | Nominal length of sequencing library reads. Illumina runs only. If left blank we will try and infer it from uploaded data. |


Each `biosample` is an object that contains the following keys:

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| central_sample_id    | coguk_sample_id               | **Yes**      | str        | The centrally generated "Heron" barcode assigned to this sample. This biosample must have already been added to Majora. |
| library_selection*        |                               | **Yes**      | str        | **Options** `RANDOM`, `PCR` `RANDOM_PCR`, `OTHER` |
| library_source*        |                               | **Yes**      | str        | **Options** `GENOMIC`, `TRANSCRIPTOMIC`, `METAGENOMIC`, `METATRANSCRIPTOMIC`, `VIRAL_RNA`, `OTHER` |
| library_strategy*        |                               | **Yes**      | str        | **Options** `WGA`, `WGS`, `AMPLICON`, `OTHER` |
| barcode        |                               | **No**      | str        | Optional reference to barcode adapter or barcode number |

Each `run` is an object with the following keys:

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| sequencing_id        |                               | **Yes**      | uuid        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |
| instrument_make*        |                               | **Yes**      | str        | **Options** `ILLUMINA`, `OXFORD_NANOPORE` |
| instrument_model*        |                               | **Yes**      | str        | **Options** `GridION` |
| end_time        |                               | No      | str        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |
| flowcell_id        |                               | No      | str        | Flowcell serial number |
| flowcell_type        |                               | No      | str        | Flowcell description |
| start_time          |                               | No      | str        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |

* These fields are for ENA submission and use a subset of the valid options available. If a valid ENA option is not listed here but you need it, please contact `Sam Nicholls` to have it added.
