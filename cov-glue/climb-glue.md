---
layout: docpost
title: Accessing CoV-GLUE on CLIMB
date_published: 2020-05-18 11:45:00 +0000
date_modified:  2020-05-18 11:45:00 +0000
author: joshsinger
maintainer: joshsinger
---

# Offline CoV-GLUE 
You can run the [GLUE command line tool](http://glue-tools.cvr.gla.ac.uk) on CLIMB infrastructure. Benefits:
* Broader functionality than the [CoV-GLUE web application](http://cov-glue.cvr.gla.ac.uk)
* Scriptable
* Access datasets based on COG-UK data as well as GISAID data 

## Getting started
There is a special CLIMB VM `glue.covid19.climb.ac.uk` for running GLUE. You can ssh to it using the same user ID (e.g. `climb-covid19-singerj`) and private key file (e.g. `climb_cog_id_rsa`) you would use for COG-UK CLIMB generally:

`$ ssh -i climb_cog_id_rsa climb-covid19-singerj@glue.covid19.climb.ac.uk`

Once you have connected, you need to perform a one-time task to set up your personal GLUE instance within the VM:

```
$ initGlue.sh
```

You should see some log messages ending with:

```
GLUE installation complete
Log in again or run source ~/.bash_profile to add gluetools.sh to your PATH
```

Now do:

`$ source ~/.bash_profile`

This adds the `gluetools.sh` command to your PATH. On future logins to the VM it will always be there. 

## Installing a CoV-GLUE dataset
You now have a personal GLUE instance but it contains no data. You have two options:
1. `$ installGlueProject.sh cov_glue` 
installs the dataset backing the CoV-GLUE web application, based purely on GISAID data.
1. `$ installGlueProject.sh coguk_cov_glue` 
installs a larger dataset, containing `cov_glue` plus COG-UK sequences/metadata and various items relating to the HOCI project.

These datasets are being updated approximately weekly.

## Some example GLUE commands
To give a flavour of what CoV-GLUE can do, try this:

```
$ gluetools.sh
GLUE> project cov
OK
GLUE> list sequence -w "m49_country.id = 'BEL' and collection_date < #gluedate(01-Mar-2020)" sequenceID collection_date cov_glue_lineage
OK
GLUE> module covFastaProteinAlignmentExporterSeqIdOnly export AL_GISAID_CONSTRAINED -r REF_MASTER_WUHAN_HU_1 -f NSP13 -l 10 20 -w "sequence.m49_country.m49_region = 'asia' and sequence.cov_glue_lineage like 'A%'" -p
...
GLUE> quit
```

The `list sequence` command listed the GISAID ID, collection date and lineage of all sequences collected in Belgium before 1st March.

The longer command exported a protein alignment of nsp13, codons 10 to 20, for all lineage A sequences from Asia.   

Many other things are possible. Anything where you are querying some aspect of a multiple sequence alignment together with metadata is within the scope of CoV-GLUE. 

