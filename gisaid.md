---
layout: docpost
title: Automated GISAID submissions
date_published: 2020-04-15 19:00:00 +0000
date_modified:  2021-01-19 10:15:00 +0000
author: samstudio8
maintainer: samstudio8
---

Sequencing sites can opt-in to a process where consensus sequences uploaded to CLIMB that pass high quality QC are automatically submitted to GISAID on their behalf.

## How do I opt-in?

You can opt-in via your [Institute profile on Majora](https://majora.covid19.climb.ac.uk/forms/institute/).
One only user per site needs to provide this information and it is does not need to be the same person who provides the metadata or uploads the sequences.
You will need to provide:

* your e-mail address (we will pass this on to GISAID curators to contact you about your entries)
* a valid GISAID username (**if you have not registered, [you will need to get a GISAID account first](https://www.gisaid.org/registration/register/)**), this username **is not your email address**, failing to provide the username for your account will cause errors for your submissions
* the name of the lab or labs that you wish to credit as the originating lab (this will include your sequencing lab)
* a list of people you wish you credit

You will also need to raise this to Sam in `#outbound-distribution` as we must notify GISAID of your username.

## How does it work?

Bulk uploads are automatically generated at noon on Monday and will release all new seqeunces that pass high quality QC that have been uploaded in the past week.

## Do I have to do anything?

You should periodically check the "My Unreleased" tab on the GISAID website. Curators will flag sequences with frameshifts and other quality artefacts for you to approve before they are made public, we do not control this process.
