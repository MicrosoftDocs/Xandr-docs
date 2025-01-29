---
title: Vungle Demand for Android
description: Learn how to integrate and display interstitial video ads using Vungle on Android.
ms.custom: android-sdk
ms.date: 10/28/2023
---

# Vungle demand for Android

This page provides steps to integrate and display interstitial video ads using Vungle on Android. Follow these steps to configure and display interstitial video ads using Vungle on Android.

## Step 1: Install the SDK

To integrate Vungle demand, include the **AppNexus Mobile SDK** and the **ANVungleAdapter** in your project.  Include the following dependencies in the `build.gradle` file under the `dependencies` section:

```gradle
dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:[9,10)'
    implementation 'com.appnexus.opensdk.csr:appnexus-vungle-csr:[9,10)'
}
```

## Step 2: Initialize the Vungle SDK

Initialize the Vungle SDK early in your app's lifecycle to ensure it is ready to use. Replace `YOUR_APP_ID` with the app ID provided by Vungle.

### Example

#### [Java](#tab/Java1)

```java
VungleAds.init(this, "YOUR_APP_ID", new InitializationListener() {
    @Override
    public void onSuccess() {
        Log.d("vunglecsr", "Vungle SDK initialized successfully");
    }
    @Override
    public void onError(@NonNull VungleError vungleError) {
        Log.d("vunglecsr", "Initialization failed: " + vungleError.getErrorMessage());
    }
});

```

#### [Kotlin](#tab/kotlin1)

```kotlin


VungleAds.init(this, "YOUR_APP_ID", object : InitializationListener {
    override fun onSuccess() {
        Log.d("vunglecsrlog", "Vungle SDK init onSuccess()")
    }

    override fun onError(vungleError: VungleError) {
        Log.d("vunglecsrlog", "onError():" + vungleError.errorMessage)
    }
})

```
