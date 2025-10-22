---
title: Configure SDK Logging on Android
description: In this article, find the instructions to turn logging on and off, and to set logging levels on Android SDK.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Configure SDK logging on Android

This article has instructions for turning logging on and off, and for setting logging levels.

Depending on your Mobile SDK version (whether it is RC 1.21 or newer), the configuration of logging mechnism changes. In RC 1.21, the SDK uses the native Android logging system properties. For more information, see the section below that corresponds to your SDK version.

## RC 1.21 and above

As of RC 1.21, Android's logging system properties are used instead of the SDK's built-in `Clog.clogged`.

To turn on the SDK's logging during development, connect the device via USB and issue the following command from your terminal:

```
$ adb shell setprop log.tag.OPENSDK VERBOSE
      
```

The logging setting will remain in effect until the device reboots.

For more information about how log tags work on Android, see the documentation for [Log.isLoggable()](https://developer.android.com/reference/android/util/Log).

For more information about how to use ADB shell commands, see [ADB Shell Commands](https://developer.android.com/tools/adb#shellcommands).

## RC 1.20 and below

In versions RC 1.20 and below, by default, SDK logging is turned on. You can turn it off as follows:

```
// Turn off the log messages emitted by the SDK.
Clog.clogged = true;
    
```
