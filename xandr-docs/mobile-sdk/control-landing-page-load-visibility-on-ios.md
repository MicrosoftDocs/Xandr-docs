---
title: Control Landing Page Load Visibility on iOS
description: In this article, learn instructions for configuring the landing page load behavior when ads are clicked on iOS devices.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Control landing page load visibility on iOS

This page has instructions for configuring the landing page load behavior on ad clicks. By default, the landing page loads in the background until the initial payload finishes loading and can present a fully rendered landing page to the user. Setting this to `NO` will cause the in-app browser to immediately become visible and display the unrendered landing page.

> [!NOTE]
> If you're consistently experiencing slow clickthrough rates, try setting this property to `false` (Android) or `NO` (iOS).

Use the `ANAdProtocol`'s `landingPageLoadsInBackground` flag to determine whether, when an ad is clicked, the SDK loads the landing page in the background (the default is `YES`):

``` 
banner.landingPageLoadsInBackground = NO;
```

Setting this to `NO` will cause the in-app browser to immediately become visible and display the unrendered landing page. Setting this to `NO` when an ad redirects to the app store may cause the in-app browser to briefly flash on the screen.
