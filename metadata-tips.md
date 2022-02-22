---
layout: docpost
title: So you think you are ready to provide metadata
date_published: 2020-04-03 12:30:00 +0000
date_modified:  2020-04-03 12:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

## You have read the docs?

* You know what a biosample, library and sequencing run is and what identifier they should have (ie. you read [Terminology and minimal metadata](/metadata))
* If you're submitting via the web tool, [you have read those docs](https://docs.cog-uk.io/metadata/)?
   
## Your data is really ready?

* You have provided at least the [minimum metadata](/metadata)?
* Your samples have one and only one, single, unique, shareable identifier?
* You know that the "COGUK ID" does not necessarily have to be a WSI "Heron" barcode, but that it should be consistent and is usually prefixed by some short code for your site?
* Your pooled sample libraries have a name that is reasonably unique? (`BIRM-LIBRARY-001` good, `1` bad).
* Your sequencing runs have a name that is reasonably unique? (`<date>_<machine_id>_<run_no>_<some_zeros>_<flowcell>` good, `my-run` bad)

* You are sure that you have permission to provide us this metadata?
* You are sure that any identifiers are not personally identifiable?

* If multiple samples have come from the same patient, you have set the `biosample_source_id` to the first COGUK sample identifier for all of the related samples?
* If you are re-sequencing a sample from another site, you have not changed the `central_sample_id`?

* **You are aware that once a record has been submitted, its `central_sample_id` (COGUK ID), `library_name` and `run_name` cannot be changed.** If you were thinking about changing the COGUK ID, it is now or never.
* For spreadsheet-like uploads, your data is in a CSV or XLSX with the right template for the webtool?

* It seemed to work when youn ran it on the test version of Majora? (See below)

## You have uploaded data to us at least once before?

* You have [registered for a test account](https://majora-test.covid19.climb.ac.uk/forms/register)?
* You know that this test account is different from your real CLIMB account and begins with `test-`?
* You know that the testing version of Majora has a magenta coloured banner at the top to remind you that it's the test version?
* You have your [API key token from your test profile](https://majora-test.covid19.climb.ac.uk/accounts/profile/)?
* You have tried one of the two ways to upload metadata and checked it looked right on the website?

## (a) You have tested using the web tool before?

* You used your test username and test API key to log-in?
* You have [tested an upload of a CSV or XLSX to us before](https://metadata.cog-uk.io/)?
* You tried at least:
    * [Uploading a biosample](https://docs.cog-uk.io/metadata/bulk-upload-1/bulk-upload)?
    * [Uploading a biosample and its library and sequencing run](https://docs.cog-uk.io/metadata/bulk-upload-1/samples-and-sequencing)?

## (b) You have tested the `ocarina` API before?

* You have [downloaded ocarina](https://github.com/SamStudio8/ocarina)
* You know that the configration is saved to `~/.ocarina` by default and instructions for doing this appear the first time you run the tool?
* You have set the `MAJORA_DOMAIN` to `https://majora-test.covid19.climb.ac.uk/` for testing?
* You set the `MAJORA_USER` and `MAJORA_TOKEN` to your testing username and token?
* You have tried uploading data with:
    * `ocarina put biosample`?
    * `ocarina put library`?
    * `ocarina put sequencing`?
* So you know that for `ocarina` uploads, you have to provide a biosample*, then a library, then the sequencing run, in that order? (Ask @samstudio8 about generating dummy biosamples if you want to skip straight to libraries and sequencing...).
    
## You are ready to do this for real?

* [You registered for a real unified CLIMB account](https://majora.covid19.climb.ac.uk/forms/register) and you've had an e-mail to tell you it was approved?
* You still know your password? ([Reset](https://majora.covid19.climb.ac.uk/accounts/password_reset/))
* [You have an API key token on your CLIMB profile](https://majora.covid19.climb.ac.uk/accounts/profile/)?
* You know that this account is your real account because the username does not start with `test-`?
* You know that the API key for this account is different from the one for your test account?
* You know that this username and API key will only work on the real Majora website?

* For webtool uploads: provide your real username and token and upload as normal
* For `ocarina` uploads: set `MAJORA_DOMAIN` to `https://majora.covid19.climb.ac.uk/` and update the `MAJORA_USER` and `MAJORA_TOKEN` to your real credentials?

* You promise to be careful to not submit test data to the real database because it's really hard to get rid of data once it is there?
* You know that we know who has uploaded bad metadata?
* You know that without sufficient metadata, CLIMB will not publish your sample or consensus?



