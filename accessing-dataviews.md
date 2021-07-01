---
layout: docpost
title: Accessing metadata through a data view using Ocarina
date_published: 2020-09-07 16:00:00 +0000
date_modified:  2021-07-01 15:01:00 +0000
author: samstudio8
maintainer: samstudio8
---

### 0. Register for an account via Majora
[Read the instructions for how to register](register)

### 1. Acquire permission to access a data view
A data view is basically a list of metadata fields. If you are granted access to a data view, you can see all of the fields covered by that data view.
Every data view is associated with a short name, which we sometimes call a `code` or Majora data view code (`mdv` code).

Guidance on how to obtain access to a view is in progress, check back after the consortium agreement has been distributed.
This document has been written ahead of time and we are not currently granting permissions to any restricted views. Do not attempt to contact anyone to arrange access at this time.

### 2. Install the Ocarina client

[Ocarina](https://github.com/SamStudio8/ocarina/tree/master/ocarina) is a command line tool that is used to connect to Majora and perform actions with elevated privileges that are not possible on the website.
It is not terribly difficult to use, but ideally you will have used a command line tool before.

You can install the latest version with the Python package manager. You'll probably want to install it into a conda environment on the shared node.

```
conda create -n mdv-ocarina python=3.7
conda activate mdv-ocarina
pip install git+https://github.com/samstudio8/ocarina.git
```

### 3. Register your Ocarina instance as an OAuth application

You must register an instance of Ocarina with Majora so that it can authenticate as you through OAuth.

Note that the testing and real versions of Majora are entirely separate, and so are the OAuth systems.
The locations to register an application are:

* [Test Majora (MAGENTA)](https://covid.majora.ironowl.it/o/applications/)
* [Real Majora (COG-UK)](https://majora.covid19.climb.ac.uk/o/applications/)

Click "New application" and fill out the form as appropriate:

* `Name` A name for your application, we do not enforce naming but suggest: `username-ocarina` so that you can distinguish your application from others.
* `Client ID` Do not alter this
* `Client Secret` Do not alter this
* `Client type` set to `confidential`
* `Grant type` set to `authorization code`

For Test Majora (MAGENTA)
* `Redirect Uris` set to `https://covid.majora.ironowl.it/o/callback/`

For Real Majora (COG-UK)
* `Redirect Uris` set to `https://majora.covid19.climb.ac.uk/o/callback/`

**NOTE** The approprite URL must be entered into the box **exactly** as listed here or it will not work.

Then press `Save`

### 4. Set your Ocarina credentials

Create a JSON file in your home directory named `.ocarina`. Note the starting dot. [Download the example here](.ocarina).

```
{"MAJORA_DOMAIN": "https://majora.covid19.climb.ac.uk/", "MAJORA_USER": "your-username", "MAJORA_TOKEN": "OAUTH", "CLIENT_ID": "your-client-id", "CLIENT_SECRET": "your-client-secret"}
```

Where:
* `MAJORA_DOMAIN` points to either the domain of the real, or test Majora. Do not miss the `/` at the end of the URL.
* `MAJORA_USER` is your username on the appropriate Majora instance
* `MAJORA_TOKEN` is set to `OAUTH` (note that you will not be able to use the `v2+` API without a rotating token)
* `CLIENT_ID` is the Client ID of your registered application
* `CLIENT_SECRET` is the Client Secret of your registered application

### 5. Use Ocarina to request the data from the view

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
