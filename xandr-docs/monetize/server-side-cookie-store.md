---
title: Microsoft Monetize - Server Side Cookie Store
description: Explore server-side cookie store for web app control/security. Sync user data across platforms for consistent ad campaign targeting.
ms.date: 10/28/2023
---

# Microsoft Monetize - Server side cookie store

User data, such as segments and how many times a user has seen a particular creative, is a big part of the targeting and decision-making process for most campaigns. For this reason we need to maintain consistent and comprehensive data about a user no matter where, when, or how we are "seeing" them across the Internet landscape.

Traditionally user data is stored in the user's browser cookie, but in many auctions, Microsoft Advertising does not have access to the browser. (For example, when we are passed a server-side ad call from an exchange.) So how do we both recognize that user, and access their relevant user data across multiple sites and platforms? To do this, we designed the Microsoft Advertising cookie store, a server-side user data storage system. With the cookie store and user syncing, we are able to:

- Sync user ID and frequency data across all Microsoft Advertising supply partners.
- Store cookie data, both yours and ours, server side, so that it is accessible on every ad call.

  > [!NOTE]
  > For an exact listing of the cookies set by the Microsoft Advertising Platform, and detailed information on what they contain, see [Cookies](http://appnexus.com/cookies).

## Mapping user IDs

If we had a tag from Microsoft Advertising on every page for every impression that passed through our platform, we would have access to the cookie for every user we see. But we don't.

Let's say we are passed inventory through a server-side integration with Google Ad Manager, and so Google Ad Manager has access to the cookie but we do not. When Google Ad Manager passes us an ad call, they ID the user as ABC. Yahoo Ad Exchange calls the user 123, and AdMeld uses 007. We need to know that this is all the same user so that we can apply any relevant data and properly regulate frequency targeting.

The exact method of ID mapping differs depending on our integration partner. We may perform the map through a pixel on the publisher's page, or by serving an ad to the user. We may store the User ID mapping in our database or they might store it in theirs. Here are a few example integrations.

- Ad Network X stores the mapping in their database. Network X places a pixel on their publishers' pages, including mysite.com. When a user visits mysite.com, the pixel fires and Microsoft Advertising is able to mark the user as 1938 in the user's browser cookie. The pixel also redirects to Network X to let them know that Microsoft Advertising calls this user 1938 so that it can be mapped to the Network's User ID and stored for future use.
- Exchange Y stores the mapping in their database, but they don't put our pixel on the page. Instead, the first time we serve an ad to this user, we fire a usersync pixel that adds a unique user ID to the user's browser cookie, and redirects to pass the user ID to Exchange Y.
- For Exchange Z, Microsoft Advertising stores the ID map. In this case, the first time Microsoft Advertising serves an ad to a user, we fire off a pixel to Exchange Z, who then passes us their user ID, which we store. Now on future impressions, Exchange Z sends us their user ID, and we can look it up in our database.

## Cross datacenter syncing

One thing we are highly focused on is making sure all user data is available in all Microsoft Advertising data centers. We currently have datacenters in Los Angeles, the New York metro region, and Amsterdam, and users are routed to the topologically closest one. This means that users in the middle of the United States might be sometimes routed to New York and sometimes Los Angeles. Or, in the event of a networking blip at one datacenter, all traffic would be routed to the other datacenter.

Let's say we have a user in North Dakota who sees a creative six times. Three of those times the user was routed to the New York datacenter, and three of those times they were routed to LA.

On the seventh impression, the user is routed to New York. We need to know that they have already seen this creative six times, rather than the three times that were recorded in New York. Therefore, we designed our LAX and NYM datacenters to synchronize by passing segment data back and forth, while AMS retains its own cookies exclusively.

## Server-side segment data storage

Segment data, whether passed in through a [segment](working-with-segments.md) or through an offline transfer, is stored in the Cookie Store instead of the user's browser. This way segment data is available across all inventory sources, third party exchanges, and inventory aggregators.

You can also update segment data at any time without having access to the user via our Batch Segment API.

## Related topic

[User ID Mapping with getUID and mapUID](user-id-mapping-with-getuid-and-mapuid.md)
