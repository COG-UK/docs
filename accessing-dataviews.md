---
layout: docpost
title: Accessing metadata through a data view using Ocarina
date_published: 2020-09-07 16:00:00 +0000
date_modified:  2021-07-01 15:01:00 +0000
author: samstudio8
maintainer: samstudio8
---

### 0. Set up Ocarina

[Follow these instructions to set up Ocarina for the first time](setting-up-ocarina)

### 1. Use Ocarina to request the data from the view

Once this has been set up, you are ready to retrieve data. 

```
ocarina --oauth get dataview --mdv CODE --task-wait --output-table -o my_data.tsv
```

Replace `CODE` with the appropriate data view name. Ocarina will reject your request if you attempt to access a data view you do not have permission to view.
Use the command exactly as stated (do not skip providing `--task-wait`) for ease of use.

When you submit this command, you will need to authenticate yourself through the following process:

* Ocarina will give you a link to the Majora website and then wait for you to provide more information. Open the link in your browser.
* The link will ask you to authorise the Ocarina application. Carefully check that the permissions and the owner of the application seem sensible.
* Once authorised, the Majora website will refresh to show a "Application authorized" message. DO NOT CLOSE THE PAGE.
* Copy the ENTIRE URL from your browser window (including `https://`) and paste it to your command line window.
* Ocarina will use the link you have provided to request an access token on your behalf, and request the data view.
* It may take a little while for your data to be ready, Ocarina will check every minute with the message: `[WAIT] Giving Majora a minute to finish task`.
* When your data is ready, it will be saved to whatever output file you specify with `-o`.
* **If you are requesting restricted data, it is your responsibility to protect it. Save it somewhere secure. Do not save it to a location that is group or world readable.**

This is an experimental feature and can change at any time. Please visit `#metadata-apis` if you have questions or trouble.
