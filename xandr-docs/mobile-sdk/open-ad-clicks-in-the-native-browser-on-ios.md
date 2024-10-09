---
title: Open Ad Clicks in the Native Browser on iOS
description: This article provides information on how to open ad clicks in the native browser on iOS. By default, the SDK will open clicks in an in-app browser.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Open ad clicks in the native browser on iOS

You can choose whether the device's native browser will open if the user clicks an ad in this view. By default, the SDK will open clicks in an in-app browser.

To cause a specific ad creative to open in the native browser, use the [ANJAM API](anjam-user-guide.md).

Use this code to open the device's native browser when the user clicks an ad:

```
banner.clickThroughAction = ANClickThroughActionOpenDeviceBrowser;
```

> [!NOTE]
> The `banner.opensInNativeBrowser` has been deprecated as of Mobile SDK version 5.0.
