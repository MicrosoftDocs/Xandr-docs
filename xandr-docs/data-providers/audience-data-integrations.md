---
title: Audience Data Integrations
description: Learn steps involved in integrating user-based data into the Xandr platform. This page explains steps in the integration process. 
ms.custom: data-providers
ms.date: 11/29/2023
---

# Audience data integrations

This article describes the integration steps for user-based data into the Xandr platform.

## Integration steps

When integrating user-based data such as behavioral and demographic segments, the integration process involves the following steps:

> [!TIP]
> Make sure to use the Impression Bus endpoint `https://api.adnxs.com` for the API services (Segment, Batch Segment and Member Data Sharing) referenced in this section.

**Step 1.** Establish a mapping between Xandr's user IDs and your internal user IDs. User ID mapping can be done through either our getUID or mapUID pixels; in either case data providers are responsible for dropping the usersync pixel.

**Step 2.** Use your API credentials to [authenticate](../digital-platform-api/authentication-service.md).

**Step 3.** Create segments through the process outlined on the [Creating  & Managing Segments](creating-and-managing-segments.md) page. The [Segment service](../digital-platform-api/segment-service.md) exclusively permits you to create segments in your own member, not in your client's (the data buyer's) seats.

**Step 4.** Add user data to segments via the Batch Segment API service. Alternatively, adding user data to segments can be done through [Client Side Segment Calls](client-side-segment-calls.md). Remember that segments and users uploaded must exist on Xandr's platform for segment enrichment to be successful.

> [!NOTE]
> For best practices, see [Batch Segment Service Best Practices](../digital-platform-api//batch-segment-service-best-practices.md).

**Step 5.** Share segments with your client (the data buyer) using the [Member Data Sharing API service](member-data-sharing-service.md). It is important to note that you may only share segments that are housed in your data provider member.

If you are using the Batch Segment API service, there is also an alternative option, mainly used for 1st party segments, that does not require sharing segments from one member to another:

1. Have your client (the data buyer) create segments in their own member, through the [API Segment service](../digital-platform-api/segment-service.md) or Xandr's UI, and tell you the IDs (or codes, if you are using codes) of those segments.
1. Have the client submit a [support ticket](https://support.ads.microsoft.com) allowing you (the data provider) to populate their segments using Batch Segment.
1. Xandr will then permission you (the data provider) to populate these segments on behalf of the client.
