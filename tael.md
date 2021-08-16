---
layout: docpost
title: The COGUK Transport for Announcing Ephemeral Logs (TAEL)
date_published: 2020-07-16 12:00:00 +0000
date_modified:  2021-08-16 14:30:00 +0000
author: samstudio8, BioWilko
maintainer: samstudio8, BioWilko
---

# Basics
There is a need for pipelines and processes within the consortium to communicate with one another.
Sam Nicholls has tried to address this for COGUK and has deployed an `mqtt` based solution referred to as `Tael`.
The `mqtt` model involves running a central messaging server called a **broker**, an example is currently being run on the COVID19 shared node.
Any `mqtt` compatible **client** can connect to this network and send/receive messages.
Messages are sent to the broker and must specify a **topic** (imagine this like a mandatory subject line in an email); clients can subscribe to specific topics that might be of interest to them.
For example, a client that controls a downstream pipeline might subscribe to a topic about the status of the inbound pipeline, and so on.

# Joining the network

### Implementing a client

To join the Tael network, you need a valid client.
A basic client that can access `Tael`, subscribe to a topic, automatically export the payload to the current OS environment, and run a shell command is available in the `/cephfs/covid/software/sam/public/mqtt-client.py` directory in CLIMB.

This must be used from a clean conda environment which can be set up with the following commands:
```
$ conda create -n tael-messenger python=3.7
$ conda activate tael-messenger
$ pip install paho-mqtt
```

You can set up a client which will listen to a topic with the following commands:

```
$ conda activate tael-messenger
$ python /cephfs/covid/software/sam/public/mqtt-client.py -c <COMMAND HERE> -t 'COGUK/<TOPIC HERE>/status' --who <YOUR USER HERE>
```
The `-c` argument should be a command which will be executed when the topic receives a message with the attribute `status finished`.

---
### Sending a message

Send a test mesage with the following:

```
$ conda activate tael-messenger
$ python /cephfs/covid/software/sam/public/mqtt-message.py -t 'COGUK/<TOPIC HERE>/status' -attr date YYYYMMDD -attr elan_date YYYYMMDD --attr status finished
```
Where `YYYYMMDD` is todays date in that format.

This should trigger the client you set up in the previous step (as well as printing on `#tael-stream`).

# Testing the network

Every five minutes, a client on the network sends a message to the `COGUK/test/beacon` topic.
The payload is a string that can be coerced to JSON (e.g. in Python you can use `json.loads(msg.payload)`) that contains three keys: `date`, `time` and `status`. The `date` and `time` values are strings containing the undelimited current date and time of the shared server (note the server time is `UTC`).
The `status` value of the test message is always `finished` as the default behaviour of the example client performs actions only when the `status` in the payload is `finished`. 

```
{
    "date": "20200716",
    "status": "finished",
    "time": "115001",
}
```

# Status

This subproject of COGUK is under development. Sam has been working with downstream pipeline authors to connect the inbound pipeline to other core components of the consortium response.
Tael's primary goal and focus will be to facilitate interpipeline communication, but it could be used for almost anything within COGUK.
That said, Sam will provide no active support for developing clients and messages at this time.
Note that Tael is running only as a proof of concept at this time and should not be relied upon for any element of service.
Be aware that the properties of the network can and will change at any time.

You can watch the messages being sent around the network with fascination by joining `#tael-stream`
