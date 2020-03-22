---
layout: docpost
title: Using the Majora API
date_published: 2020-03-22 13:00:00 +0000
date_modified:  2020-03-22 13:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Responses

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
| new       | list[uuid]     | List of UUIDs created as a result of your request |
| updated   | list[uuid]     | List of UUIDs updated by your request |
| ignored   | list[uuid, str]     |  List of UUIDs or string IDs ignored by your request due to errors |
| success   | bool           | `true` if `errors == 0`             |
