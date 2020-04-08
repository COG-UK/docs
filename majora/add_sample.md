---
layout: docpost
title: api.artifact.biosample.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-04-06 15:40:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example
```json
{
    "biosamples": [
        {
            "adm1": "UK-ENG",
            "central_sample_id": "BIRM-XXXXX",
            "collection_date": "2020-03-22",
            "source_age": 29,
            "source_sex": "M",
            "secondary_accession": "EPI_ISL_XXXXXX",
            "secondary_identifier": "hCov-19/England/Patient0/2020",
            "adm2": "WEST MIDLANDS",
            "collecting_org": "Queen Elizabeth Hospital Birmingham",
            "root_sample_id": "H20XXXXXXXX",
            "sample_type_collected": "swab",
            "sender_sample_id": "QELAB-01",
            "swab_site": "nose",
            
            "metadata": {
                "epi": {
                    "cluster": "my cluster identifier",
                }
            }
        },
        {...},
    ],
}
```

### Reference

`biosamples` is the only mandatory key, which is a **list** that may contain **one or more** objects with the following structure:


| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| adm1          | adm1_region                              | **Yes**      | str | **Options** `UK-ENG`,`UK-SCT`,`UK-WLS`,`UK-NIR`|
| central_sample_id    | coguk_sample_id               | **Yes**      | str        | The centrally shared ID that you will use to refer to this sample inside the consortium. |
| received_date      |                               | **Yes**, if collection_date not available      | str | The date the sample was received. **YYYY-MM-DD** only. |
| secondary_accession     | gisaid_accession              | **Yes**, if in GISAID | str | GISAID accession if the sample has already been uploaded to GISAID |
| secondary_identifier    | gisaid_identifier             | **Yes**, if in GISAID | str | GISAID identifier (eg. hCov-19/.../2020) if the sample has already been uploaded to GISAID
| adm2          | adm2_county                              | No       | str        | The county that the patient lives in (no abbreviations or short hand) |
| adm2_private          | adm2_postcode                              | No       | str        | The outer postcode for the patient's home address (**first half of the postcode only**) |
| biosample_source_id  |                               | No       | str        | Unique identifier of patient or environmental sample. **Do not use an NHS number here**. This field will be backfilled later by PHx and HDR-UK. |
| collection_date      |                               | No      | str | The date the sample was collected. **YYYY-MM-DD** only. |
| collecting_org       |                               | No       | str       | The site (eg. hospital or surgery) that this sample was originally collected by. Use the first line of the 'sender' from the E28 form.
| root_sample_id       | phx_sample_id                 | No       | str        | Identifier assigned to this sample from one of the health agencies (eg. PHE samples will be prefixed with `H20`). This is necessary for linking samples to private patient metadata later. |
| sample_type_collected          |                               | No       | str | Sample type. **Options** `dry swab`, `swab`,`sputum`,`BAL`,`aspirate`|
| sample_type_received         |                               | No       | str | Sample type. **Options** `primary`,`extract`,`culture`|
| sender_sample_id     | local_sample_id               | No      | str        | If this sample was renamed by a local organisation (eg. hospital virology lab, sequencing lab), provide this identifier here. Otherwise leave blank. |
| source_age           |                               | No      | int        | Age of the patient in years |
| source_sex           |                               | No      | str | Sex of the patient. **Options** `F`,`M`,`Other` |
| swab_site            |                               | No       | str | Swab site. **Options** `nose`,`throat`,`nose-throat`|


Additionally, one may optionally provid metadata for a biosample using the `metadata` key.
Each object inside `metadata` will be created as a tag to hold one or more key: value pairs.

You can specify any tags you like. However, the following tags are used within the project and should be followed if you want to provide this information meaningfully.

| Tag         | Name      | Description                           |
|-------------|-----------|---------------------------------------|
| `epi`     | `cluster` | A local identifier for a known case cluster |

All metadata is optional. Metadata can be updated at any time.


The following fields are also required, but are submitted automatically. **You do not need to provide these fields**.

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| submitting_user |              | Yes, but provided automatically       | str        | Your username 
| submitting_org  |              | Yes, but provided automatically       | str        | Your organisation

### Frequently asked questions

* Ages should be whole numbers. Neonatals should be entered as 0. Leave the field blank for not recorded.
