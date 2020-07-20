---
layout: docpost
title: Upload instructions
date_published: 2020-03-17 10:00:00 +0000
date_modified:  2020-05-21 12:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

### 0. Register for an account via Majora
[Read the instructions for how to register](register)

### 1. Prepare your data
We are accepting:

* `.bam` Reads aligned to the `MN908947.3` \ `NC_045512` reference. The BAM must be **sorted** and unmapped reads must be **filtered**. If you used the ARTIC pipeline, provide the **untrimmed** BAM.
* `.fa|.fas|.fasta` Consensus sequence as FASTA

Arrange your <code>DATA_DIR</code> by creating a directory for each sequencing run.
Each run directory should be named with your sequencing `run_name`, **exactly** as it appears in the associated metadata.

Inside each run directory, you should create a directory for each sample, named with the sample's `central_sample_id`, **exactly** as it appears in your metadata.

**You must name your directories in this way to ensure they are collected by the system when your metadata is uploaded**.

The file names are less important, but must end with the right file extension to be detected (see list above).
In lieu of a formal unified naming scheme at this time, please ensure that your sample directories are named such that you will be able to identify them in the future and at the least, are unique to your site.

As an example, the following `data_dir` contains two runs with two samples each:

```
        | data_dir/
        |--| 200320_M00001_0001
           |--| BIRM-XXXXX
              |-- alignment.bam
              |-- consensus.fa
           |--| BIRM-YYYYY
              |-- alignment.bam
              |-- consensus.fa
        |--| 200320_M00001_0002
           |--| BIRM-AAAAA
              |-- alignment.bam
              |-- consensus.fa
           |--| BIRM-BBBBB
              |-- alignment.bam
              |-- consensus.fa

```
Further runs on the same sample can be added in future by adding a new run directory and re-using the original sample name. Do not delete the old data.
```
        | data_dir/
        |--| 200320_M00001_0001
           |--| BIRM-XXXXX
              |-- alignment.bam
              |-- consensus.fa
           |--| BIRM-YYYYY
              |-- alignment.bam
              |-- consensus.fa
        |--| 200320_M00001_0002
           |--| BIRM-AAAAA
              |-- alignment.bam
              |-- consensus.fa
           |--| BIRM-BBBBB
              |-- alignment.bam
              |-- consensus.fa
        |--| 200320_M00001_0003
           |--| BIRM-AAAAA
              |-- alignment.bam
              |-- consensus.fa
           |--| BIRM-BBBBB
              |-- alignment.bam
              |-- consensus.fa
```

### 2. Upload with rsync or scp
#### rsync

```
rsync -av --progress **DATA_DIR** **USERNAME**@bham.covid19.climb.ac.uk:upload/
```

#### scp
```
scp -r **DATA_DIR** **USERNAME**@bham.covid19.climb.ac.uk:upload/
```

Recall your username begins with `climb-covid19-`.

### 3. Metadata
See [providing metadata](metadata).

**You will not be able to run analyses of your samples on climb without providing metadata.**

### 4. SSH
You may check your upload was successful by logging in with SSH:
```
ssh **USERNAME**@bham.covid19.climb.ac.uk
```



