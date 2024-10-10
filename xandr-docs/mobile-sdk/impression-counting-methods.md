---
title: Impression counting methods
description: In this article, learn about the various impression counting methods, types, AdUnits, and how to enable them.
ms.custom: android-sdk, ios-sdk
ms.date : 10/28/2023
ms.author: shsrinivasan
---

# Impression counting methods

The Mobile SDK uses different impression tracking mechanisms for various Ad formats. In this page, find the methods that apply to Mobile SDK versions 8.0 and above and to Mobile SDK versions 7.22 and below.

## Impression counting mechanism - Mobile SDK v8.0 and above

The advertising industry recognizes the need to move away from "begin to render" to visibility-based impressions. Accordingly, we have updated our mobile SDK in-app impression counting to account for ad container visibility. The move to counting based on ad container visibility strengthens the definition of an impression equating to an ad seen by the user on their device. This change is included in Xandr's Mobile SDK v8.0 and above.

### Counting methods in mobile apps

With SDK v8.0, there are two counting methods that can be applied for impression counting in mobile apps:

| Counting Method | Description |
|--|--|
| Begin-to-render | The impression is counted when an ad is fully downloaded and loaded on to the view, irrespective of the user’s screen. |
| 1px-in-view | The impression is counted when one or more pixels of the ad's creative is visible on a device’s screen. |

### 1px-in-view tracking mechanism

The move to counting based on ad container visibility strengthens the definition of an impression equating to an ad seen by the user on their device. 1px-in-view counting however, is not standard across the industry and may create discrepancies with third party impression metrics. Based on the transaction types below, Xandr takes a hybrid approach to reduce discrepancies with partners as the industry moves to 1px-in-view tracking mechanism, for mobile in app inventory.

Impression counting is summarized as follows:

| Transaction Type | Impression Type | Counting Method |
|--|--|--|
| Direct-Sold Insertion Orders | Kept | Xandr will count an impression when one pixel of the ad creative is visible on a device’s screen (referred to as "1px-in-view" counting). |
| Xandr Marketplace Transactions | Resold | Xandr will use “1px-in-view” counting for DSP partners that support it. For all other exchange demand, impression counting will remain unchanged and will continue to follow the “begin to render” methodology, where the impression will be counted when an ad is fully downloaded and loaded on to the view, irrespective of the user’s screen. |

### Impression tracking mechanisms

<!--Following sections explain about various impression counting methodologies:

### Counting Methodology: Mobile SDK version 7.22.0 and older

The Mobile SDK v7.22 continues to use the old impression counting mechanism for various Ad formats. For more information, see [Impression Counting Methods](impression-counting-methods.md).

### Counting Methodology: Mobile SDK version v8.0 and above -->

| AdUnits | Impression Type | Enablement by Impression Type |
|--|--|--|
| Banner | 1px-in-view | Default for Impression type = Kept Default for Impression type = Resold (limited DSP partners) |
| Banner | Begin to Render | Default for Impression Type = Resold |
| Native | 1px-in-view | Default for Impression type = Kept Default for Impression type = Resold (limited DSP partners) |
| Native | Begin to Render | Default for Impression Type = Resold |
| Interstitial | Count on Render | Default |
| Video | Count on Video Start | Default |

## Impression counting using Mobile SDK V7.22 and below

The Mobile SDK uses the following impression tracking mechanisms for versions 7.22 and earlier.

| Type | Counting Method | AdUnits | How to enable |
|:---|:---|:---|:---|
| Default | Impression trackers are fired when rendered (attached to window) | Banner Ads | NA |
| Default | Impression trackers are fired when rendered (attached to window) | Native Ads | NA |
| Feature | Impression trackers are fired when 1 pixel of the content is loaded | Banner and Native Ads | iOS: `ANSDKSettings.sharedInstance.countImpressionOn1PxRendering = YES` <br> Android: `SDKSettings.setCountImpressionOn1pxRendering(true)` |
| Feature | When lazy load is enabled, impression trackers are fired when content is loaded in webview  | Banner Ads | For more information on lazy load, visit [Lazy Load for iOS](lazy-load-for-ios.md) and [Android](lazy-load-for-android.md) page. |

## Viewability and impression counting

Viewability and impression counting are two different entities. Impression counting measures if an ad is served whereas viewability measures a whole lot of analytics like how long the ad was viewed by the user, what actions the user took, etc. to give better picture for the advertiser to serve better.

The definition of impression counting has evolved over the years. Initially an impression was counted when it was rendered on the page or it was downloaded to the user page. However, it was not necessary that the ad was viewed though it was downloaded. So even if the ad was downloaded in the background the impression count was considered.

This method of impression counting becomes irrelevant as advertisers want accurate counts to understand how many ads are actually served to the user which means how many ads are actually downloaded as well as viewed by the user. This is what 1px-in-view counts. 1px-in-view counting applies for all managed demand and for certain bidders like DV 360. The logic applies only for mobile app impressions and not for mobile web or web pages as these still count when the ad is rendered or downloaded to the page.

For more information about generic impression counting, see [Impression counting](../industry-reference/impression-counting.md).
