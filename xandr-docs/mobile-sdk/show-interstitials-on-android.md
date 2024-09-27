---
title: Show Interstitials on Android
description: This page gives an overview on instructions and code samples for showing interstitial ads on Android.
ms.custom: android-sdk
ms.date: 09/27/2024
---

# Show interstitials on Android

This page has instructions and code samples for showing interstitial ads on Android.

> [!NOTE]
> Interstitial Ad Views and Placement/Creative Media Types
>
> Most of the time, the placements used in your SDK interstitial ad views should be configured to allow the *Banner* media type. This will give you the maximum amount of demand. You may still choose the *interstitial* media type depending on the type of ad you want to show, e.g.:
>
> - [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
> - [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)
> - [Ad Ops - Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)
>
> Likewise, creatives that serve into interstitial views in the SDK should usually be created with the Banner media type (keeping in mind the exceptions listed above).

## Overview

Showing interstitial ads is a little more work. In addition to setting up an `InterstitialAdView` with your placement ID, you must implement the `AdListener` interface, which includes methods that tell you when an interstitial ad has successfully finished loading, or when the request has failed.

Interstitial Ad Unit supports VAST Video creatives as of version 9.1.0. The code example below is suitable to request and render a video creative if the implemented placement is enabled for video demand.

Furthermore, actually showing interstitial ads to users is a two-step process:

1. Call `InterstitialAdView.loadAd()` to fetch the ad contents from our server and cache them locally. Note that any ad content is rendered in a WebView at the time it is fetched from the ad server and cached. This means that any third-party tracking pixels that are part of the ad content will be fired at the time of the call to `loadAd()`, not when the call to `show()` is made at a later time.
1. When you're ready to show the interstitial ad to the user, call `show()`. This needs to happen within approximately 4 minutes of the call to `loadAd()` in order for the impression to be counted by Xandr. <!-- (For the exact timing in milliseconds, see the value of `InterstitialAdView.MAX_AGE` in the source code.) -->

> [!NOTE]
> The close button appears after ten seconds by default. You can set the delay using `InterstitialAdView.setCloseButtonDelay(int closeButtonDelay)`.

For more information, see the code sample below.

## Code sample

> [!NOTE]
> Beginning with version RC2.8, you can also use an inventory code and member ID to request an ad (placement ID is still supported). Currently this is only available from Java (not XML). Note that if both inventory code and placement ID are passed in, the inventory code will be passed to the server instead of the placement ID.

```
// Android: Java code that uses inventory code and member ID instead of placement ID (optional)
adview.setInventoryCodeAndMemberID(int memberID, String inventoryCode)
```

> [!NOTE]
> As best practices:
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the Interstitial that is expected to be destroyed.

```
// Android: Java code to show an interstitial ad
package com.example.simpleinterstitial;
import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;
import android.util.Log;
import com.appnexus.opensdk.*;
public class MainActivity extends Activity implements AdListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // Set up an ad view with our placement ID.
        InterstitialAdView iav = new InterstitialAdView(this);
        iav.setPlacementID("1326299");
        iav.setAdListener(this);
        // Fetch an ad from the server.  If this works, `onAdLoaded' will
        // be called, and we can show the ad.
        iav.loadAd();
    }
        @Override
        protected void onDestroy() {
        if (iav != null) {
                iav.activityOnDestroy();
        }
        super.onDestroy();
        }
    @Override
    public void onAdLoaded(AdView av) {
        Log.d("onAdLoaded", "The ad has loaded, now we can show it...");
        // Now that the ad has loaded, we can show it to the user.
        InterstitialAdView iav = (InterstitialAdView) av;
        iav.show();
    }
 
    @Override
        public void onAdLoaded(NativeAdResponse nativeAdResponse) {
        // JUST ignore it. This callback is for Native in Banner. 
        }
    @Override
    public void onAdRequestFailed(AdView av, ResultCode rc) {
        Log.d("onAdRequestFailed", "Not sure why the ad request failed; try again? Return code ==> " + rc);
    }
    @Override
    public void onAdClicked(AdView av) {
        Log.d("onAdClicked", "The user clicked your ad.  Congrats!");
    }
        @Override
        public void onAdClicked(AdView adView, String clickUrl) {
        // This will be getting called if you have set setClickThroughAction(ANClickThroughAction.RETURN_URL);
        // Handle the URL appropriately
        }
     @Override
    public void onAdCollapsed(AdView av) {
        // Do something here.
    }
    @Override
    public void onAdExpanded(AdView av) {
        // Do something here as well.
    }
}
```

## Using custom interstitial sizes

By default, if you don't specify an ad size, the SDK will fetch ads in any of the sizes below that are less than or equal to the size of the device's screen.

- 1x1 (always sent)
- The detected size of the screen (always sent)
- 300x250
- 320x480
- 900x500
- 1024x1024

If you want to show interstitial ads in sizes other than the defaults, use the `setAllowedSizes` method on the interstitial ad view as shown below. Note that the detected size of the screen will still be passed as the primary size. The sizes set using `setAllowedSizes` will be passed in as additional size on the interstitial ad view and will replace the defaults of 300x250, 320x480, 900x500, and 1024x1024.

```
// Android: Java code to show interstitial ads in sizes other than the defaults (optional)
InterstitialAdView iav = new InterstitialAdView(this);
iav.setPlacementID("1326299");
AdSize test_size1 = new AdSize(320,480);
AdSize test_size2 = new AdSize(768,1024);
ArrayList test_array_list = new ArrayList() {};
test_array_list.add(test_size1);
test_array_list.add(test_size2);
iav.setAllowedSizes(test_array_list);
```

## Auto-close an interstitial

If you want to auto-close an interstitial ad after a specific timeout period, do not call `show()` as described in the above sections. Instead call `showWithAutoDismissDelay(delayinseconds)`, where `delayinseconds` is the number of seconds the ad will be displayed before it closes.

``` 
// This will show an interstitial ad, wait for 10 seconds, then auto close it.
interstitialAdView.showWithAutoDismissDelay(10);
```
