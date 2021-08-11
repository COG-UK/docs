---
layout: docpost
title: Creating an OAuth application
date_published: 2020-09-11 10:00:00 +0000
date_modified:  2020-09-11 10:30:00 +0000
author: samstudio8
maintainer: samstudio8
---

### Registering Ocarina with Majora

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

***

### Registering an OAuth application with Majora

If you want an applicaton to perform actions as a Majora account holder, you need to register an application.
Note that the testing and real versions of Majora are entirely separate, and so are the OAuth systems.
The locations to register an application are:

* [Test Majora (MAGENTA)](https://covid.majora.ironowl.it/o/applications/)
* [Real Majora (COG-UK)](https://majora.covid19.climb.ac.uk/o/applications/)

Click "New application" and fill out the form as appropriate:

* `Name` A name for your application, we do not enforce naming but suggest: `username-{application}` so that you can distinguish your application from others.
* `Client ID` Do not alter this
* `Client Secret` Do not alter this
* `Client type` set to `confidential`
* `Grant type` set to `authorization code`

Finally, if your application has a web-based front end, you can specify a callback for authorised requests to automatically flow to - along with a grant token.
If you do not have one, we provide a basic callback that will expose the grant code.

* `Callback` should be set to one of the following, based on whether this is a testing or production application:
    * Test: https://covid.majora.ironowl.it/o/callback/
    * Real: https://majora.covid19.climb.ac.uk/o/callback/
    * Do not skip `https://` or the final `/`.
    
 [As per NHS digital guidelines](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis#top), we only allow applications that use the authorization code flow.
 
 **If you are following [setting up ocarina](setting-up-ocarina) go back to that document at this point.**

### Basics

Once you have an application, the authorisation flow can be summarised as follows:

#### 1. Ask for a user to give permissions to your application (e.g. your copy of Ocarina)

* You must direct a user to the `/o/authorize/` endpoint, specifying the following URL parameters:
    * `response_type`: must be `code`, no other options are permitted
    * `client_id` : your application's public client id (do not send the secret)
    * `state`: your application should generate a random value, it will be returned to the callback for comparison later
    * `redirect_uri`: the URL-encoded `callback` endpoint
    * `scope`: the permissions (see later) to request from the user
* The user will log-in with their password and 2FA, then see a page describing the your application and the permissions requested.
* If the user authorises your application, they will be directed to the specified callback and receive a `grant` and a copy of `state`. Your application should determine the `state` received is the same as the `state` you sent.

#### 2. Convert the new grant token to an access token

* You must act quickly, the `grant` is valid for 60 seconds. Your application is responsible for converting the grant token into an access token.
* To convert a grant token into an access token you must `POST` to the `/o/token/` endpoint, with the following payload:
    * `grant_type`: must be `authorization_code`
    * `code`: the grant code sent to the callback in the previous step
    * `redirect_uri`: the same URL-encoded callback endpoint
    * `client_id`: your application's Client ID
    * `client_secret`: your application's secret (you must keep this safe)
    
#### 3. Receive an access token

* If all is well, the token endpoint will reply with a JSON struct:
    * `access_token`: your access token
    * `expires_in`: the number of seconds the access_token is valid for
    * `refresh_token`: the refresh token to use to get a new token
    * `token_type`: should be `Bearer`
    
    
#### 4. Use the access token

You will need to send a `Authorization` header formatted: `Bearer TOKEN` where `TOKEN` is your `access_token`.
All API endpoints in the `v2` API support OAuth and rotating API keys.

API requests must continue to include the `username` and `token` in the request data, though these are not
checked (this is just a feature that enables backward compatibility).

#### 5. Refresh the access token

* To refresh a token you must post to the `/o/token/` endpoint with the following payload:
    * `grant_type`: must be `refresh_token`
    * `refresh_token`: your `refresh_token`
    * `client_id`: your application's Client ID
    * `client_secret`: your application's secret (you must keep this safe)

If successful, you'll see the same JSON struct as step 3. Store the new access token and refresh token to repeat. You can automate this process easily through `cron` to keep your token rotated.

* Refreshing a token will immediately invalidate the corresponding access token.
* Currently, refresh tokens do not expire, but we plan to introduce a longetivity (weeks+).


### Scopes 
You must request at least one `scope` from a user. Every scope maps to a user permission in Majora.
A user can only authorize an application if they have been granted all the permissions for all scopes requested.
When specifying `scope` in Step 1, scopes must be separated by an URL-encoded space (`%20`).

Currently, OAuth scopes only cover the functionality provided by the uploader tool (e.g. biosamples and their collections, sequencing libraries and their pooling events and seqencing runs). To simplify matters during this trial phase, just request all scopes to cover these activities:

```
majora2.add_biosampleartifact
majora2.change_biosampleartifact
majora2.add_biosamplesource
majora2.change_biosamplesource
majora2.add_biosourcesamplingprocess
majora2.change_biosourcesamplingprocess
majora2.add_libraryartifact
majora2.change_libraryartifact
majora2.add_librarypoolingprocess
majora2.change_librarypoolingprocess
majora2.add_dnasequencingprocess
majora2.change_dnasequencingprocess
```

These will change and be expanded as we continue to integrate OAuth to the rest of the system.

### More information

* [NHS digital tutorial on user restricted APIs with helpful cURL examples for requesting tokens](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/user-restricted-restful-apis-nhs-identity-combined-authentication-and-authorisation#tutorial)
    
### Common pitfalls

* Incorrectly URL-encoded `redirect_uri`, or the callback URL you have registered is missing a terminating `/`.
* Taking too long to convert the grant code to an access token, they are valid for 60 seconds.
* Trying to use a grant code to authorize yourself against the API, you need to convert a grant to an access token.
* Trying to use a grant code after you have asked for another one (requesting a new grant will invalidate existing grants).
* Not sendng the `Authorization` header to the API.
* Trying to use an access token that you have refreshed.
