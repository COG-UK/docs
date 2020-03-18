---
layout: docpost
title: Upload instructions
date_published: 2017-12-17 10:00:00 +0000
date_modified:  2020-03-18 16:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

### 0. Request access to CLIMB
Request access by sending a message to the `#account-requests` Slack channel with the following information:

* Full name
* Organisation
* Email address
* SSH Public Key

**You will not be able to upload data until your key has been added to the server.**  
**Your username will begin with <code>climb-covid19-</code>. Remember to use this prefix when accessing systems later.**
**The server accepts public SSH keys only. You will not be allowed to login with a password.**

### 1. Prepare you data
We are accepting:

* `.bam` Reads aligned to the `MN908947.3` reference. The BAM must be **sorted** and unmapped reads must be **filtered**.
* `.fa` Consensus sequence as FASTA

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
Discussion on minimal and desired metadata is ongoing (see the `#metadata` Slack channel).
Please do not upload metadata in any format at this time.
CLIMB will be storing a subset of the mandatory sample and sequencing run information in SQL, primarily for orchestrating pipelines on CLIMB and automating submissions to public databases (e.g. ENA).
We will provide an interface through which metadata can be provided (e.g. JSON over HTTPS POST and web form), once the list of fields has been confirmed.

### 4. SSH
You may check your upload was successful by logging in with SSH:
```
ssh **USERNAME**@bham.covid19.climb.ac.uk
```



