---
title: Get Facebook Demand for Native on Android
description: In this article, learn how to retrieve native ad assets for display in Facebook's Audience Network SDK on Android devices.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Get Facebook demand for native on Android

This article describes the process for retrieving native ad assets to display in Facebook's Audience Network SDK in following steps:

## SDK installation

The Mobile SDK and Xandr-FAN-Demand Package will need to be installed. To know more about the details of the releases, see our [release page](android-sdk-release-notes.md). In the dependencies section of the `build.gradle` of your project add these two lines:

``` 
dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:[8,9)'
    implementation 'com.appnexus.opensdk.csr:appnexus-facebook-csr:[8,9)'
}
```

## Initialize Facebook's Audience Network SDK

Early in the lifecycle of your app, initialize `Audience Network` like so:

``` 
AudienceNetworkAds.buildInitSettings(this).withInitListener(new AudienceNetworkAds.InitListener() {
    @Override
    public void onInitialized(AudienceNetworkAds.InitResult initResult) {
        // do something, load ad or else
    }
}).initialize();
```

> [!NOTE]
> To ensure a successful implementation of a native ad with `Audience Network` your custom native view must include [MediaView](https://developers.facebook.com/docs/audience-network/setting-up/ad-setup/android/native#mediaview) for the main asset.

## Create a native banner ad layout

In the activity layout's `activity_main.xml` of your app, add a container for your native ad. This container should be of type `com.facebook.ads.NativeAdLayout`, which is a wrapper on top of a `FrameLayout`. This wrapper provides extra functionality that enables Mobile SDK to render a native `Ad Reporting Flow` on top of the ad.

``` 
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    ...
    <com.facebook.ads.NativeAdLayout
        android:id="@+id/native_banner_ad_container"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true" />
    ...
</RelativeLayout>
```

[Click here to view a sample code](https://developers.facebook.com/docs/audience-network/guides/ad-formats/native-banner/android#layout) provided by Facebook for setting up native banner ad custom layouts.

## Create a native ad request and load the ad

> [!NOTE]
> Hold a reference to the request until you receive a response.

Check the type of response returned from the `NativeAdRequest`. If the response type is `FBNativeBannerAdResponse`, cast the initial response to an `FBNativeBannerAdResponse` and call the `inflateAndRegisterFB` method. For other native ad types, call the `inflateAndRegisterNonFB`.

``` 
NativeAdRequest request = new NativeAdRequest(MainActivity.this, "17823252");
request.setListener(new NativeAdRequestListener() {
    @Override
    public void onAdLoaded(NativeAdResponse response) {
        Log.d("NativeBanner", "loaded");
        MainActivity.this.response = response;
        if (response instanceof FBNativeBannerAdResponse) {
            FBNativeBannerAdResponse fbResponse = (FBNativeBannerAdResponse) response;
            inflateAndRegisterFB(fbResponse);
        } else {
            inflateAndRegisterNonFB(response);
        }
    }
 
    @Override
    public void onAdFailed(ResultCode errorcode) {
        Log.d("NativeBanner", "failed");
    }
});
request.loadAd();
```

## Inflate and register the native ad

The process for creating the NativeAdRequest and loading the ad uses one of these methods, depending on the native ad object returned in the response:

- `inflateAndRegisterFB`
- `inflateAndRegisterNonFB`

These methods are identical in function except for the registration process. If the object returned in the response is a `FBNativeBannerAdResponse` the response would call the `registerView` method to register the ad. If it was not a `FBNativeBannerAdResponse` object the response would then call `NativeAdSDK.registerTracking` to register the ad.

### `inflateAndRegisterFB` example

Retrieve and display the call to action text for the call to action button:

``` 
Button nativeAdCallToAction = adView.findViewById(R.id.native_ad_call_to_action);
nativeAdCallToAction.setText(fbResponse.getCallToAction());
```

Once the button text has been retrieved, register the native ad so the click action and impression tracking can be activated:

``` 
fbResponse.registerView(adView, nativeAdIconView, clickableViews, new NativeAdEventListener() {
    @Override
    public void onAdWasClicked() {
     
    }
 
    @Override
    public void onAdWillLeaveApplication() {
 
    }
 
    @Override
    public void onAdWasClicked(String clickUrl, String fallbackURL) {
 
    }
});
```

### `inflateAndRegisterNonFB` example

Retrieve the call to action text to display on the call to action button and display that text:

``` 
Button nativeAdCallToAction = adView.findViewById(R.id.native_ad_call_to_action);
nativeAdCallToAction.setText(response.getCallToAction());
```

Once the button text has been retrieved register the native ad so the click action and impression tracking can be activated:

```
NativeAdSDK.registerTracking(response, adView, clickableViews, new NativeAdEventListener() {
    @Override
    public void onAdWasClicked() {
         
    }
 
    @Override
    public void onAdWillLeaveApplication() {
 
    }
 
    @Override
    public void onAdWasClicked(String clickUrl, String fallbackURL) {
 
    }
});
```

### Access the original native object

Publishers can access the original native object through the `getNativeElements` method:

``` 
nativeAdCallToAction.setText(fbResponse.getCallToAction());
nativeAdSocialContext.setText(((NativeAdBase) 
response.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)).getAdSocialContext());
```

## Unregister the views

When the app is finished displaying the ads you must unregister the views.

``` 
if (this.response != null) {
    if (this.response instanceof FBNativeBannerAdResponse) {
        FBNativeBannerAdResponse fbresponse = (FBNativeBannerAdResponse) response;
        fbresponse.unregisterView();
        this.response = null;
    } else {
        NativeAdSDK.unRegisterTracking(nativeAdView);
    }
}
```

## Example app

Xandr has provided an [example app](https://github.com/appnexus/AppExamples/tree/master/Android/Java/FacebookDemand) on our Github repo.

## Related topics

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Show Banner Native on Android](show-banner-native-on-android.md)
- [Show Native Ads on Android](show-native-ads-on-android.md)
