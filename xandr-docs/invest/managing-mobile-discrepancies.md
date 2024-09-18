---
title: Microsoft Invest - Managing Mobile Discrepancies
description: In this article, understand the factors that might cause discrepancies in mobile advertising and how mobile impressions are counted.
ms.date: 10/28/2023
---

# Microsoft Invest - Manage mobile discrepancies

There are a few factors that can play a role in causing more discrepancies on mobile devices than in display advertising:

- Rapid user navigation away from loading ads (also known as "drop offs"), which could be more common on mobile devices due to touch-screen interfaces, swiping
- Varying degrees of support for rich media creatives by different combinations of mobile ad SDKs, operating systems, and devices
- Limited connectivity and bandwidth constraints that can affect how rich media creatives are loaded by apps, and how conversions are  attributed

## Count mobile impressions

For mobile impressions our ad server will wait longer to count an impression than it would for a standard display impression. This applies to all mobile creatives across all inventory types. This means that mobile apps using advertising SDKs such as [Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md) can pre-fetch rich media creatives before they need to be shown to the user. This pre-fetching by the SDK is performed due to the connection bandwidth and battery constraints that mobile devices operate under.

For example, a mobile game developer may wish to show advertisements between stages of a game app. The creative may be fetched from the ad server several minutes before actually being shown to a user when they complete a game level. Because our ad server waits several minutes to count the impression, the user finishes the game, views the creative, and Microsoft Advertising then logs the impression as expected, thus avoiding any discrepancy issues.

## Related topics

- [Welcome to Mobile](welcome-to-mobile.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)
