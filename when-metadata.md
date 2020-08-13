---
layout: docpost
title: When is metadata and sequence data processed on CLIMB?
date_published: 2020-05-29 10:50:00 +0000
date_modified:  2020-08-13 14:30:00 +0000
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
| `1201` | Permissions check | A cron job runs `chmod` to ensure all the upload directories are readable by the pipeline. |
| `1205` | Pre-pull check | Using the uploaded metadata, Majora generates a list of samples to check against the file system. |
| `1215` | Pre-pull message | The Majora bot annouces in `#inbound-distribution` the number of new sequences for each site that can be linked to metadata. It will also list the number of sequences that appear to be missing uploaded metadata, or metadata that appears to be missing uploaded sequence. |
| `1301` | Permissions check | A cron job runs `chmod` to ensure all the upload directories are readable by the pipeline. |
| `1305` | Pull check | Using the uploaded metadata, Majora generates a list of samples to check against the file system. |
| `1315` | Pull message | The `Majora` bot announces in `#inbound-distribution` the number of sequences pulled for each site, the week's total and the new cumulative upload total. |
| `1330` | Pipeline starts | If nothing horrible has gone wrong, the pipeline will start. |
| ~`1500`  | Pipeline ends | After a few hours, the Majora bot will annouce to `#inbound-distribution` the number of sequences that made it through the pipeline and passed basic QC. |

## Outbound pipeline
GISAID and ENA pipelines run on Mondays. All sites are automatically enrolled for ENA uploads. You must however [opt-in for GISAID uploads](gisaid). Data uploaded over the weekend will miss the official reporting cut-off, but will be included in Monday's outbound pipeline.

#### Note

* Files and metadata uploaded between 1201 and 1215 may not have the requisite permissions to be seen for the pre-pull message.
* Files and metadata uploaded between 1301 and 1315 may not have the requisite permissions to be seen before the pull message. These files will not be pulled into the pipeline.
* We strongly recommend metadata and sequence is uploaded before 1200 to ensure any issues are brought to your attention by the pre-pull message.
* You are however welcome to wing it and roll the dice by uploading between 1200 and 1300. The pull message will inform you whether your gamble was a success or not.
* The pipeline begins completely autonomously at `1330`.
* If you typically stage metadata or sequencing with the intention of updating it before the formal Friday cut-off, you will need to take action to avoid your data being pulled. If you do not want records to be pulled in to elan then you could (a) stop uploading metadata until it is ready and/or (b) withold uploading the sequence to CLIMB until ready. A potential middle-ground solution would be to create a staging directory outside your upload/ directory to sftp to, then move those folders to upload/ when ready.
* Please be vigilant with your metadata as errors will be integrated into the downstream analysis dataset in a matter of hours.
* Note that the weekend pipeline is provided as a courtesy to support emergency scenarios requiring data analysis on the weekend. The weekend pipeline will run without dedicated support.
