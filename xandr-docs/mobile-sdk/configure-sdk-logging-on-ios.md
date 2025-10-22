---
title: Configure SDK Logging on iOS
description: In this article, find the instructions to turn logging on and off, and to set logging levels on iOS SDK.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Configure SDK logging on iOS

This page has instructions for:

- turning logging on and off, and for setting logging levels
- enabling subscription for notifications as well as retrieving notification status

## Enable and set the logging level

You can use below methods on the `ANLogManager` interface to set the logging level of the iOS SDK:

- `getANLogLevel`
- `setANLogLevel`

**Example**

```
[ANLogManager setANLogLevel:ANLogLevelDebug];
```

> [!NOTE]
> See `ANLogManager.h` for all available log levels.

## Enable and disable notification observer and retrieve notification status

Additionally, you have an option to enable logs to be posted as notification if your app wants to ingest these logs and do further processing. You can use below methods on the `ANLogManager` interface to set and retrieve the notification status of the iOS SDK logs:

- `setNotificationsEnabled`  
- `isNotificationsEnabled`

  ```
  /**
   Enable to subscribe for Notifications
   */
   + (void)setNotificationsEnabled:(BOOL)enabled;
   /**
  Get Notification Status
   */
   + (BOOL)isNotificationsEnabled;
  ```

**Example**

```
// To Enable Notifications Observer
[ANLogManager setNotificationsEnabled:YES];
// To get the status of current Notifications Observer
[ANLogManager isNotificationsEnabled]
```
