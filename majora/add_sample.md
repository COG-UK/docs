---
layout: docpost
title: api.artifact.biosample.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-05-20 15:20:00 +0000
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
            "adm2": "WEST MIDLANDS",
            "collecting_org": "Queen Elizabeth Hospital Birmingham",
            "root_sample_id": "H20XXXXXXXX",
            "sample_type_collected": "swab",
            "sender_sample_id": "QELAB-01",
            "swab_site": "nose",
            
            "metadata": {
                "epi": {
                    "cluster": "my cluster identifier",
                },
                "investigation": {
                    "name": "West Midlands HCW",
                    "site": "QEB",
                    "cluster": "Ward 0",
                }
            },
            
            "metrics": {
                "ct": {
                    "records": {
                        "1": {
                            "ct_value": "29.8",
                            "test_kit": "TEST",
                            "test_platform": "TEST",
                            "test_target": "TEST"
                        },
                    }
                }
            },
            
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
| is_surveillance    |                             | **Yes**           | str        | Whether this sample was collected under the COGUK surveillance protocol. **Options** `Y`, `N` |
| received_date      |                               | **Yes**, if collection_date not available      | str | The date the sample was received. **YYYY-MM-DD** only. |
| adm2          | adm2_county                              | No       | str        | The county that the patient lives in (no abbreviations or short hand) |
| adm2_private          | adm2_postcode                              | No       | str        | The outer postcode for the patient's home address (**first half of the postcode only**) |
| biosample_source_id  |                               | No       | str        | Unique identifier of patient or environmental sample. **Do not use an NHS number here**. This field will be backfilled later by PHx and HDR-UK. |
| collection_date      |                               | No      | str | The date the sample was collected. **YYYY-MM-DD** only. |
| collecting_org       |                               | No       | str       | The site (eg. hospital or surgery) that this sample was originally collected by. Use the first line of the 'sender' from the E28 form.
| root_sample_id       | phx_sample_id                 | No       | str        | Identifier assigned to this sample from one of the health agencies (eg. PHE samples will be prefixed with `H20`). This is necessary for linking samples to private patient metadata later. |
| sample_type_collected          |                               | No       | str | Sample type. **Options** `dry swab`, `swab`,`sputum`,`BAL`,`aspirate`|
| sample_type_received         |                               | No       | str | Sample type. **Options** `primary`,`extract`,`culture`,`lysate`|
| sender_sample_id     | local_sample_id               | No      | str        | If this sample was renamed by a local organisation (eg. hospital virology lab, sequencing lab), provide this identifier here. Otherwise leave blank. |
| source_age           |                               | No      | int        | Age of the patient in years |
| source_sex           |                               | No      | str | Sex of the patient. **Options** `F`,`M`,`Other` |
| swab_site            |                               | No       | str | Swab site. **Options** `nose`,`throat`,`nose-throat`,`endotracheal`,`rectal`|
| is_hcw               || No | str | **Options** `Y`, `N` or blank |
| employing_hospital_name || No | str ||
| employing_hospital_trust_or_board || No | str ||
| is_hospital_patient              || No | str | **Options** `Y`, `N` or blank |
| admitted_date      || No      | str | The date the patient was admitted to hospital. **YYYY-MM-DD** only. |
| admitted_hospital_name || No | str ||
| admitted_hospital_trust_or_board || No | str ||
| is_care_home_worker              || No | str | **Options** `Y`, `N` or blank |
| is_care_home_resident              || No | str | **Options** `Y`, `N` or blank |
| anonymised_care_home_code || No | str(3) ||
| admitted_with_covid_diagnosis || No | str | **Options** `Y`, `N` or blank |


#### Metadata

Additionally, one may optionally provide simple key-value secondary-metadata for a biosample using the `metadata` key.
Each object inside `metadata` will be created as a tag to hold one or more key: value pairs.

You can specify any tags you like. However, the following tags are used within the project and should be followed if you want to provide this information meaningfully.

| Tag         | Name      | Description                           |
|-------------|-----------|---------------------------------------|
| `epi`     | `cluster` | A local identifier for a known case cluster |
| `investigation` | `name` | A named investigation (eg. a surveillance or directed case group) |
| `investigation` | `site` | An optional site name (likely to be the same as `collecting_org`) to distinguish cases between sites if the investigation covers more than one site |
| `investigation` | `cluster` | An optional identifier for a cluster within an investigation |

All metadata is optional. Metadata can be updated at any time.

#### Metrics

Finally, it is also possible to provide primary-metadata in the form of metrics using the `metrics` key.
Metrics are not arbitrary and have a fixed set of fields that may or may not be optional.
Metrics are identified with a key and the value is a complex object validated by the API.
For a biosample you may submit the following metrics:

##### Sample cycle threshold (Ct)

Add a `ct` key to the `metrics` structure. 
There are no mandatory or optional fields, other than `records` which takes a dictionary of Ct tests. Each test must be identified with an arbitrary key that is ignored by the API. The value is a dictionary with the following fields:

| Tag         | Name      | Description                           |
|-------------|-----------|---------------------------------------|
|  | `ct_value` | Cycle threshold value |
|  | `test_kit` | The kit used to perform the assay |
|  | `test_platform` | The platform used to perform the assay |
|  | `test_target` | The target under assay |


### Frequently asked questions

* Ages should be whole numbers. Neonatals should be entered as 0. Leave the field blank for not recorded.
