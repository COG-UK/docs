---
layout: docpost
title: Using the Majora API
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-22 21:50:00 +0000
author: samstudio8
maintainer: samstudio8
---
# Basics
## Requests
All requests have the following mandatory keys:

```json
{
    "username": 0,
    "token": 0,
}
```

Where `username` is your COG-UK CLIMB username and `token` is your secret API key.
If you do not have access to COG-UK CLIMB, [register for a COG-UK account](https://majora.covid19.climb.ac.uk/forms/register).

Existing users can check their key by logging in and [viewing their profile](https://majora.covid19.climb.ac.uk/accounts/profile).
**Treat your key as securely as your password. Anyone with your key can perform API actions, as you**.

Send your request as a `POST`, with `"Content-Type: application/json"`:

```
curl --header "Content-Type: application/json" \
     --request POST \
     --data '{ "username":"USERNAME", "token":"TOKEN", [...] }' \
     <ENDPOINT>
```

## Responses

Each **valid** request to the Majora API will return the following basic structure:

```json
{
    "errors": 0,
    "warnings": 0,
    "messages": [],

    "new": [],
    "updated": [],
    "ignored": [],

    "success": true
}
```

| Key       | Type           | Description                           |
|-----------|----------------|---------------------------------------|
| errors    | int            | Number of errors encountered          |
| warnings  | int            | Number of warnings raised             |
| messages  | list[list, str]| List (of lists) with warnings and messages as strings |
| new       | list[ [str, uuid, str],... ]     | List of tuples in the format (object_type, object_uuid, object_id) for objects created as a result of your request |
| updated   | list[ [str, uuid, str],... ]   | List of tuples in the format (object_type, object_uuid, object_id) for objects updated as a result of your request |
| ignored   | list[uuid, str]     |  List of UUIDs or string IDs ignored by your request due to errors |
| success   | bool           | `true` if `errors == 0`             |

<hr>

# Actions

| Action              | Description                                                            | Endpoint                              |
|---------------------|------------------------------------------------------------------------|---------------------------------------|
| [api.artifact.biosample.add](majora/add_sample)       | Add biosample metadata, and additionally biosamplesource metadata      | `api/v2/artifact/biosample/add/` |
| [api.artifact.library.add](majora/add_library)       | Add sequencing library for pooled samples | `api/v2/artifact/library/add/` |
| [api.process.sequencing.add](majora/add_sequencing)       | Add sequencing runs for a library      | `api/v2/process/sequencing/add/` |

Note that the examples in the following section assume that you are providing the mandatory fields described above.
