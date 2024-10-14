---
title: Click-Through URL on Android
description: In this article, learn what click-through refers to and the methods used to implement it on Android with examples.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Click-through URL on Android

The term click-through refers to the capability of our Mobile SDK to handle what happens when the user clicks on an ad. This document describes how click-through works and provides examples on ways to implement this feature.

## Overview

Xandr's Mobile SDK allows you to determine how the value of the `click_url` string in the bid response will be handled when the user clicks on an ad.

There are three possibilities:

- Open the click-through URL in the SDK browser.
- Open the click-through URL in the external device browser.
- Return the URL to the calling environment without opening any browser.

Cases that open a browser will notify the caller via `onAdClicked`.

In the case of a native ad request:

- Two URLs are returned: `click_url` and `click_url_fallback`.
  
  It is assumed that the caller will handle click-through URL(s) appropriately by displaying their contents to the user. The `click_url_fallback`, if defined, is used only if `click_url` cannot be resolved, for whatever reason, by the browser display system.

- The listener/delegate callback method is: `onAdWasClicked(clickUrl, fallbackURL).`

## Mobile SDK structure

- For Banner, Interstitial and Video: `AdListener` defines the method `onAdClicked(adView, clickUrl)`.
- For Native: `AdListener` defines the method `onAdWasClicked(clickUrl, fallbackURL)`.

## Examples

If you do not want to fetch ClickURL, you still need to implement a method `onAdClicked` that returns `clickURL`, but it can be left empty.

If you do want to fetch ClickURL, you can use the following code example to get started:

```
// Enable RETURN_URL API
adObject.setClickThroughAction(ANClickThroughAction.RETURN_URL);
```

Then add `onAdClicked` to get `clickURL`.

```
// Android: Java to handle ClickURL in ad response
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
 
public class PresentAdClickURL extends Activity {
 
    Context context;
    BannerAdView bav;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        context = this;
 
        // Create the AdView and set its placement ID.  Tweak a few other settings.
        bav = new BannerAdView(this);
        bav.setPlacementID("1326299");
        bav.setAdSize(300, 50);
        bav.setAdListener(adListener);
        // Enable RETURN_URL API
        bav.setClickThroughAction(ANClickThroughAction.RETURN_URL);
 
        //If auto-refresh is enabled
        bav.loadAd();
    }
 
 
 
 
    final AdListener adListener = new AdListener() {
        @Override
        public void onAdRequestFailed(AdView adView, ResultCode errorCode) {
        }
 
        @Override
        public void onAdLoaded(AdView adView) {
        }
 
        @Override
        public void onAdLoaded(NativeAdResponse response) { }
 
        @Override
        public void onAdExpanded(AdView adView) {
        }
 
        @Override
        public void onAdCollapsed(AdView adView) {
        }
 
        @Override
        public void onAdClicked(AdView adView) {
        }
 
        @Override
        public void onAdClicked(AdView adView, String clickUrl) {
        // the caller can handle it appropriately, displaying its content to the user.
        }
    };
 
 
    @Override
    protected void onDestroy() {
        super.onDestroy();
       }
} 
```
