---
title: Client Side Segment Calls
description: Segment data is written to and read from the server-side cookies store as well as to and from each user's browser cookie. Learn how a client side segment pixel call will always return a 1x1 invisible GIF image unless piggyback pixels are specified. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---


# Client side segment calls

## Client side segment calls

Segment pixels are the mechanism for categorizing users into groups (segments) so that they can be targeted by a campaign. Segment data is written to and read from the server-side cookies store as well as to and from each user's browser cookie. The Xandr segment call looks like the below:

`<img src="media/seg?add=12345,67890" width="1" height="1"/>`

where 12345 and 67890 are the IDs for two segments.

A client side segment pixel call will always return a 1x1 invisible GIF image unless piggyback pixels are specified.

## Codes

You may wish to refer to your segments using "codes" rather than the Xandr segment ID. These codes can be custom specified to match your internal naming or identification. To use segment codes instead of IDs in your segment calls, replace "add" with "add_code". Since codes are unique across a single member, rather than platform-wide, it is necessary to specify the ID for the member who owns the segment. For example, the tag may look like the below:

`<img src="media/seg?member=123&add_Code=abcde,fghij" width="1" height="1"/>`

Codes may contain any alphanumeric character, underscores ("\_") or hyphens ("-"). Currently, periods (".") are not supported in segment codes.
