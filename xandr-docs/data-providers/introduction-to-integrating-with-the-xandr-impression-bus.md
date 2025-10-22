---
title: Introduction to Integrating with the Xandr Impression Bus
description: In this page, learn about the various pointers to consider while integrating with the Xandr impression bus. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Introduction to integrating with the Xandr impression bus

When considering integrating with the impression bus, there are many things to consider. Most people underestimate the volume of requests that Xandr has to offer and the infrastructure required in order to properly process those requests efficiently.

## Our Impression Bus’ connection management behavior

The Xandr impression bus has a very efficient connection management model that is built to maximize requests per connection in a dynamic, horizontally scalable model. It currently has over a thousand instances running that process our ad traffic. When integrating one of your instances (a unique IP+Port combination) through our API, this instance is added to a round robin list of all of your instances. The impression bus will round robin requests to all of these instances, sparing you from having to manage load balancing.

The impression bus will establish connections from all of our instances to each one of your unique instances, averaging ~1600 connections today. Each connection will have a ready request expecting a “1” response, and then will expect to utilize that same connection to send hundreds of requests (generally 300 queries per connection). The number of connections and which connection to utilize for each request is determined dynamically in order to effectively leverage all of our impression bus instances without bogging down our systems.

As our volume grows, the number of instances in our impression bus will grow, and therefore the number of connections established to each of your instances will grow. It is important to keep an eye on this and have your listeners configured to accept all of the connection attempts being made.

> [!NOTE]
> Bid requests and bid responses are synchronous, so there is no possibility of a race condition between the impression bus and bidders. Because of the sheer volume of traffic that goes through Xandr, your bidder may receive an apparently constant stream of requests from the impression bus, but requests are only sent once responses have been received for previous requests (bid responses are not associated with bid requests by order of issuance). That said, after the impression bus has waited for 10ms for a bid response it will time out and close the connection to the data provider bidder. This means that the data provider bidder will not have the opportunity to respond to the bid request that timed out (the bid request will go unanswered).

## Architecting a solution

Too many people do not value the phase of architecting a solution before they begin tackling it. Whether you are building a bidding solution or looking to integrate data, the biggest mistake you can make is architecting and building the software without considering the environment as a whole, including the layers that must function below the software. Before you begin coding, be sure you have laid out all the pieces necessary for your solution. This article covers the commonly missed aspects outside of your proprietary software to aid you in proper planning and realizing the magnitude and scope of this integration.

## Server specifications

There are three components to consider when deciding the appropriate hardware to run: CPU, RAM, and disk. CPUs require the least thought as most server-class CPUs today are able to successfully manage operations thrown at them. When deciding on the amount of RAM required, consider the size of your database and the amount of RAM you will need to store that database (or at least a healthy cache) within RAM. Also, consider the amount of RAM required to temporarily store approximately a day’s (or so) worth of log data. I will explain this later. Disk is also an important consideration for long-term storage.  There should be enough storage capacity to store your log-level data long-term. **Disk should not be where you are storing your logs in real-time or where the database that is being accessed in real-time is stored.**

## Software stack

To begin, let us be sure to decouple two very distinct pieces of this stack, your listener and your application. The listener is there to listen for requests being sent from our impression bus. Conventional wisdom has most engineers running web serving software to handle this; however, this is not a web server. I want to be sure that point is made clear. Web serving software is built to manage connections that stay open for the shortest amount of time possible due to the potential of millions of users connecting to your server. In this scenario, you are integrating with a known set of users, the servers in our impression bus equaling ~1600 connections today (but growing as our impression volume grows).

The impression bus will establish a connection, utilize keep-alive, and attempt to send thousands of requests over that same connection in order to be as efficient as possible. This is equivalent to a user base connecting to a web server and clicking refresh thousands of times per second. If your listener is not configured to handle this behavior appropriately, it will be overwhelmed. Web serving software can be configured to handle this form of traffic, but it is recommended to develop your own listener that is built specifically for this behavior.

> [!NOTE]
> Apache has proven to be able to handle our impression bus’ traffic quite well if configured correctly. If utilizing Apache as your web serving software, the keys lie in your keep-alive settings and having Apache as lightweight as possible. Most system administrators may consider these settings as extreme, however realize again that this is not a web server and therefore will not be configured as such.
>
> Timeout 150
>
> KeepAlive On
>
> MaxKeepAliveRequests 50000
>
> KeepAliveTimeout 150
>
> These settings will allow Apache to maintain open connections and have our impression bus manage closing those connections. This is important in order to save load on your systems. When your system is managing closing/opening multiple connections, it will be very difficult for it to keep up with the tens of thousands of requests per second it needs to manage. Apache also loads many unnecessary modules by default. Commenting out extraneous modules will allow Apache to run in a more lightweight fashion, allowing it to be more efficient. Finally, before you're integrated with our platform, you can use the Apache "ab" tool to stress test your servers.

**The key takeaway to remember is the behavior of our impression bus. As long as the listener that was used is built to manage the impression bus’ behavior, you will be successful in scaling your volume.**
