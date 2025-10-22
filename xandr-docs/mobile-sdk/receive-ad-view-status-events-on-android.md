---
title: Receive Ad View Status Events on Android
description: Learn how to receive ad view status events from the SDK to determine ad clicks and expanded state. Implement AdListener interface and attach it to the ad view.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Receive ad view status events on Android

This article has instructions to receive ad view status events from our SDK. You can use these events to determine when an ad has been clicked, whether it's in an expanded state, and more.

In order to receive status events during the life cycle of the ad view, you must implement the `AdListener` interface and attach it to the ad view. Its methods are:

- `void onAdClicked(AdView adView)`: Called when an ad is clicked.
- `void onAdClicked(adView, clickUrl)`: Called when an ad is clicked and allows you to determine how the value of the `click_url` string in the bid response will be handled.
- `void onAdCollapsed(AdView adView)`: Called when an ad is closed/unexpanded, for example if the user has stopped interacting with the ad.
- `void onAdExpanded(AdView adView)`: Called when an ad expands due to user interaction.
- `void onAdLoaded(AdView adView)`: Called when an ad has successfully been loaded from the server.
- `void onAdLoaded(NativeAdResponse nativeAdResponse)`: Called when an ad has successfully been loaded from the server. Used for Banner Native ads.
- `void onAdRequestFailed(AdView adView, ResultCode errorCode)`: Called when an ad request has failed.
- void on `AdImpression` (`AdView adView`): Called when an ad impression is observed during a banner or interstitial ad event.

The example below implements this interface:

```
// ... other imports ...
import com.appnexus.opensdk.*;
import com.appnexus.opensdk.utils.Clog;
// ... other code ...
// Set up a listener on this ad view that logs events.
AdListener adListener = new AdListener() {
    @Override
    public void onAdRequestFailed(AdView bav, ResultCode errorCode) {
        if (errorCode == null) {
       Clog.v("SIMPLEBANNER", "Call to loadAd failed");
        } else {
       Clog.v("SIMPLEBANNER", "Ad request failed: " + errorCode);
        }
    }
    @Override
    public void onAdLoaded(AdView bav) {
        Clog.v("SIMPLEBANNER", "The Ad Loaded!");
    }   
        @Override
    public void onAdImpression(AdView bav) {
        Clog.v("SIMPLEBANNER", "onAdImpression");
    }       
        @Override
    public void onAdLoaded(NativeAdResponse bav) {
        Clog.v("SIMPLEBANNER", "The Banner Native Ad Loaded!");
    }
    @Override
    public void onAdExpanded(AdView bav) {
        Clog.v("SIMPLEBANNER", "Ad expanded");
    }
    @Override
    public void onAdCollapsed(AdView bav) {
        Clog.v("SIMPLEBANNER", "Ad collapsed");
    }
    @Override
    public void onAdClicked(AdView bav) {
        Clog.v("SIMPLEBANNER", "Ad clicked; opening browser");
    }
 
    @Override
    public void onAdClicked(AdView adView, String clickUrl) {
        Clog.v("SIMPLEBANNER", "Ad clicked; app should handle url:" + clickUrl);
    }
};
bav.setAdListener(adListener);
```

We can see the results in LogCat:

```
*** Filter is changed to 'SIMPLEBANNER' ***
09-04 16:48:54.181 19005 19005 V SIMPLEBANNER: The Ad Loaded!
09-04 16:48:57.059 19005 19005 V SIMPLEBANNER: Ad clicked; opening browser    
```
