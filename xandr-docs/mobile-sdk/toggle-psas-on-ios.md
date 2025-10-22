---
title: Toggle PSAs on iOS
description: Learn about PSAs (Public Service Announcements) which are ads that can be served if there are no other ads to show on iOS.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Toggle PSAs on iOS

PSAs (Public Service Announcements) are ads that can be served as a last resort, if there are no other ads to show.

They are not enabled by default, but you can turn them on using the coden shown below.

``` 
// Whether to serve PSAs if there are no ads.
banner.shouldServePublicServiceAnnouncements = true;
    
```
