---
layout: docpost
title: api.process.sequencing.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-23 20:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example

```json
{
    "library_name": "BIRM-LIBRARY-20200322",
    "biosamples": [
        "BIRM-XXXXX",
        "BIRM-YYYYY",
        "BIRM-ZZZZZ",
    ],
    
    "sequencing_id": "09ef4b3a-1bad-453a-a291-029ac9bd705d",
    "instrument_make": "OXFORD_NANOPORE",
}
```

### Reference

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| instrument_make        |                               | **Yes**      | str        | **Options** `ILLUMINA`, `OXFORD_NANOPORE` |
| library_name    |                                    | **Yes**      | str, unique        | A unique, somewhat memorable name for your library. |
| biosamples              |                               | **Yes**      | list[str] | The `central_sample_id` of each biosample in the library |
| sequencing_id        |                               | **Yes**      | uuid        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |
