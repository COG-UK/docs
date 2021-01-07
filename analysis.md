---
layout: docpost
title: Analysing data and submitting jobs on CLIMB-COVID
date_published: 2021-01-07 11:30:00 +0000
date_modified:  2021-01-07 11:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

## Using CLIMB-COVID for analysis
### Recommended workflow packages

We strongly recommend using [Nextflow](https://www.nextflow.io/) or [Snakemake](https://snakemake.readthedocs.io/en/stable/) to orchestrate analysis on CLIMB-COVID.
Users should not run any analysis on the login node and be aware that any processes that threaten the system stability will be terminated without notice.


### Submitting jobs directly to the SLURM scheduler

[How to submit jobs to the Slurm scheduler](https://intranet.birmingham.ac.uk/it/teams/infrastructure/research/bear/bluebear/bluebear-job-submission.aspx)
