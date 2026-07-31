---
title: Show Interstitials on Android
description: This page gives an overview on instructions and code samples for showing interstitial ads on Android.
ms.custom: android-sdk
ms.date: 07/17/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Show interstitials on Android

This page has instructions and code samples for showing interstitial ads on Android.

<!-- > [!NOTE]
> Interstitial Ad Views and Placement/Creative Media Types
>
> Most of the time, the placements used in your SDK interstitial ad views should be configured to allow the *Banner* media type. This will give you the maximum amount of demand. You may still choose the *interstitial* media type depending on the type of ad you want to show, e.g.:
>
> - [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
> - [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)
> - [Ad Ops - Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)
>
> Likewise, creatives that serve into interstitial views in the SDK should usually be created with the Banner media type (keeping in mind the exceptions listed above). -->

## Overview

Showing interstitial ads requires a bit more work than banners. In addition to setting up an `InterstitialAdView` with your placement ID, you must implement the `AdListener` interface, which includes methods that tell you when an interstitial ad has successfully finished loading, or when the request has failed.

When you're ready to show the interstitial ad to the user, call `show()`. This needs to happen within approximately 4 minutes of the call to `loadAd()` for the impression to be counted.

For more information, see the code sample below.

## Creative media types supported by the Interstitial ad unit

The `InterstitialAdView` can render creatives of the following media types, which map to the media types Monetize categorizes creatives by (see [Create a Placement — Media types and subtypes](../monetize/create-a-placement.md#media-types-and-subtypes)):

| Media Type | Description |
|:---|:---|
| Banner (`1`) | Static or animated display banner creatives. |
| Interstitial (`3`) | Full-screen creatives, including MRAID, static image, and HTML responsive formats. For creative setup, see:<br><ul><li>[Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)</li><li>[Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)</li><li>[Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)</li></ul> |
| Video (`4`) | VAST video creatives. See [Customize video player options on Android](customize-video-player-options-on-android.md) to customize the video player UI. |

> [!IMPORTANT]
> Each media type must be **explicitly enabled** in the placement's **Allowed Media** configuration in Monetize to be eligible to serve. Configure **Allowed Media** in the Monetize UI or via the API to include every media type you want the interstitial to receive — if no compatible media type is allowed on the placement, no ads will serve. For details, see [Create a Placement — Limit the type and size of creatives that can serve](../monetize/create-a-placement.md#step-3-limit-the-type-and-size-of-creatives-that-can-serve).

## Basic integration

> [!NOTE]
> As best practices:
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the Interstitial that is expected to be destroyed.

### [Kotlin](#tab/kotlin1)

```
// Android: Kotlin code to show an interstitial ad
package com.example.simpleinterstitial

import android.app.Activity
import android.os.Bundle
import android.util.Log
import com.appnexus.opensdk.*

class MainActivity : Activity(), AdListener {

    private var interstitial: InterstitialAdView? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        // Set up an ad view with our placement ID.
        interstitial = InterstitialAdView(this).apply {
            placementID = "1326299"
            setAdListener(this@MainActivity)
        }
        // Fetch an ad from the server. If this works, `onAdLoaded` will
        // be called, and we can show the ad.
        interstitial?.loadAd()
    }

    override fun onDestroy() {
        interstitial?.activityOnDestroy()
        super.onDestroy()
    }

    override fun onAdLoaded(av: AdView) {
        Log.d("onAdLoaded", "The ad has loaded, now we can show it...")
        (av as? InterstitialAdView)?.show()
    }

    override fun onAdLoaded(nativeAdResponse: NativeAdResponse) {
        // Ignore. This callback is for Native in Banner.
    }

    override fun onAdRequestFailed(av: AdView, rc: ResultCode) {
        Log.d("onAdRequestFailed", "The ad request failed: $rc")
    }

    override fun onAdClicked(av: AdView) {
        Log.d("onAdClicked", "The user clicked your ad.")
    }

    override fun onAdClicked(adView: AdView, clickUrl: String) {
        // Called only if setClickThroughAction(ANClickThroughAction.RETURN_URL) is set.
        // Handle the URL appropriately.
    }

    override fun onAdCollapsed(av: AdView) {
        // Do something here.
    }

    override fun onAdExpanded(av: AdView) {
        // Do something here as well.
    }

    override fun onAdImpression(av: AdView) {
        // Do something here as well.
    }
}
```

### [Java](#tab/java1)

```
// Android: Java code to show an interstitial ad
package com.example.simpleinterstitial;

import android.app.Activity;
import android.os.Bundle;
import android.util.Log;
import com.appnexus.opensdk.*;

public class MainActivity extends Activity implements AdListener {

    private InterstitialAdView interstitial;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // Set up an ad view with our placement ID.
        interstitial = new InterstitialAdView(this);
        interstitial.setPlacementID("1326299");
        interstitial.setAdListener(this);
        // Fetch an ad from the server. If this works, `onAdLoaded` will
        // be called, and we can show the ad.
        interstitial.loadAd();
    }

    @Override
    protected void onDestroy() {
        if (interstitial != null) {
            interstitial.activityOnDestroy();
        }
        super.onDestroy();
    }

    @Override
    public void onAdLoaded(AdView av) {
        Log.d("onAdLoaded", "The ad has loaded, now we can show it...");
        ((InterstitialAdView) av).show();
    }

    @Override
    public void onAdLoaded(NativeAdResponse nativeAdResponse) {
        // Ignore. This callback is for Native in Banner.
    }

    @Override
    public void onAdRequestFailed(AdView av, ResultCode rc) {
        Log.d("onAdRequestFailed", "The ad request failed: " + rc);
    }

    @Override
    public void onAdClicked(AdView av) {
        Log.d("onAdClicked", "The user clicked your ad.");
    }

    @Override
    public void onAdClicked(AdView adView, String clickUrl) {
        // Called only if setClickThroughAction(ANClickThroughAction.RETURN_URL) is set.
        // Handle the URL appropriately.
    }

    @Override
    public void onAdCollapsed(AdView av) {
        // Do something here.
    }

    @Override
    public void onAdExpanded(AdView av) {
        // Do something here as well.
    }

    @Override
    public void onAdImpression(AdView av) {
        // Do something here as well.
    }
}
```

---

## Advanced settings

The following sections describe optional configuration and callbacks you can use to customize how your interstitial ad requests and displays creatives.

### Initialize with member ID and inventory code

As an alternative to a placement ID, you can request an interstitial ad using a member ID and an inventory code by calling `setInventoryCodeAndMemberID(int memberID, String inventoryCode)` on the `InterstitialAdView`. If both an inventory code and a placement ID are set, the inventory code takes precedence.

#### [Kotlin](#tab/kotlin2)

```
// Android: Kotlin code to request an interstitial using member ID and inventory code
val interstitial = InterstitialAdView(this)
interstitial.setInventoryCodeAndMemberID(123, "your-inventory-code")
interstitial.setAdListener(this)
interstitial.loadAd()
```

#### [Java](#tab/java2)

```
// Android: Java code to request an interstitial using member ID and inventory code
InterstitialAdView interstitial = new InterstitialAdView(this);
interstitial.setInventoryCodeAndMemberID(123, "your-inventory-code");
interstitial.setAdListener(this);
interstitial.loadAd();
```

---

### Use custom interstitial sizes

By default, if you don't specify an ad size, the SDK will fetch ads in any of the sizes below that are less than or equal to the size of the device's screen.

- 1x1 (always sent)
- The detected size of the screen (always sent)
- 300x250
- 320x480
- 900x500
- 1024x1024

If you want to show interstitial ads in sizes other than the defaults, use the `setAllowedSizes` method on the interstitial ad view as shown below. Note that the detected size of the screen will still be passed as the primary size. The sizes set using `setAllowedSizes` will be passed in as additional size on the interstitial ad view and will replace the defaults of 300x250, 320x480, 900x500, and 1024x1024.

#### [Kotlin](#tab/kotlin3)

```
// Android: Kotlin code to show interstitial ads in sizes other than the defaults
val interstitial = InterstitialAdView(this)
interstitial.placementID = "1326299"
interstitial.setAllowedSizes(arrayListOf(AdSize(320, 480), AdSize(768, 1024)))
```

#### [Java](#tab/java3)

```
// Android: Java code to show interstitial ads in sizes other than the defaults
InterstitialAdView interstitial = new InterstitialAdView(this);
interstitial.setPlacementID("1326299");
ArrayList<AdSize> sizes = new ArrayList<>();
sizes.add(new AdSize(320, 480));
sizes.add(new AdSize(768, 1024));
interstitial.setAllowedSizes(sizes);
```

---

### Set the close button delay

For **Banner** and **Interstitial** creatives, the close button appears on the interstitial ad ten seconds after it is displayed by default. To change the delay, call `setCloseButtonDelay(int closeButtonDelay)` on the `InterstitialAdView`, passing the delay in **milliseconds**. The maximum is 10000 ms (10 seconds); values above that are clamped to 10 seconds. Passing `0` allows the close button to appear immediately. This setting has no effect on **Video** creatives, which use the video's own skip/close controls.

#### [Kotlin](#tab/kotlin4)

```
// Show the close button after 5 seconds instead of the default 10.
interstitial.setCloseButtonDelay(5000)
```

#### [Java](#tab/java4)

```
// Show the close button after 5 seconds instead of the default 10.
interstitial.setCloseButtonDelay(5000);
```

---

### Auto-close an interstitial

To auto-close a **Banner** or **Interstitial** creative after a specific timeout, do not call `show()`. Instead, call `showWithAutoDismissDelay(delayinseconds)`, where `delayinseconds` is the number of seconds the ad will be displayed before it closes. This setting has no effect on **Video** creatives, which run until they complete or are skipped.

#### [Kotlin](#tab/kotlin5)

```
// Show an interstitial ad, wait for 10 seconds, then auto-close it.
interstitial.showWithAutoDismissDelay(10)
```

#### [Java](#tab/java5)

```
// Show an interstitial ad, wait for 10 seconds, then auto-close it.
interstitial.showWithAutoDismissDelay(10);
```

---

### Customize video player options

To customize the video player UI — skip controls, mute, click-through text, and other playback controls — see [Customize video player options on Android](customize-video-player-options-on-android.md).

---

### Receive video completion callbacks

Register a `VideoEventListener` on your `InterstitialAdView` via `setVideoEventListener(...)` to be notified how a **Video** interstitial ad ended — `VideoCompletionState.COMPLETED`, `SKIPPED`, or `ERROR`. The callback fires only for RTB interstitial video ads (not mediated or CSR) and runs alongside the existing close callbacks.

#### [Kotlin](#tab/kotlin6)

```
// Android: Kotlin code to receive interstitial video completion callbacks
val interstitial = InterstitialAdView(this) // Create the interstitial ad view
interstitial.placementID = "1326299" // Set placement ID

interstitial.setVideoEventListener { adView, state -> // Register the video completion listener
    when (state) {
        VideoCompletionState.COMPLETED -> {
            // The video played to its natural end
        }
        VideoCompletionState.SKIPPED -> {
            // The user skipped the video before it ended
        }
        VideoCompletionState.ERROR -> {
            // Playback ended because of an error or timeout
        }
    }
}

interstitial.loadAd() // Load the ad
```

#### [Java](#tab/java6)

```
// Android: Java code to receive interstitial video completion callbacks
InterstitialAdView interstitial = new InterstitialAdView(this); // Create the interstitial ad view
interstitial.setPlacementID("1326299"); // Set placement ID

interstitial.setVideoEventListener(new VideoEventListener() { // Register the video completion listener
    @Override
    public void onAdCompleted(InterstitialAdView adView, VideoCompletionState state) {
        switch (state) {
            case COMPLETED:
                // The video played to its natural end
                break;
            case SKIPPED:
                // The user skipped the video before it ended
                break;
            case ERROR:
                // Playback ended because of an error or timeout
                break;
        }
    }
});

interstitial.loadAd(); // Load the ad
```

---
