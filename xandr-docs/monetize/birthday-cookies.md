---
title: Microsoft Monetize - Birthday Cookies
description: Learn what is a Birthday Cookie and when it is generated. In this page, go through use cases for sellers and buyers for the birthday cookie.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Birthday cookies

The first time a user without one of our cookie visits a website where we serve ads, we set a cookie. We also add that user to the "Microsoft Advertising Birthday Cookie" segment. This segment appears in Monetize as "cookie_birthday (shared)" and its segment ID is 1.

This segment is not owned by any particular member; instead, we expose the birthday cookie segment to all members of the platform. In other words, it is a shared segment that any member can use. This document describes several example use cases for the birthday cookie segment; it also provides links to further documentation on segments, targeting, and conversion attribution.

## Use cases for sellers

Platform members do not have access to other members' segments, except in cases where there is a special arrangement. Even if a member does not have access to segments shared by external data providers or other platform members, the birthday cookie segment can serve as a useful heuristic when a seller is deciding how to set yield management price floors.

For example, even though you may not know what other segments a particular user is part of, you can guesstimate that a user who has been a member of the "cookie_birthday (shared)" segment for more than a week is probably rich in segment data, and thus more valuable to advertisers. Based on this information, you can configure your yield management floor rules to reflect the higher value of impressions served to this user. Conversely, you may drop floors for users whose "birthdays" are more recent.

## Use cases for buyers

Here are two buy-side use cases for the birthday cookie:

- As a buyer, it is often in your interest to target users who don't clear their cookies. This is especially true if you are running a performance ad campaign. In this case you may want to target users who have been members of the birthday cookie segment for more than a day, since that implies that they do not clear browser cookies, and thus conversions from these users are more likely to be attributed correctly.
- On the other hand, a buyer may wish to do the opposite: target users who have been members of the birthday cookie segment for very short periods of time—say, less than a day—on the chance that these users may be undervalued as a result of allegedly belonging to fewer segments.

 > [!TIP]
 > For instructions on how to implement segment targeting, see [Segment Targeting](segment-targeting.md).

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Working with Segments](working-with-segments.md)
- [Segment Targeting](segment-targeting.md)
- [Conversion Attribution](conversion-attribution.md)
