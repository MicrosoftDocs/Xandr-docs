---
title: Microsoft Monetize - Impression Counting
description: In this article, learn how Microsoft Advertising counts impressions and find a list of media types with their respective look-back windows.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Impression counting

Microsoft Advertising counts an impression, and records payment to the seller, once we receive an "accept call", which notifies us that a creative was served to the web page or mobile app. Because the amount of time between when an impression is requested and when the creative is served varies by media type, we have defined appropriate look-back windows for each media type.

This flexible approach is especially important for media types like mobile video, which can pre-cache an ad long before the ad is actually served, as well as interstitial and native media types that require a longer window than standard formats.

> [!NOTE]
> Impressions are reported on in the hour in which the creative was served to the web page or mobile app, not the hour in which the impression was request.

| Media Type | Look-Back Window |
|---|---|
| Banner | Up to 5 minutes after request |
| Expandable | Up to 6 hours after request |
| Interstitial | Up to 6 hours after request |
| Native | Up to 6 hours after request |
| Pop-up | Up to 5 minutes after request |
| Skin | Up to 5 minutes after request |
| Text | Up to 5 minutes after request |
| Video and Audio | Up to 6 hours after request |
