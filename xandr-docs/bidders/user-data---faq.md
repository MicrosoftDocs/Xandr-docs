---
title: User Data - FAQ
description: Explore addressing user data concerns, synchronize user IDs by storing mapping tables on servers, utilize /getuid pixel, incorporate user ID in redirect URL.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# User data - FAQ

This page has answers to frequently asked questions about user data.

## Cookie matching

### How can I sync user IDs with Xandr?

To sync user IDs, either you or Xandr must store the mapping table. If you would like Xandr to store the mapping table, please contact your Xandr representative.

To store the mappings on your servers, you will use the `/getuid` pixel. The `/getuid` pixel will populate the `$UID` macro with the Xandr user ID and redirect to the specified URL. The format is: `https://ib.adnxs.com/getuid?REDIRECT_URL`. The redirect must contain the user ID macro, in the format `$UID`, with the ID we have for that user. The example call below will result in the following:

1. Direct the user to
  `https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID`
1. Replace the `$UID` macro with `12345`
1. Redirect the user to a`https://ad.adserver.com/pixel?adnxs_uid=12345`

### Do you have the same user pool in your US and EU data centers?

No, the US data centers have one pool of user data and the EU data centers have another. This means that Xandr user ID 12345 in the US is different from Xandr user ID 12345 in the EU.

## Filtering

### How can I only see users that I have a cookie match for?

This is a multi-step process:

1. Create a segment (you can do this in the [Bidder UI](https://bidder.xandr.com)).
1. Populate the segment using segment adds (see below). If you are interested in having Xandr drop your usersync pixel, please reach out to your Xandr representative.
1. When you are confident that the segment has been sufficient filled, add this segment to your bidder profile.

## Segments

### How do I add a user to a segment?

Xandr users can be added to segments using a [Segment Pixel](../monetize/working-with-segments.md). The segment can be created through the UI [https://bidder.adnxs.net](https://bidder.adnxs.net) in the Segments tab. You must create a segment before adding users via the segment pixel. When you create the segment, Xandr will define a unique ID. You may also specify a code, which will be your unique identifier for that segment.

To add users to a segment or several segments, a segment pixel must be fired and must identify all the segments to which that user will be added. For example:

`<img src="media/seg?add=101,102,104" width=1 height=1/>`

This will add a user to segments 101, 102 and 104. The example below will add a user to segments using the segment codes. When using codes, you must specify your member ID.

`<img src="media/seg?add_code=auto1,travel5&member=10" width=1 height=1/>`

### How do I remove a user from a segment?

Xandr users can be removed from segments using a [Segment Pixel](../monetize/working-with-segments.md). When you create the segment, Xandr will define a unique ID. You may also specify a code, which will be your unique identifier for that segment.

To remove users from a segment or several segments, a segment pixel must be fired and must identify all the segments from which that user will be removed. For example:

`<img src="media/seg?remove=101,102,104" width=1 height=1/>`

This will remove a user from segments 101, 102 and 104. The example below will remove a user from segments using the segment codes. When using codes, you must specify your member ID.

`<img src="media/seg?remove_code=auto1,travel5&member=10" width=1 height=1/>`
