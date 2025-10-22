---
title: iOS Mediation Overview
description: In this article, learn about iOS mediation and how to mediate an iOS app for the latest release.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# iOS mediation overview

Mediation lets you sell ad impressions through multiple networks to generate more revenue. This is initiated by your main (mediating) SDK which calls out to one or more mediated SDKs in a "waterfall"-like process. If your main SDK can't show an ad for some reason, it can iterate over the list of mediated SDKs and contact them in the order you specify. This will continue until the impression is filled or you've run out of mediated SDKs.

Reasons to mediate to another SDK include the following:

- To provide better monetization under specific circumstances.
- To provide access to information such as a unique user ID or the device's operating system, location, or ID.
- Some networks only accept requests from their own SDKs, forcing you to use their SDK to access their demand.

This section describes how to mediate your iOS app for our latest release.

| Topics | Description |
|:---|:---|
| [Mediate with iOS SDK](mediate-with-ios.md) | How to mediate with networks and media types. |
| [iOS Custom Adapters](ios-custom-adaptors.md) | How to call out to another SDK installed on the same device. |
