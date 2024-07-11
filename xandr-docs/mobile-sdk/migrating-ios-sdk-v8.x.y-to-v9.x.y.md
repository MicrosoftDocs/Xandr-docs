---
title: Migrating iOS SDK v8.x to v9.0.0
description: Learn how to integrate the latest Mobile SDKs for iOS using CocoaPods, Carthage, XCFramework, and Swift Package Manager.
ms.custom: ios-sdk
ms.date: 07/09/2023
---

# Migrating iOS SDK v8.x to v9.0.0

> [!NOTE]
> Refer to the detailed integration guide for first time implementations in the [iOS SDK Integration Instructions](ios-sdk-integration-instructions.md).

Starting with SDK v9.0.0, there are no longer release source code updates for the Android/iOS Mobile SDKs on GitHub. Instead, all new SDK updates are exclusively published through the methods referenced in implementation guide.

> [!NOTE]
> There are no breaking changes while upgrading the SDK from 8.x to 9.0.0.

## CocoaPods

There are no changes for support of CocoaPods. Your podfile should look like this:

```

# iOS: Podfile config to include our SDK
platform :ios, '12.0'
project 'FunBanner'
target 'FunBanner' do
  pod 'AppNexusSDK'
end
```

## Carthage

As of SDK v9.0.0, the framework is moved away from GitHub and to access binary only framework, use the URLs listed in the example Cartfile below.

Your cartfile should look like this:

```

# iOS: Carthage config to include our SDK
binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/AppNexusSDK.json"
binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/OMSDK_Microsoft.json"
```

## XCFramework

As of SDK v9.0.0, the framework is moved to the CDN URL listed below and you can use the following link to access the static framework.

```

- https://adsdkprod.azureedge.net/mobile/ios/releases/9.0.0/static/sdks.zip
```

## Swift Package Manager

You can either incorporate the latest release or main branch into your app or you can choose a specific release. Use the following link in your Xcode Package Dependencies:

```

# For the latest version of our SDK
  https://github.com/appnexus/mobile-sdk-ios-spm

```
