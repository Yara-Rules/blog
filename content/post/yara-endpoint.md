---
title: "Yara Endpoint"
date: 2018-03-23T22:00:22+01:00
keywords: ["endpoint", "anti-malware", "anti-virus"]
tags: ["Go", "endpoint", "anti-malware", "anti-virus"]
draft: false
---

It's been long time without any updates here. Let's publish some news. Yara-Rules project is proud to anounce another interesting tool for the comunity, it is Yara-Endpoint. It is a tool that has been designed for helping incident handlers during their daily job.

As you may guess Yara-Endpoint is a tool that runs Yara remotely on endpoints. Well, that is a basic summarize for the whole project so let's explain it a little bit.

Yara-Endpoint is build using a classic client-server architecture. That means clients will be deployed on your assets and those clients are in charge of running Yara. On the other side, the server schedule tasks can be performed by the clients. You can manage yara rules and endpoints from server side and it allows you to see reports.


Let's see some images so you get a clear idea of everything.

{{< figure src="/img/yara-endpoint/dashboard.png" title="Dashboard" height="120" width="240" link="/img/yara-endpoint/dashboard.png" >}}
{{< figure src="/img/yara-endpoint/rule_details.png" title="Rule description" height="120" width="240" link="/img/yara-endpoint/rule_details.png" >}}
{{< figure src="/img/yara-endpoint/tasks.png" title="Task schedule" height="120" width="240" link="/img/yara-endpoint/tasks.png" >}}

Let's go deep with Yara-Endpoint.

### How they connect together
The server exposes a TCP port to comunicate with clients. When running the clients you must set the server IP and port.


### Client characteristics
The client is a standalone binary. It is not necessary to be installed and it is self-registered during the first run. Moreover, the client creates a configuration file that stores its ID.

The client performs Yara scans based on the server schedule so you can fire a Yara scan whenever you want from your server console to any connected client at any time you wish. Meanwhile, the client performs a keep-alive or ping-pong flow thus the server knows the client status.

### Server characteristics
The Server binds two ports, one for the comunication with the endpoints, which is a TCP connection. The other one is used for serving the administrative website. You can configure them but by default TCP port is 8080 and website port is 8000.

The server handles everything from the website interface. The main characteristics are:

- Manage Endpoints
  - It is also possible to tag endpoints. The idea behind this is to perform analysis to a grup of assets.
- Manage Rules
  - It is also possible to tag rules. The idea behind this is to perform analysis using a grup of rules.
- Shedule scans
  - At this point you are not able to schedule scan programaticaly. It has to be done manually.
- Reporting

### First steps with Yara-Endpoint
The unique requirement for Yara-Endpoint is MongoDB on the server side. There is no need to run the server with administrative privileges as long as you do not use a privilege port (below 1024). A part from that nothing else is needed. Well... you should run the server before the clients.

{{< figure src="/img/yara-endpoint/server.png" title="Booting up the server" height="240" width="480" link="/img/yara-endpoint/server.png" >}}

As we explained before the server binds to 0.0.0.0:8080 and localhost:8000. Once both processes are ready the server waits for clients.

Right now most of the logs are in JSON format, we are working to log everything in JSON format.

When running a client you will see something like this.

{{< figure src="/img/yara-endpoint/client.png" title="Booting up the client" height="240" width="480" link="/img/yara-endpoint/client.png" >}}

What you can see here is a self-register process. The client checks whether itself is registered or not and it starts a registration process because there is not a configuration file. When the registration is done the client sends the Ping command to the server so the server response with a pong.

{{< figure src="/img/yara-endpoint/server-pong.png" title="Server registers a client" height="240" width="480" link="/img/yara-endpoint/server-pong.png" >}}



### Your time
Well after this short introduction to Yara-Endpoint is time to play with it. We, from Yara-Rules, encourage you to install Yara-Endpoint in a test environment and play around. If you find any bug or you miss some functionality, please open an issue in our [github](https://github.com/Yara-Rules/yara-endpoint/).
