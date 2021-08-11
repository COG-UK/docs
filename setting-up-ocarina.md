---
layout: docpost
title: Setting up Ocarina and OAuth
date_published: 
date_modified:  2021-07-05 15:01:00 +0000
author: BioWilko
maintainer: BioWilko
---

### 0. Register for an account via Majora
[Read the instructions for how to register](register)

### 1. Install the Ocarina client

[Ocarina](https://github.com/SamStudio8/ocarina/tree/master/ocarina) is a command line tool that is used to connect to Majora and perform actions with elevated privileges that are not possible on the website.
It is not terribly difficult to use, but ideally you will have used a command line tool before.

You can install the latest version with the Python package manager. You'll probably want to install it into a conda environment on the shared node.

```
conda create -n ocarina python=3.7
conda activate ocarina
pip install git+https://github.com/samstudio8/ocarina.git
```

Please remember to check the [ocarina changelog](https://github.com/SamStudio8/ocarina/blob/master/CHANGELOG.md) periodically and update your client as necessary.

### 2. Register your Ocarina instance as an OAuth application

Instructions to do this are located [here](oauth-app). Only the first section is necessary to set up ocarina but must be done before moving to the next step.

### 3. Set your Ocarina credentials

Create a JSON file in your home directory named `.ocarina`. Note the starting dot.

```
{"MAJORA_DOMAIN": "https://majora.covid19.climb.ac.uk/", "MAJORA_USER": "your-username", "MAJORA_TOKEN": "OAUTH", "CLIENT_ID": "your-client-id", "CLIENT_SECRET": "your-client-secret"}
```

Where:
* `MAJORA_DOMAIN` points to either the domain of the real, or test Majora. Do not miss the `/` at the end of the URL.
* `MAJORA_USER` is your username on the appropriate Majora instance
* `MAJORA_TOKEN` is set to `OAUTH` (note that you will not be able to use the `v2+` API without a rotating token)
* `CLIENT_ID` is the Client ID of your registered application
* `CLIENT_SECRET` is the Client Secret ID of your registered application

OAuth has been the standard way to authenticate since September 2020 but legacy API keys are still supported, [instructions here.](getting-api-keys)

### 4. Submit an ocarina query and generate an OAuth token

Activate your Ocarina conda environment

```
conda activate ocarina
```

Attempt to access a biosample with the following command

```
ocarina --oauth get biosample --central-sample-id *Insert COG ID here*
```

You should then see the following message in your terminal

```
                                 .@ 888S
                            ;@S8888:8%tX
 :XS.                 .;8: @8t88888t8888
X8%%S:              .8 8S888    :8.88S@:
8;8;888:        :@; 888888@8    88%888
%8:8%X8 t8. ;8 888.X8    88S@88888S %
 888S@@888  8@888@S8C    888    S%S:
 .@%888%@@t.888@@8@8@8::X88C   88 %
  ;S@X8@888S8X@@X8X88X888888%@888;
  Xt88X@8@@XX8S8X88@88888S888S.;
  t S888X8S8S8888X88@88%8@:@8%;
  :888X   @888    @88S88S888X
 .88;.     %X8    8@88S8X8:
 S8@S8@   8t8888%8@:8%S@88
 8%8;88888S@%.8S88;@8% %.
 :8.8    888    8XS:%:
 ::8St   88;   88S8;
   ;t 8X.8;%8 8%
Hello YOUR-USERNAME.
Please request a grant via:
https://majora.covid19.climb.ac.uk/o/authorize/.................
Enter the full callback URL as seen in your browser window
```

Then Ctrl + click the majora URL to request a grant via OAuth, your browser should then open a page which looks similar to this:

![image](images/oauth_example.png)

Then click "Authorize" to confirm that you have indeed requested an OAuth token and you should see a page which looks like this apart from the text boxes will be populated:

![image](images/ocarina_example.png)

Now click the copy button next to the the upper text box to copy the callback URL.

Now paste the copied return URL into Ocarina which should now return your requested dataview.

### 5. Refreshing OAuth tokens

Now you have fully set up OAuth and Ocarina in order to keep using the same token you can refresh it with the command `ocarina oauth refresh`, these tokens expire after **10 hours after which you will have to repeat the process of generating a token by following step 4 again.**

Refreshing your OAuth token can be automated by using a `cron job` scheduled to run at any interval < 10 hours for convenience.
