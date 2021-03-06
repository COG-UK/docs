---
layout: docpost
title: Analysing data and submitting jobs on CLIMB-COVID
date_published: 2021-01-07 11:30:00 +0000
date_modified:  2021-02-03 10:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

## Using CLIMB-COVID for analysis

We strongly recommend using [Nextflow](https://www.nextflow.io/) or [Snakemake](https://snakemake.readthedocs.io/en/stable/) to orchestrate analysis on CLIMB-COVID.
Users should not run any analysis on the login node and be aware that any processes that threaten the system stability will be terminated without notice.
If you are unsure how to proceed with your analysis, please feel free to ask questions on the `#climb` Slack channel.

### Nextflow

Nextflow is already installed on the login node. A default config that will automatically set the required Slurm parameters is provided at `/cephfs/covid/nextflow/conf/nextflow.config`. You must specify the `slurm` profile when running your pipeline.
You can copy this configuration and change parameters as required (for example to increase or decrease the default resources allocated).

### Snakemake

Snakemake is already installed on the login node. A default config that will automatically set the required Slurm parameters and submission scripts can be activated by adding `--profile /cephfs/covid/snakemake/profiles/slurm/` to your Snakemake pipeline invocation.
You can copy this configuration and change parameters as required (for example to increase or decrease the default resources allocated).


### Submitting jobs directly to the SLURM scheduler

For Slurm command reference see [how to submit jobs to the Slurm scheduler](https://intranet.birmingham.ac.uk/it/teams/infrastructure/research/bear/bluebear/bluebear-job-submission.aspx). The `QoS` account for submissions on CLIMB-COVID is `lomannj` (do not use the `bbdefault` or `bbshort` account from the linked example). An example `sbatch` script is included below:

#### Example sbatch incantation

```
#!/bin/bash
#SBATCH --cpus-per-task=1
#SBATCH --job-name=my_first_job
#SBATCH --account=lomannj-covid-19-realtime-epidemiology
#SBATCH --qos=lomannj
#SBATCH --time 10:0:0
#SBATCH --nodes=1

# Magic conda hack to correctly init conda
eval "$(conda shell.bash hook)"
```

You can adjust `--time` for jobs that you expect to run longer. Additionally `--mem-per-cpu nnG` will request `nn` GB of RAM for each requested CPU (or `--mem nnG` will request `nn` GB of RAM total). `--nodes=1` ensures that multicore jobs will be assigned CPU cores on the same machine.
