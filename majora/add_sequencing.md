---
layout: docpost
title: api.process.sequencing.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-25 10:45:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example

```json
{
    "library_name": "BIRM-LIBRARY-20200322",


        "runs": [
            {
                "sequencing_id": "09ef4b3a-1bad-453a-a291-029ac9bd705d",
                "instrument_make": "OXFORD_NANOPORE",
                "instrument_model": "GridION",
                "flowcell_type": "R9.4.1D",
                "flowcell_id": "00000",
                "start_time": "YYYY-MM-DD HH:MM:SS",
                "end_time": "YYYY-MM-DD HH:MM:SS",

            },
            {
                "sequencing_id": "2f3b14e7-7f60-4442-a199-71eee0b52e6c",
                "instrument_make": "OXFORD_NANOPORE",
                "instrument_model": "GridION",
                "flowcell_type": "R9.4.1D",
                "flowcell_id": "00000",
                "start_time": "YYYY-MM-DD HH:MM:SS",
                "end_time": "YYYY-MM-DD HH:MM:SS",
            },
            {
                "sequencing_id": "82c9831c-fe2f-4c3c-9655-611ba1f13fec",
                "instrument_make": "OXFORD_NANOPORE",
                "instrument_model": "GridION",
                "flowcell_type": "R10.3",
                "flowcell_id": "00001",
                "start_time": "YYYY-MM-DD HH:MM:SS",
                "end_time": "YYYY-MM-DD HH:MM:SS",
            }
        ]
}
```

### Reference

Each `run` is an object with the following keys:

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| sequencing_id        |                               | **Yes**      | uuid        | A single UUID corresponding to your sequencing run, you can use the one your sequencer gives you, or generate one yourself |
| instrument_make*        |                               | **Yes**      | str        | **Options** `ILLUMINA`, `OXFORD_NANOPORE`, `PACIFIC_BIOSCIENCES` |
| instrument_model*        |                               | **Yes**      | str        |  |
| end_time        |                               | No      | str        |  |
| flowcell_id        |                               | No      | str        | Flowcell serial number |
| flowcell_type        |                               | No      | str        | Flowcell description |
| start_time          |                               | No      | str        |||
