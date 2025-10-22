---
title: Android Custom Adaptors
description: In this article, learn what custom adaptors are, how to create your own custom adaptors, and the callbacks to be implemented by the custom adaptors.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Android custom adaptors

Custom adaptors allow our SDK to call out to another SDK installed on the same device, usually for mediation. This document describes the code you must write to create your own custom adaptors.

> [!NOTE]
> The interfaces described here are exactly what we used to implement our own mediation adaptors.

## Banners

In order to show mediated banner ads, you must implement the `MediatedBannerAdView` interface, which consists of two methods: `requestAd` and `destroy`.

You are also responsible for implementing the callbacks that translate the mediated SDK’s events into events that are understood by our mobile SDK. For details, see the example implementation below:

```
 /**
 * The custom adaptor for banners must implement our mobile SDK
 * interface `MediatedBannerAdView`. In this example, the class also
 * implements the `AdListener` interface from the mediated SDK,
 * in order to handle the events from the mediated SDK.
 */
public class TestMediatedBanner implements MediatedBannerAdView {
    MediatedBannerAdViewController controller = null;
    AdView bannerAd;
    
    @Override
    public View requestAd(MediatedBannerAdViewController mediatedBannerAdViewController,
                          Activity activity, String parameter,
                          String adId, int width, int height,
                          TargetingParameters targetingParameters) {

        // Here is where you are responsible for (1) instantiating the mediated SDK,
        // (2) building a request object using the elements of `targetingParameters`.
        // Note that you are responsible for ensuring that the targeting
        // parameters can be understood by the mediated SDK.  We also assume that (3)
        // you create and return a view in the mediated SDK that you can use to make
        // the ad request.

        // Next, we tell the mediated SDK's ad view to request a banner ad from their ad
        // server.  If it works, we call the `onAdLoaded` method on our controller to
        // notify it that we've successfully loaded an ad.

        controller = mediatedBannerAdViewController;

        bannerAd = new AdView(activity, new AdSize(width, height));
        bannerAd.setAdId(adId);

        // You are responsible for creating a mapping between the events
        // emitted by the mediated SDK and those understood by our mobile SDK.
        bannerAd.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded(AdView adView) {
                controller.onAdLoaded();
            }

            @Override
            public void onAdRequestFailed(AdView adView) {
                // If available, map the mediated SDK's failure code
                // to the appropriate Xandr `ResultCode`.  In this example
                // we just pass in ResultCode.UNABLE_TO_FILL.
                controller.onAdFailed(ResultCode.UNABLE_TO_FILL);
            }

            @Override
            public void onAdExpanded(AdView adView) {
                controller.onAdExpanded();
            }

            @Override
            public void onAdCollapsed(AdView adView) {
                controller.onAdCollapsed();
            }

            @Override
            public void onAdClicked(AdView adView) {
                controller.onAdClicked();
            }
        });

        // create a `request` for the mediated SDK from targeting parameters.

        bannerAd.loadAd(request);
        return bannerAd;
    }

    @Override
    public void destroy() {
        // Called when the mediated SDK's view is no longer being shown.
        bannerAd.destroy();
    }
}
```

Xandr's mobile SDK calls the `requestAd` method when the third-party SDK should begin requesting an ad. `requestAd` returns a view that holds the ad from the third-party SDK; it takes the following parameters:

- `mBC`: A `MediatedBannerAdViewController` through which the adaptor must send events to our SDK.
- `activity`: `Activity` context through which the adaptor can instantiate its view object.
- `parameter`: An optional opaque string passed from the server, this can be used to define SDK-specific parameters such as additional targeting information. The encoding of the contents of this string are entirely up to the implementation of the third-party SDK adaptor.
- `uid`: The network ID for this ad call. This ID is opaque to our mobile SDK; the ID’s contents and their encoding are up to the implementation of the third-party SDK. In other words, you must populate this with a value understood by the third-party SDK’s ad server.
- `width`: The width of the advertisement in pixels as defined in the `MediatedBannerAdView` object that initiated this call.
- `height`: The height of the advertisement in pixels as defined in the `MediatedBannerAdView` object that initiated this call.
- `targetingParameters` A `TargetingParameters` object containing targeting information that was passed to our mobile SDK such as age, gender, and location.

## Interstitials

Interstitials need to be prefetched by the mediated SDK before being shown to the user. As with banners, you must implement `requestAd`. You must also implement `isReady` to let the user know if an ad is available, and `show`, which displays an ad.

You are responsible for implementing the callbacks that translate the mediated SDK’s events into events that are understood by our SDK. For details, see the example implementation below:

