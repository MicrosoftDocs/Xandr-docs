---
title: Introduction to Mobile Advertising
description: Learn how advertising works on mobile devices. This page covers the types of mobile advertising and the different challenges faced.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---


# Introduction to mobile advertising

> [!TIP]
> For an introduction to the main concepts involved in online advertising, see [Introduction to Ad Serving](introduction-to-ad-serving.md).

Since mobile devices have become one of the primary ways people access the Internet, learning the basics of mobile buying is essential. The documentation in this section is designed to provide you with an understanding of how advertising works on mobile devices. If you're interested in a more technical explanation,
Xandr also provides a public [MRAID and Mobile Video Tutorial](mraid-and-mobile-video-tutorial.md) intended for audiences who need to work with our mobile offerings.

Mobile advertising is very similar to [web display advertising](online-advertising-and-ad-tech-glossary.md#display-advertising), with a few exceptions, which we'll discuss below.

## Types of mobile advertising

There are two kinds of advertisements for mobile devices:

- **Mobile web ads** appear in mobile web browsers the same way they do in desktop web browsers. Frequently browser ads, like the [publisher](online-advertising-and-ad-tech-glossary.md#publisher) websites that host them, are optimized especially for display on mobile devices.
- **In-app ads** (sometimes called "mobile app install ads") appear inside mobile apps as the user uses the app.  You can measure in-app success by the usual metrics such as [CPM](online-advertising-and-ad-tech-glossary.md#cpm) or [CPA](online-advertising-and-ad-tech-glossary.md#cpa), which measure cost per impression, view, or click. In-app success can also be measured by cost per install (CPI), sometimes also called "cost per download", a special type of acquisition unique to mobile devices.

## Mobile identification and targeting

In mobile web advertising, users are typically targeted and success is typically measured in the same way as [web display advertising](introduction-to-ad-serving.md).  For in-app advertising, users are identified by their mobile device IDs. The device ID, as its name implies, identifies users for all applications on the mobile device, unlike cookies, which are specific to each website. Different operating systems use different identifiers: IDFA (iOS), AAID (Android), and Windows Advertising ID(Windows). These identifiers were created specifically to be used for advertising and provide users the ability to opt out of identification by resetting their identifiers.  Identifiers are also reset if the operating system is reinstalled.

Note that the device ID cannot be linked to [personally identifiable information (PII)](online-advertising-and-ad-tech-glossary.md#personally-identifiable-information-pii).

In addition to the typical kinds of segment or browser targeting, mobile devices can be targeted by:

- Device type
- Carrier
- Latitude and longitude
- Connection type
- Operating system

Latitude and longitude, in particular, allow for precisely targeted advertising, such as advertisements from stores that are geographically close to the device user.

## Mobile targeting challenges

Currently, users cannot be reliably identified across multiple devices. This affects targeting and [frequency capping](online-advertising-and-ad-tech-glossary.md#frequency-capping). For example, if you see an ad multiple times from your Android phone and hit the frequency cap defined by the campaign serving that ad, you shouldn't see that ad anymore. If you switch to your iPad later in the evening for some bedtime reading, you won't be identified as the same user by the campaign, and you may see ads from that same campaign again. Frequency capping on mobile devices works on a per-device basis; in other words, if you switch devices, your frequency cap is reset.

As in web display advertising, it's difficult to identify users across different browsers on the same device. If the user switches mobile browsers, then frequency and recency will only apply on a per-browser basis.

## Related topics

- [Introduction to Ad Serving](introduction-to-ad-serving.md)
- [Ad Tags](ad-tags.md)
- [Creatives](creatives.md)
- [mraid-and-mobile-video-tutorial](mraid-and-mobile-video-tutorial.md)
