---
layout: docpost
title: Using the Majora API
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-22 14:10:00 +0000
author: samstudio8
maintainer: samstudio8
---
# Basics
## Requests
All requests have the following mandatory keys:

```json
{
    "username": 0,
    "token": 0,
}
```

Where `username` is your COG-UK CLIMB username and `token` is your secret API key.
If you do not have access to COG-UK CLIMB, [register for a COG-UK account](https://majora.covid19.climb.ac.uk/forms/register).

Existing users can check their key by logging in and [viewing their profile](https://majora.covid19.climb.ac.uk/accounts/profile).
**Treat your key as securely as your password. Anyone with your key can perform API actions, as you**.

## Responses

Each **valid** request to the Majora API will return the following basic structure:

```json
{
    "errors": 0,
    "warnings": 0,
    "messages": [],
    
    "new": [],
    "updated": [],
    "ignored": [],
    
    "success": true
}
```

| Key       | Type           | Description                           |
|-----------|----------------|---------------------------------------|
| errors    | int            | Number of errors encountered          |
| warnings  | int            | Number of warnings raised             |
| messages  | list[list, str]| List (of lists) with warnings and messages as strings |
| new       | list[uuid]     | List of UUIDs created as a result of your request |
| updated   | list[uuid]     | List of UUIDs updated by your request |
| ignored   | list[uuid, str]     |  List of UUIDs or string IDs ignored by your request due to errors |
| success   | bool           | `true` if `errors == 0`             |

<hr>

# Actions

| Action              | Description                                                            | Endpoint                              |
|---------------------|------------------------------------------------------------------------|---------------------------------------|
| `api.artifact.biosample.add`       | Add biosample metadata, and additionally biosamplesource metadata      | `api/v2/artifact/biosample/add/` |

Note that the examples in the following section assume that you are providing the mandatory fields described above.

### Add a sample: `api.artifact.biosample.add`

Example
```json
{
    "biosamples": [
    ]
}
```

`biosamples` is the only mandatory key, which is a **list** that may contain **one or more** objects with the following structure:


| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| biosample_source_id  | sample_source_id              | No       | str        | Unique identifier of patient or environmental sample. **Do not use an NHS number here**. This field will be backfilled later by PHx and HDR-UK. |
| root_sample_id       | phx_sample_id                 | No       | str        | Identifier assigned to this sample from one of the health agencies (eg. PHE samples will be prefixed with `H20`). This is necessary for linking samples to private patient metadata later. |
| sender_sample_id     | local_sample_id               | No      | str        | If this sample was renamed by a local organisation (eg. hospital virology lab, sequencing lab), provide this identifier here. Otherwise leave blank. |
| central_sample_id    | coguk_sample_id               | Yes      | str        | The centrally generated "Heron" barcode assigned to this sample. If this sample does not have a Heron barcode, use the `root_sample_id`. |
| collection_date      |                               | Yes      | str | The date the sample was collected. **YYYY-MM-DD** only. |
| adm1_region          |                               | Yes      | str | **Options** `UK-ENG`,`UK-SCT`,`UK-WLS`,`UK-NIR`|
| adm2_county          |                               | No       | str        | The county that the patient lives in (no abbreviations or short hand) |
| source_age           |                               | Yes      | int        | Age of the patient in years |
| source_sex           |                               | Yes      | str | Sex of the patient. **Options** `F`,`M`,`Other` |
| sample_type          |                               | No       | str | Sample type. **Options** `swab`,`sputum`,`BAL`,`extract`,`culture` |
| swab_site            |                               | No       | str | Swab site. **Options** `nose`,`throat`,`nose-throat`|
| secondary_identifier    | gisaid_identifier             | Yes, if in GISAID | str | GISAID identifier (eg. hCov-19/.../2020) if the sample has already been uploaded to GISAID
| gisaid_accession     |                               | Yes, if in GISAID | str | GISAID accession if the sample has already been uploaded to GISAID |
| collecting_org       |                               | No       | str       | The site (eg. hospital or surgery) that this sample was originally collected by. Use the first line of the 'sender' from the E28 form.

The following fields are also required, but are submitted automatically. **You do not need to provide these fields**.

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| submitting_user |              | Yes, but provided automatically       | str        | Your username 
| submitting_org  |              | Yes, but provided automatically       | str        | Your organisation
