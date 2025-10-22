---
title: Toggle PSAs on Android
description: Learn about PSAs (Public Service Announcements) which are ads that can be served if there are no other ads to show on Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Toggle PSAs on Android

PSAs (Public Service Announcements) are ads that can be served as a last resort, if there are no other ads to show.

They are not enabled by default, but you can turn them on using the code shown below.

Turn on PSAs with the following code:

``` 
// Whether the ad view should show PSAs if there are no ads to
// show.
adView.setShouldServePSAs(true);
    
```
