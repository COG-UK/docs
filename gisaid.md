---
layout: docpost
title: Automated GISAID submissions
date_published: 2020-04-15 19:00:00 +0000
date_modified:  2020-04-15 19:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

Sequencing sites can opt-in to a process where consensus sequences uploaded to CLIMB are automatically submitted to GISAID on their behalf.
To do this you will need to notify the `#outbound-distribution` Slack channel that your site would like to be included in bulk uploads to GISAID.

## How do I opt-in?

You will need to provide:

* your COG-UK barcode prefix as assigned by WSI, or your own prefix that you will use consistently
* your e-mail address (we will pass this on to GISAID curators to contact you about your entries)
* a valid GISAID username (if you have not registered, [you will need to get a GISAID account first](https://www.gisaid.org/registration/register/)) 
* the name of the lab or labs that you wish to credit as the originating lab (this will include your sequencing lab)
* a list of people you wish you credit

## What will I have to do?

Bulk uploads are generated Friday afternoon.
Metadata is automatically gathered from Majora and manually inserted into a Google Sheet for sites to enter their authorship information and confirm the sequences.
Once signed off by all sites, the bulk upload is sent directly to GISAID.
