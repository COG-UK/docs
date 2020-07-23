---
layout: docpost
title: Accessing data
date_published: 2020-03-29 23:20:00 +0000
date_modified:  2020-07-23 15:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

## Accessing CLIMB data that has passed basic QC

You need a CLIMB account to upload or access data. If you haven't got one, [see instructions on registering](register).
You will need to SSH into the CLIMB COVID server.

The latest artifacts are published in `/cephfs/covid/bham/artifacts/published/latest`.

For just the sequences, you can use `/cephfs/covid/bham/artifacts/published/elan.latest.consensus.fasta`.
The FASTA headers are encoded with the `central_sample_id`, `sequencing_center` and `run_name`:

```
COG-UK/`central_sample_id`/`sequencing_center`:`run_name`|`row_number`
```

Basic metadata is provided in the table `/cephfs/covid/bham/artifacts/published/majora.latest.metadata.tsv`.
The FASTA consensus and metadata table are perfectly paired. The sequence records in the FASTA and metadata rows in the table are in the same order.
Additionally, the table contains a `fasta_header` column that can be used to map the records in the FASTA file; and likewise, the end of each FASTA header ends with the numeric index of the corresponding row in the metadata table (starting at 1).

Note that the merged consensus FASTA will also include resequencing. That is, a biosample may have more than one genome in the consensus FASTA, you can identify them as they will have the same `central_sample_id` in their header.


For all metadata, use `/cephfs/covid/bham/artifacts/published/majora.latest.metadata.tsv`.

Note that the merged consensus FASTA will also include resequencing. That is, a biosample may have more than one genome in the consensus FASTA, you can identify them as they will have the same `central_sample_id` in their header.
