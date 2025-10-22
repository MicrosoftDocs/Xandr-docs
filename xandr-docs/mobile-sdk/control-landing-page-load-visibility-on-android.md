---
title: Control Landing Page Load Visibility on Android
description: In this article, learn instructions for configuring the landing page load behavior when ads are clicked on Android devices.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Control landing page load visibility on Android

This page has instructions for configuring the landing page load behavior on ad clicks. By default, the landing page loads in the background until the initial payload finishes loading and can present a fully rendered landing page to the user. Setting this to `NO` causes the in-app browser to become visible immediately and display the unrendered landing page.

> [!NOTE]
> If you're consistently experiencing slow clickthrough rates, try setting this property to `false`.

Use the `AdView.setLoadsInBackground(boolean)` method to determine whether, when an ad is clicked, the SDK loads the landing page in the background (the default is `true`):

``` 
bav.setLoadsInBackground(false);
```

Setting this to `false` will cause the in-app browser to immediately become visible and display the unrendered landing page. Setting this
to `false` when an ad redirects to the app store may cause the in-app browser to briefly flash on the screen.
