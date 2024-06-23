---
title: Migrating iOS SDK v8.X.Y to v9.X.Y
description: Learn how to integrate the latest Mobile SDKs for iOS using CocoaPods, Carthage, XCFramework, and Swift Package Manager.
ms.custom: ios-sdk
ms.date: 10/28/2023
---

# Migrating iOS SDK v8.X.Y to v9.X.Y

Starting with SDK v9.0, we will no longer release source code updates for the Android/iOS Mobile SDKs on GitHub. Instead, all new SDK updates will be exclusively published through the methods referenced in our implementation guide.

Refer the detailed integration instructions for first-time implementations in the [iOS SDK Integration Instructions](ios-sdk-integration-instructions.md).

> [!NOTE]
> There are no breaking changes while upgrading the SDK from 8.x to 9.0.

## CocoaPods

There are no changes to our support of CocoaPods. Your podfile should look like this:

```

# iOS: Podfile config to include our SDK
platform :ios, '12.0'
project 'FunBanner'
target 'FunBanner' do
  pod 'AppNexusSDK'
end
```

## Carthage

Your cartfile should look like this:

```

# iOS: Carthage config to include our SDK
binary "https://adsdkdevstand.azureedge.net/dev/mobile/mtest/adoreleasetest/9.0.0-alpha.9/carthage/AppNexusSDK.json"
binary "https://adsdkdevstand.azureedge.net/dev/mobile/mtest/adoreleasetest/9.0.0-alpha.9/carthage/OMSDK_Microsoft.json"
```

## XCFramework

- To access the frameworks from our CDN, use these links:

```

- https://adsdkdevstand.azureedge.net/dev/mobile/mtest/adoreleasetest/9.0.0-alpha.9/static/ANSDKS.zip
```

## Swift Package Manager

You can either incorporate the latest release or main branch into your app or you can choose a specific release. Please use the appropriate link below in your Package Dependencies:

```

# For the latest version of our SDK
  https://github.com/appnexus/mobile-sdk-ios-spm















The links below provide guidance on integrating inventory with Prebid Server Premium (PSP), adjusting settings and demand partner mappings, and leveraging platform analytics:

- [Set Up Prebid Server Premium](set-up-prebid-server-premium.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Prebid Server Premium Analytics](prebid-server-premium-analytics.md)
- [Prebid Server Premium Services (APIs)](../digital-platform-api/prebid-server-premium-services.md)

> [!IMPORTANT]
> At this time, not all clients have access to PSP. If you would like more information, please contact your Microsoft Advertising Representative.
