---
title: Show Banner Native on Android
description: This page covers concepts on Banner Native and changes in the procedure of handling banner and video ad objects via the Banner class.  
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Show banner native on Android

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

The term *Banner Native* refers to the capability of our Mobile SDK Banner class to return native demand. The BannerAdView object is multi-format, returning demand for banner ads and, if enabled via the APIs as described in the examples below, video and native ads. This means that you can instantiate a single Banner class object and pass it a single Member ID and Code (or Placement ID) and access demand across any or all of banner, video and native Media Type formats.

If you decide not to use the Banner Native capability you won't notice any significant changes in the manner in which your existing implementations function. There are minor changes to the standard MobileSDK headers. But other than minor, one-time changes to satisfy the compilation process, there should be no impact on any existing code that uses the Banner class.

The assumption of this document is that you're already familiar with both the Banner and Native classes. To use Banner Native there are a number of significant changes both structurally and procedurally that you must manage. The Banner class with Banner Native behaves like the traditional Native Request class. When the Banner class returns with a native ad object, like traditional Native Request, it returns a Native Response object. This Native Response object can then be used in the traditional manner to display and track the ad content of a native ad object.

## Process changes

As of MobileSDK Version 4.9 for Android, there is one breaking change in the procedure of handling banner and video ad objects via the Banner class. Before the introduction of Banner Native, it was possible to add the Banner class instance view to a view hierarchy, even before the class instance returned the ad object. This made it possible to finalize the display setup of the class even before the lifecycle of loading and fetching the ad object had completed. Although this convenient short-cut meant potentially ignoring the callback that indicates the ad has loaded, it is a common pattern with the MobileSDK.

If the Banner class is used to fetch native ads, the display step MUST wait until after the callback has fired.  This is because the callback provides the delivery point for the native ad object, if it is returned, and because it is the only place to distinguish between the return of a native ad object versus a banner or video ad object.

## Mobile SDK structure

The AdListener defines a method, `onAdLoaded `(NativeAdResponse response), which must be declared even if it is not used.

Please follow below steps to understand how the multi-format `BannerAdView` is used:

- Enable Native demand for your `BannerAdView` using `enableNativeRendering(boolean enabled)` and `setAllowNativeDemand(boolean enabled)` methods. For enabling
 Video demand, use `setAllowVideoDemand(boolean enabled)` method. By default these values are false, in which case your `BannerAdView` will deliver only traditional HTML banner ads. You must explicitly enable native and video in the app.

  ```
  /**
       * Sets whether or not Native Ads(AppNexus Media Type:12) should be Renderered or not.
       *
       * @param enabled whether to enable Native Assembly Renderer or not. default is false
       */
      public void enableNativeRendering(boolean enabled) {
          enableNativeRendering = enabled;
      }
   /**
       * Sets whether or not Native Ads(AppNexus Media Type:12) can serve on this Ad object.
       * This overrides the value set in console.
       *
       * @param enabled    whether to enable Native Ads or not. default is false
       */
      public void setAllowNativeDemand(boolean enabled) {
          Clog.d(Clog.publicFunctionsLogTag, Clog.getString(
                  R.string.set_allow_native, enabled));
          requestParameters.setBannerNativeEnabled(enabled);
      }
  /**
       * Sets whether or not Video Ads(AppNexus Media Type:4) can serve on this Ad object.
       * This overrides the value set in console.
       *
       * @param enabled whether to enable Video Ads or not. default is false
       */
      public void setAllowVideoDemand(boolean enabled) {
          Clog.d(Clog.publicFunctionsLogTag, Clog.getString(
                  R.string.set_allow_video, enabled));
          requestParameters.setBannerVideoEnabled(enabled);
      }
  ```

- Whereas `loadAd` may be called as soon as possible, the banner (or video) ad cannot be put into a subview until one of the overloaded onAdLoaded functions has been called. This is because we must first determine the Media Type of the returned Ad.

- A `NativeAdResponse` is returned as one of the overloaded `onAdLoaded` calls, which can be handled in the same way as if it were returned in the traditional way by `NativeAdRequest`. In this case, `BannerAdView` effectively plays the same role as `NativeAdRequest`. (See [Show Native Ads on Android ](show-native-ads-on-android.md) for more on NativeAdResponse.)

- By default, the mainImage and iconImage are not loaded. You can manually download these images via the URLs returned by the methods getImageUrl() and getIconUrl(), in the class `NativeAdReponse`.

## Examples

Usage of the multi-format BannerAdView class is simply a combination of the usage for banner and traditional native classes.

