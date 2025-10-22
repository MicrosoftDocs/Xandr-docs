---
title: Pass Custom Keywords on Android
description: This article provides information on passing custom keywords on Android. Custom keywords are used to attach arbitrary key-value pairs to the request body of the ad call.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Pass custom keywords on Android

Custom keywords are used to attach arbitrary key-value pairs to the request body of the ad call. These can be used for several purposes, including:

- Custom campaign targeting options (see [Key-Value Targeting](../digital-platform-api/custom-key-value-targeting.md) for more information)
- Reporting (see [Key Value Analytics Report](../digital-platform-api/key-value-analytics-report.md))

The following line of code adds a single key-value pair to the JSON body of the ad call:

```
// Add key foo with a single value (bar).
adView.addCustomKeywords("foo", "bar");
```

For a more robust/complex setup, you can pass multiple values for the same key in the ad call. To do this, call `addCustomKeywords` multiple times with the same key:

```
adView.addCustomKeywords("foo", "bar");
adView.addCustomKeywords("foo", "baz");
adView.addCustomKeywords("foo", "foe");
adView.addCustomKeywords("customkey", "bar");
```
