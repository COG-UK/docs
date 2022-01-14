---
layout: docpost
title: When is metadata and sequence data processed on CLIMB?
date_published: 2020-05-29 10:50:00 +0000
date_modified:  2021-03-03 12:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

# Timeline
## Inbound pipeline

The inbound distribution pipeline (called `Elan`) currently runs every day (including weekends). 
The dataset as it stands after the Friday pipeline is used for weekly reporting.
The pipeline currently consists of the following events:

| Time    | Event | Descirption |
|---------|-------|-------------|
| `1605` | End of day check 1 | Using the uploaded metadata, Majora generates a list of samples to check against the file system. |
| `1630` | End of day message 1 | The Majora bot annouces in `#inbound-distribution` the number of new sequences for each site that can be linked to metadata. It will also list the number of sequences that appear to be missing uploaded metadata, or metadata that appears to be missing uploaded sequence. |
| `1705` | End of day check 2 | Using the uploaded metadata, Majora generates a list of samples to check against the file system. |
| `1730` | End of day message 2 | The `Majora` bot announces in `#inbound-distribution` the number of sequences pulled for each site, the week's total and the new cumulative upload total. |
| +1 day `0501` | Permissions check | A cron job runs `chmod` to ensure all the upload directories are readable by the pipeline. |
| +1 day `0505` | Pre-pull | Using the uploaded metadata, Majora generates a list of samples to check against the file system. |
| +1 day `0601` | Pipeline starts | If nothing horrible has gone wrong, the pipeline will start. |
| ~  | Pipeline ends | After a few hours, the Majora bot will annouce to `#inbound-distribution` the number of sequences that made it through the pipeline and passed basic QC. |

### How long does the pipeline take?

Elan can process approximately 1000 samples an hour on a good day. Combined with around 90 minutes for "post-Elan publishing", an average pipeline of 3000 samples should take around 5 hours to complete (ready for lunch). For PHA subscribed to `Asklepian`, processing time on a good day is around 90 minutes (mid afternoon).

## Outbound pipeline
The GISAID pipeline runs every day and releases sequences on a 7 day time lag. The ENA BAM pipeline runs on Mondays, the ENA consensus pipeline runs on Fridays. All sites are automatically enrolled for ENA BAM uploads. You must however [opt-in for GISAID uploads](gisaid) or ENA consensus uploads. Data uploaded over the weekend will miss the official reporting cut-off, but will be included in Monday's outbound pipeline.

#### Note

* We strongly recommend metadata and sequence is uploaded before 1600 to ensure any issues are brought to your attention by the first end of day message.
* You are however welcome to wing it and roll the dice by uploading between `1600` and `0500`. The pre-Elan message will inform you whether your gamble was a success or not.
* The pipeline begins completely autonomously at `0601`.
* If you typically stage metadata or sequencing with the intention of updating it before the formal Friday cut-off, you will need to take action to avoid your data being pulled. If you do not want records to be pulled in to elan then you could (a) stop uploading metadata until it is ready and/or (b) withold uploading the sequence to CLIMB until ready. A potential middle-ground solution would be to create a staging directory outside your upload/ directory to sftp to, then move those folders to upload/ when ready.
* Please be vigilant with your metadata as errors will be integrated into the downstream analysis dataset in a matter of hours.
* Note that the weekend pipeline is provided as a courtesy to support emergency scenarios requiring data analysis on the weekend. The weekend pipeline will run without dedicated support.