If you adopt this SDK but do not want to fetch native demand, you still need to implement an overloaded method onAdLoaded that returns NativeAdResponse, but it can be left empty.

If you want to fetch native or a combination of banner, video and/or native, you can use the following code example to get started:

> [!NOTE]
> As best practices :
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the BannerAdView that is expected to be destroyed.

  ``` 
  // Android: Java to handle a banner-native ad response
  package com.appnexus.opensdk;
   
  import android.content.Context;
  import android.os.Bundle;
  import android.os.Handler;
  import android.app.Activity;
  import android.widget.FrameLayout;
  import android.widget.ImageView;
  import android.widget.RelativeLayout;
  import android.widget.LinearLayout;
  import android.widget.TextView;
   
  import com.appnexus.opensdk.*;
  import com.appnexus.opensdk.R.*;
   
  public class PresentBannerNative extends Activity {
   
      FrameLayout adFrame;
      Context context;
      BannerAdView bav;
      NativeAdResponse nativeAdResponse;
   
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          context = this;
          adFrame = (FrameLayout) findViewById(android.R.id.content);
   
          // Create the AdView and set its placement ID.  Tweak a few other settings.
          bav = new BannerAdView(this);
          bav.setPlacementID("1326299");
          bav.setAdSize(300, 50);
          bav.setAdListener(adListener);
                  bav.setAllowNativeDemand(true);
   
          //If auto-refresh is enabled
          bav.loadAd();
      }
   
   
      final NativeAdEventListener nativeAdEventListener = new NativeAdEventListener() {
          @Override
          public void onAdWasClicked() {
          }
   
          @Override
          public void onAdWillLeaveApplication() {
          }
      };
   
      final AdListener adListener = new AdListener() {
          @Override
          public void onAdRequestFailed(AdView adView, ResultCode errorCode) {
          }
   
          @Override
          public void onAdLoaded(AdView adView) {
   
              if (nativeAdResponse != null) {
                  // It's your responsibility to keep a reference to the view
                  // and `NativeAdResponse` object if necessary.
                  // Once done with the native ad view, call the following method to
                  // unregister that view.
                  NativeAdSDK.unRegisterTracking(adFrame);
                  nativeAdResponse = null;
              }
              adFrame.removeAllViews();
              adFrame.addView(bav);
          }
   
          @Override
          public void onAdLoaded(NativeAdResponse response) {
              nativeAdResponse = response;
              adFrame.removeAllViews();
   
              // Title
              TextView title = new TextView(context);
              title.setText(nativeAdResponse.getTitle());
   
              // Main text
              TextView description = new TextView(context);
              description.setText(nativeAdResponse.getDescription());
   
              // Cover image url
              String imageUrl = nativeAdResponse.getImageUrl();
              // Icon image url
              String iconUrl = nativeAdResponse.getIconUrl();
   
              // Text that indicates a call to action -- for example, to install an app
              TextView callToAction = new TextView(context);
              callToAction.setText(nativeAdResponse.getCallToAction());
   
              // Create a container (a parent view that holds all the views for native ads)
              LinearLayout container = new LinearLayout(context);
              container.addView(title);
              container.addView(description);
              container.addView(imageView);
              container.addView(iconView);
              container.addView(callToAction);
   
              // Add the native ad container to the view hierarchy
              adFrame.addView(container);
   
              // Register native views for click and impression tracking.  The
              // `adEventListener` is the listener created above; it can be `null` if
              // you don't want to receive notifications about click events.
              // Impressions and clicks won't be counted if the view is not registered.
              NativeAdSDK.registerTracking(nativeAdResponse, adFrame, nativeAdEventListener);
          }
   
          @Override
          public void onAdExpanded(AdView adView) {
          }
   
          @Override
          public void onAdCollapsed(AdView adView) {
          }
   
          @Override
          public void onAdClicked(AdView adView) {
          }
      };
   
   
      @Override
      protected void onDestroy() {
                  if (bav != null) {
                  bav.activityOnDestroy();
          }
          super.onDestroy();
          if (nativeAdResponse != null) {
              // It's your responsibility to keep a reference to the view
              // and `NativeAdResponse` object if necessary.
              // Once done with the native ad view, call the following method to
              // unregister that view.
              NativeAdSDK.unRegisterTracking(adFrame);
              nativeAdResponse = null;
          }
      }
  }
  ```

## Related topics:

- [Get Facebook Demand for Native on Android](get-facebook-demand-for-native-on-android.md)
- [Native Assembly Renderer for Android](native-assembly-renderer-for-android.md)
