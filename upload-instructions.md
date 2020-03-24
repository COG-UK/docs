---
layout: docpost
title: Upload instructions
date_published: 2020-03-17 10:00:00 +0000
date_modified:  2020-03-24 14:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

### 0. Request access to CLIMB
Request access by filling out the [registration form](https://majora.covid19.climb.ac.uk/forms/register/).

**You will not be able to upload data until your key has been added to the server.**  
**Your username will begin with <code>climb-covid19-</code>. Remember to use this prefix when accessing systems later.**
**The server accepts public SSH keys only. You will not be allowed to login with a password.**

### 1. Prepare you data
We are accepting:

* `.bam` Reads aligned to the `MN908947.3` \ `NC_045512` reference. The BAM must be **sorted** and unmapped reads must be **filtered**.
* `.fa|.fas|.fasta` Consensus sequence as FASTA

Arrange your <code>DATA_DIR</code> by creating a directory for each sample.
Each sample's directory should be named with the identifier you are using internally for that sample.
The file names are less important, but must end with the right file extension to be detected (see list above).
In lieu of a formal unified naming scheme at this time, please ensure that your sample directories are named such that you will be able to identify them in the future and at the least, are unique to your site.

As an example, the following `data_dir` contains two samples: `Sample1` and `Sample2`:

```
        | data_dir/
        |--| Sample1
           |-- sample1.bam
           |-- sample1.fa
        |--| Sample2
           |-- sample2.bam
           |-- sample2.fa
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
We are building a central database for sample metadata.
In the meantime, sample metadata is organised into a Google Sheet, the link can be found in the `#inbound-distribution` channel. When you have **finished** uploading samples for a run, please contact `Sam Nicholls` on Slack to have your new samples pulled into the sheet.
When your samples appear, please fill in the mandatory fields as best as possible.

This is a temporary measure this week. Starting Saturday 28th March, sample metadata must be provided via one of the approved routes. Documentation for these metadata routes will be made available in the next day or so. Thanks for your patience!

**You will not be able to run analyses of your samples on climb without providing metadata.**

### 4. SSH
You may check your upload was successful by logging in with SSH:
```
ssh **USERNAME**@bham.covid19.climb.ac.uk
```



