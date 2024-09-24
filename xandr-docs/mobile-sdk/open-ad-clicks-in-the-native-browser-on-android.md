---
title: Open Ad Clicks in the Native Browser on Android
description: This article provides information on how to open ad clicks in the native browser on Android. By default, the SDK will open clicks in an in-app browser.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Open ad clicks in the native browser on android

You can choose whether the device's native browser will open if the user clicks an ad in this view. By default, the SDK will open clicks in an in-app browser.

To cause a specific ad creative to open in the native browser, use the [ANJAM API](./anjam-user-guide.md).

Use this code to open the device's native browser when the user clicks an ad:

```
adView.setClickThroughAction(ANClickThroughAction.OPEN_DEVICE_BROWSER);    
```