```
/**
 * The custom adaptor for interstitials must implement our mobile SDK
 * interface `MediatedInterstitialAdView`. In this example, the class also
 * implements the `AdListener` interface from the mediated SDK,
 * in order to handle the events from the mediated SDK.
 */
public class TestMediatedInterstitial implements MediatedInterstitialAdView {
    MediatedInterstitialAdViewController controller = null;
    InterstitialAd interstitialAd;
    
    @Override
    public void requestAd(MediatedInterstitialAdViewController     mediatedInterstitialAdViewController,
                          Activity activity, String parameter,
                          String adId, TargetingParameters targetingParameters) {
        // Here is where you would be responsible for (1) instantiating the mediated SDK,
        // (2) building a request object using the elements of `targetingParameters`.
        // Note that you are responsible for ensuring that the targeting
        // parameters can be understood by the mediated SDK.  We also assume that (3)
        // you create and return a view in the mediated SDK that you can use to make
        // the ad request.

        // Next, we tell the mediated SDK's ad view to request an interstitial ad from
        // their ad server.  If it works, we call the `onAdLoaded` method on our
        // controller to notify it that we've successfully loaded an ad.
        
        controller = mediatedInterstitialAdViewController;
       
        interstitialAd = new InterstitialAd(activity);
        interstitialAd.setAdId(adId);

        // You are responsible for creating a mapping between the events
        // emitted by the mediated SDK and those understood by our mobile SDK.
        interstitialAd.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded(AdView adView) {
                controller.onAdLoaded();
            }

            @Override
            public void onAdRequestFailed(AdView adView) {
                // If available, map the mediated SDK's failure code
                // to ours.  In this example we just pass in
                // ResultCode.UNABLE_TO_FILL.
                controller.onAdFailed(ResultCode.UNABLE_TO_FILL);
            }

            @Override
            public void onAdExpanded(AdView adView) {
                controller.onAdExpanded();
            }

            @Override
            public void onAdCollapsed(AdView adView) {
                controller.onAdCollapsed();
            }

            @Override
            public void onAdClicked(AdView adView) {
                controller.onAdClicked();
            }
        });

        // create a `request` for the mediated SDK from targeting parameters.

        interstitialAd.loadAd(request);
    }
    // Call when the mediated SDK should display the interstitial ad
    @Override
    public void show() {
        interstitialAd.displayAd();
    }

    // Returns whether or not the mediated SDK has an interstitial ad
    // fetched and ready to to be shown.
    @Override
    public boolean isReady() {
        return interstitialAd.isAdReady();
    }

    @Override
    public void destroy() {
        // Called when the mediated SDK's view is no longer being shown.
        interstitialAd.destroy();
    }
}
```

The adaptor must call `requestAd` when the third-party SDK should begin requesting an ad. It takes the following arguments:

- `mIC`: A `MediatedInterstitialAdViewController` through which the adaptor must send events to our SDK.
- `activity`: `Activity` context through which the adaptor can instantiate its view object.
- `parameter`: An optional opaque string passed from the server, this can be used to define SDK-specific parameters such as additional targeting information. The encoding of the contents of this string are entirely up to the implementation of the third-party SDK adaptor.
- `uid`: The network ID for this ad call. This ID is opaque to our SDK; the ID’s contents and their encoding are up to the implementation of the third-party SDK. In other words, the parameter must be populated with values understood by the third-party SDK’s ad server.
- `targetingParameters`: A `TargetingParameters` object containing targeting information that was passed to our mobile SDK such as age, gender, and location.

In addition to `requestAd`, the `MediatedInterstitialAdView` interface requires you to implement these methods:

- `isReady`: Our SDK calls this method to check if the interstitial view is ready when the user calls `InterstitialAdView.isReady`.
- `show`: Our SDK calls this method to show the interstitial view when the user has called `InterstitialAdView.show`.

## Required callbacks

The callbacks listed below must be implemented by your custom adaptor. Note that these callbacks are required whether the ad in question is a banner or interstitial. You can see examples of their use in the code samples above.

- `onAdLoaded`: Called to indicate that the mediated SDK’s request completed and returned a banner successfully.
- `onAdFailed`: Called to indicate that the mediated SDK’s request failed to return a valid ad.

## Optional callbacks

The callbacks listed below should be implemented in custom adaptors for both banners and interstitials.

- `onAdClicked`: The ad was clicked.
- `onAdExpanded`: The ad is presenting a modal view.
- `onAdCollapsed`: The ad is dismissing the modal view.

## Related topics

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Mediate with Android SDK Instructions](mediate-with-android-sdk-instructions.md)
