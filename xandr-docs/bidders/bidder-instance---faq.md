---
title: Bidder Instance - FAQ
description: In this article, explore answers to frequently asked questions about bidder instance, offering a clear and concise resource for optimizing your bidding strategy.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder Instance - FAQ

## Configuring bidder instances

### What is a bidder instance?

A bidder instance essentially represents the path from our datacenter to your datacenter(s), for each of our datacenters that you want to receive traffic from. An instance is also the object that is used for load balancing and connection management. When you set up a bidder instance, you are telling a Xandr datacenter that you want traffic from that datacenter.

### How do I set up a bidder instance?

Bidders must register bidder instances in order to receive traffic. Instances are created using the [Bidder Instance Service](bidder-instance-service.md). An instance is created using a POST to this service. When you create an instance, you must specify which Xandr datacenter it is associated with. Instances associate with NYM1, for example, will be eligible to receive traffic from this data center. You must also specify the destination for traffic sent using this instance. If you have three east-cost data centers, for example, you would want to set up at least one instance in the NYM1 data center for each of your three data centers.

## Using instances to receive traffic

### Can I receive bid requests to one instance and notifies to another?

No, every bidder instance must be able to receive both bid requests and notify requests.

### Do I need to set up bidder instances in the sandbox?

Yes, you must have bidder instances that are active and respond to the [Ready Request](ready-request.md) in the sandbox to receive traffic, just like in production.

### I have a bidder instance in NY that does not see any traffic from France

Xandr uses global load balancing to send an impression from a user to the closest Xandr datacenter to that user. We will then send a bid request to bidders that have bidder instances in that datacenter.

For example, if a user is in Australia, their impression would be sent to our Singapore data center. Only bidders with bidder instances in Singapore will receive the bid request for that impression.

To ensure you are able to receive traffic from France, you will need to register a bidder instance in our AMS datacenter.

### Will I automatically start to receive traffic when I set up a bidder instance?

When the instance is active, it means you want that instance to be considered in the set of instances our data center will evaluate to send traffic to. To receive traffic, a bidder instance must also respond to the [Ready Request](ready-request.md). If your instance doesn't respond to the ready request, then you won't get any traffic. When you send valid responses to the ready request, you will start to receive traffic to that bidder instance.

### Will all of my bidder instances receive every bid request?

No, a bid request will be sent to only one instance within a particular data center. These will be allocated based on availability at the time the bid request is sent. Note that European traffic could be routed through AMS and France datacenters, so if you need to receive all the impressions of a specific European seller as you'll want to use at least an AMS instance and a France instance.

### Can I use a hostname instead of an ip address for my bidder instance?

Yes, you can use the [Bidder Instance Service](bidder-instance-service.md) to assign as hostname to your bidder instance.

### Can I set a QPS cap?

Yes, we have a QPS Safety product that allows you to set a hard limit on incoming traffic. You can enable a QPS cap through the [Bidder Instance Service](bidder-instance-service.md).

## Related topics

- [Bidder Instance Service](bidder-instance-service.md)
- [Integrate a Bidder](integrate-a-bidder.md)
