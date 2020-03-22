---
layout: docpost
title: `api.artifact.biosample.add`
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-22 21:50:00 +0000
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
            "sample_type": "swab",
            "sender_sample_id": "QELAB-01",
            "swab_site": "nose",
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
| central_sample_id    | coguk_sample_id               | **Yes**      | str        | The centrally generated "Heron" barcode assigned to this sample. If this sample does not have a Heron barcode, use the `root_sample_id`. |
| collection_date      |                               | **Yes**      | str | The date the sample was collected. **YYYY-MM-DD** only. |
| source_age           |                               | **Yes**      | int        | Age of the patient in years |
| source_sex           |                               | **Yes**      | str | Sex of the patient. **Options** `F`,`M`,`Other` |
| override_heron       |                               | **Yes**, if non-Heron ID           | str        | If you are using a `central_sample_id` that is not a Heron barcode, you must provide this key as `1` or `true` to prevent the identifier being validated |
| secondary_accession     | gisaid_accession              | **Yes**, if in GISAID | str | GISAID accession if the sample has already been uploaded to GISAID |
| secondary_identifier    | gisaid_identifier             | **Yes**, if in GISAID | str | GISAID identifier (eg. hCov-19/.../2020) if the sample has already been uploaded to GISAID
| adm2          | adm2_county                              | No       | str        | The county that the patient lives in (no abbreviations or short hand) |
| biosample_source_id  |                               | No       | str        | Unique identifier of patient or environmental sample. **Do not use an NHS number here**. This field will be backfilled later by PHx and HDR-UK. |
| collecting_org       |                               | No       | str       | The site (eg. hospital or surgery) that this sample was originally collected by. Use the first line of the 'sender' from the E28 form.
| root_sample_id       | phx_sample_id                 | No       | str        | Identifier assigned to this sample from one of the health agencies (eg. PHE samples will be prefixed with `H20`). This is necessary for linking samples to private patient metadata later. |
| sample_type          |                               | No       | str | Sample type. **Options** `swab`,`sputum`,`BAL`,`extract`,`culture` |
| sender_sample_id     | local_sample_id               | No      | str        | If this sample was renamed by a local organisation (eg. hospital virology lab, sequencing lab), provide this identifier here. Otherwise leave blank. |
| swab_site            |                               | No       | str | Swab site. **Options** `nose`,`throat`,`nose-throat`|

The following fields are also required, but are submitted automatically. **You do not need to provide these fields**.

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| submitting_user |              | Yes, but provided automatically       | str        | Your username 
| submitting_org  |              | Yes, but provided automatically       | str        | Your organisation
