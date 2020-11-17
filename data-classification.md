---
layout: docpost
title: COG-UK biosample data classification
date_published: 2020-09-24 12:00:00 +0000
date_modified:  2020-09-24 12:00:00 +0000
author: michaelrchapman
maintainer: michaelrchapman
---

# Classification of COG-UK biosample data

This table shows the classification of data items covered by the COG-UK Consortium Agreement. Items are classified as:
* Public: Accessible to the consortium without application. Released to public databases.
* Consortium: Accessible to the consortium without application. May only be analysed on CLIMB-COVID.
* Restricted: Require approval from the Steering Group and Public Health Agencies for use in specific analyses on CLIMB-COVID.

**N.B. The inclusion of an item in this table does not mean it is available for analysis, simply that it has been approved for inclusion in the dataset if it can be obtained.**

Data item | Field name |  Access level (Public, Consortium or Restricted)
----------|------------|---------------------------------------------------
**Sample identifiers** | |
Central Sample ID | central_sample_id | Public
COG-UK Patient ID | biosample_source_id | Consortium
PHA Patient ID | root_biosample_source_id | Consortium
PHA sample ID | root_sample_id | Restricted
Local sample ID | sender_sample_id | Restricted
**Sample details** |  | 
Date of sample (collected) | collection_date | Public
Date of sample (received) | received_date | Public
Collecting organisation | collecting_org | Consortium
Sampling strategy | is_surveillance | Consortium
Sample type collected | sample_type_collected | Consortium
Swab site | swab_site | Consortium
Sample type received | sample_type_received | Consortium
Ct value | ct_N_ct_value | Consortium
Ct test kit | ct_N_test_kit | Consortium
Ct test platform | ct_N_test_platform | Consortium
Ct test target | ct_N_test_target | Consortium
**Demographics and employment** |  | 
UK nation | adm1 | Public
County | adm2 | Consortium
Outer postcode | adm2_private | Consortium
Age | source_age | Consortium
Sex | source_sex | Consortium
Household ID | *tbc* | Restricted
Ethnicity | *tbc* | Restricted
Socioeconomic status | *tbc* | Restricted
Healthcare worker | is_hcw | Restricted
Employing hospital | employing_hospital_name | Restricted
Employing trust / board | employing_hospital_trust_or_board | Restricted
Care home worker | is_care_home_worker | Restricted
Care home resident | is_care_home_resident | Restricted
Care home ID | anonymised_care_home_code | Restricted
**Case severity and outcome** |  | 
Hospitalisation | is_hospital_patient | Restricted
Date of admission | admitted_date | Restricted
Admitting hospital | admitted_hospital_name | Restricted
Admitting trust or board | admitted_hospital_trust_or_board | Restricted
Admitted with COVID-19 diagnosis | admitted_with_covid_diagnosis | Restricted
Critical care admission | is_icu_patient | Restricted
Outcome | *tbc* | Restricted
**Local investigations** |  | 
Investigation name | investigation_name | Restricted
Investigation site | investigation_site | Restricted
Investigation cluster | investigation_cluster | Restricted
