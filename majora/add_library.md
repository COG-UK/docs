---
layout: docpost
title: api.artifact.library.add
date_published: 2020-03-25 20:00:00 +0000
date_modified:  2020-03-25 20:00:00 +0000
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
        "artic": {
            "protocol": "bbmuik6w",
            "primers": 3,
        }
    },

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
| library_layout_insert_length*        |                               | No      | int        | Nominal length of sequencing library insert. Illumina runs only. If left blank we will try and infer it from uploaded data. |
| library_layout_read_length*        |                               | No      | int        | Nominal length of sequencing library reads. Illumina runs only. If left blank we will try and infer it from uploaded data. |
| metadata | | No | { str: { str: str, ... }} | Arbitrary metadata |

Each `biosample` is an object that contains the following keys:

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| central_sample_id    | coguk_sample_id               | **Yes**      | str        | The centrally generated "Heron" barcode assigned to this sample. This biosample must have already been added to Majora. |
| library_selection*        |                               | **Yes**      | str        | **Options** `RANDOM`, `PCR` `RANDOM_PCR`, `OTHER` |
| library_source*        |                               | **Yes**      | str        | **Options** `GENOMIC`, `TRANSCRIPTOMIC`, `METAGENOMIC`, `METATRANSCRIPTOMIC`, `VIRAL_RNA`, `OTHER` |
| library_strategy*        |                               | **Yes**      | str        | **Options** `WGA`, `WGS`, `AMPLICON`, `OTHER` |
| barcode        |                               | No      | str        | Optional reference to barcode adapter or barcode number |


Additionally, one may optionally provid metadata for a library inside a `metadata` key.
Each object inside `metadata` will be created as a tag to hold one or more key: value pairs.

You can specify any tags you like. However, the following tags are used within the project and should be followed if you want to provide this information meaningfully.

| Tag         | Name      | Description                           |
|-------------|-----------|---------------------------------------|
| `artic`     | `primers` | The version of primers used: `1` `2` or `3` |
| `artic`     | `protocol`| The version of the lab protocol used |

All metadata is optional. Metadata can be updated at any time.

* These fields are for ENA submission and use a subset of the valid options available. If a valid ENA option is not listed here but you need it, please contact `Sam Nicholls` to have it added.
