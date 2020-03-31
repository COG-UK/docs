---
layout: docpost
title: api.process.sequencing.add
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-30 12:25:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Example

```json
{
    "library_name": "BIRM-LIBRARY-20200322",
    "run_group": "my-merged-runs",


        "runs": [
            {
                "run_name": "BIRM-my_first_run",
                "instrument_make": "OXFORD_NANOPORE",
                "instrument_model": "GridION",
                "flowcell_type": "R9.4.1D",
                "flowcell_id": "00000",
                "start_time": "YYYY-MM-DD HH:MM:SS",
                "end_time": "YYYY-MM-DD HH:MM:SS",

            },
            {
                "run_name": "BIRM-my_first_rerun",
                "instrument_make": "OXFORD_NANOPORE",
                "instrument_model": "GridION",
                "flowcell_type": "R9.4.1D",
                "flowcell_id": "00000",
                "start_time": "YYYY-MM-DD HH:MM:SS",
                "end_time": "YYYY-MM-DD HH:MM:SS",
            },
            {
                "run_name": "BIRM-my_second_run",                
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

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| library_name        |                               | **Yes**      | str        | The name of the `library` as submitted to `add_library` |
| run_group        |                               | **Yes**, if multiple run objects      | str, unique        | A unique name that corresponds to a grouping of runs (an experiment). **Only provide a run group if the results of all the listed runs were merged for downstream analysis** |

Each `run` is an object with the following keys:

| Key                  | COG-UK metadata equivalent (if different)   | Required | Type       | Description                           |
|----------------------|-------------------------------|----------|------------|---------------------------------------|
| instrument_make*        |                               | **Yes**      | str        | **Options** `ILLUMINA`, `OXFORD_NANOPORE`, `PACIFIC_BIOSCIENCES` |
| instrument_model*        |                               | **Yes**      | str        |  |
| run_name        |                               | **Yes**      | str, unique        | A unique name that corresponds to your run. You may use any string identifier, including a UUID |
| end_time        |                               | No      | str        |  |
| flowcell_id        |                               | No      | str        | Flowcell serial number |
| flowcell_type        |                               | No      | str        | Flowcell description |
| start_time          |                               | No      | str        |||
