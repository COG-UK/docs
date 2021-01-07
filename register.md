---
layout: docpost
title: Registering to upload metadata and/or sequence
date_published: 2020-07-20 12:30:00 +0000
date_modified:  2021-01-07 12:00:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Quick links

* [Majora/CLIMB-COVID registration form](https://majora.covid19.climb.ac.uk/forms/register/)
* Users who registered without an SSH key need to [to update their Majora profile](https://majora.covid19.climb.ac.uk/forms/account/) **and** notify the `#account-requests` Slack channel. Please do not raise issues about permission denied errors if you did not provide an SSH key with your initial registration.
* Slack requests must be made through the Slack interface. To do this, click the name of the Slack instance on the top left and select "Invite people to...". Make sure you provide full name, institutional email and a valid reason for invite, or the request will be ignored. The CLIMB team are not responsible for approving Slack invitations so please do not message about Slack requests in `#account-requests`.


### Request access to CLIMB to upload metadata and/or sequence data
Request access by filling out the [registration form](https://majora.covid19.climb.ac.uk/forms/register/). If your organisation is not listed, please speak to Sonia Goncalves.

When asked on the form for an e-mail address, you must provide an email address that matches the domain one would expect to see for your organisation. We will ignore requests from personal email accounts (e.g. hotmail).
If you are the site lead, this email must match the email address Sonia has on file for you.

If you are only providing metadata or authorising users, you should leave the SSH Public Key box empty.

If you need access to CLIMB for uploading sequence data or performing analysis you will need to provide an SSH key.
The system only accepts `ed25519` keys. You can generate one from the command line with the following command:

```
ssh-keygen -o -a 100 -t ed25519
```

**Your key must be protected with a passphrase**. Command line generators will typically prompt you for this.
PuTTYgen users must fill out the _Key passphrase_ box on the client and select _ED25519_ in the parameters box.

**You will not be able to upload data until your key has been added to the server.**  
**Your username will begin with <code>climb-covid19-</code>. Remember to use this prefix when accessing systems later.**
**The server accepts public SSH keys only. You will not be allowed to login with a password.**

Once you submit your registration, a nominated user from your site will vet your request and approve you. Once approved by your site, your request will be processed by the system administrator and your account will be activated. You will be e-mailed when your account is activated.

For questions and assistance with registration, please use the `#account-requests` Slack channel.
