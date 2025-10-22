---
title: Build the Android SDK From Source
description: In this article, find instructions for including the source code of our Android SDK in your project and building it.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Build the Android SDK from source

This page has instructions for including the source code of our Android SDK in your project and building it.

To install using Maven or to download a JAR, see [Integrate the SDK](android-sdk-integration-instructions.md).

## Step 1. Clone the repo

Run this command in your terminal:

```
git clone https://github.com/appnexus/mobile-sdk-android.git    
```

The cloned directory will look something like:

```
├── examples
│   └── SimpleBanner   // Simple example app
├── mediation
│   ├── mediatedviews  // Mediation adaptors, one per network
│   └── mediating      // Support for other networks mediating our SDK
├── sdk                // SDK sources
      
```

> [!NOTE]
> The SDK and each of the mediation adaptors are standalone libraries.

## Step 2. Add the source to your project

Click **File** > **New** > **Import Module** (or your IDE's equivalent) and enter the location of the SDK sources you just cloned. Make sure the sources are actually copied into your project so you can edit the code.

## Step 3. Configure build settings

Include the SDK at the top of your `settings.gradle` file:

```
include ':app', ':sdk' 
```

Add a new line in the `dependencies` block of your app's `build.gradle` file:

```
dependencies {
    compile project(":sdk")
}      
```

At this point you should be able to build your app with the SDK included as a library.

## Related topics

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Xandr Mobile SDKs](xandr-mobile-sdks.md)
- [Show Banners](show-banners-on-android.md)
- [Show Interstitials](show-interstitials-on-android.md)
