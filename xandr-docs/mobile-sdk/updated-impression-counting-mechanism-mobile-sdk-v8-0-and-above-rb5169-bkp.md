---
title: Impression Counting Mechanism - Mobile SDK v8.0 and above
description: Learn the updated impression counting mechanism for the Mobile SDK and the change is included in Xandr’s Mobile SDK version 8.0 and above.
ms.custom: android-sdk, ios-sdk
ms.date: 10/28/2023
---

# Impression counting mechanism - Mobile SDK v8.0 and above

As the advertising industry recognizes the need to move away from “begin to render” to visibility-based impressions, we have updated our mobile SDK in-app impression counting to account for ad container visibility.The move to counting based on ad container visibility strengthens the definition of an impression equating to an ad seen by the user on their device. This change is included in Xandr’s Mobile SDK v8.0 and above.

## Counting methods in mobile apps

With SDK v8.0, there are two counting methods that can be applied for impression counting in mobile apps:

- **Begin-to-render:** The impression is counted when an ad is fully downloaded and loaded on to the view, irrespective of the user’s screen.

- **Viewable Impression:** The impression is counted when one or more pixels of the ad's creative is visible on a device’s screen.

## Viewable impression tracking mechanism

The move to counting based on ad container visibility strengthens the definition of an impression equating to an ad seen by the user on their device. Viewable impression counting however, is not standard across the industry and may create discrepancies with third party impression metrics. Based on the transaction types below, Xandr takes a hybrid approach to reduce discrepancies with partners as the industry moves to viewable impression tracking mechanism, for mobile in app inventory.

## Impression counting using mobile SDK v8.0

The table is summarized as follows:

| Transaction Type | Impression Type | Counting Method |
|--|--|--|
| Direct-Sold Insertion Orders | Kept | Xandr will count an impression when one pixel of the ad creative is visible on a device’s screen (referred to as "Viewable Impression" counting). |
| Xandr Marketplace Transactions | Resold | Xandr will use “Viewable Impression” counting for DSP partners that support it. For all other exchange demand, impression counting will remain unchanged and will continue to follow the “begin to render” methodology, where the impression will be counted when an ad is fully downloaded and loaded on to the view, irrespective of the user’s screen. |

## Impression Tracking Mechanisms

<!--Following sections explain about various impression counting methodologies:

### Counting Methodology: Mobile SDK version 7.22.0 and older

The Mobile SDK v7.0 continues to use the old impression counting mechanism for various Ad formats. For more information, see [Impression Counting Methods](impression-counting-methods.md).

### Counting Methodology: Mobile SDK version v8.0 and above -->

| AdUnits      | Impression Type      | Enablement by Impression Type                                                                  |
|--------------|----------------------|------------------------------------------------------------------------------------------------|
| Banner       | Viewable Impression  | Default for Impression type = Kept Default for Impression type = Resold (limited DSP partners) |
| Banner       | Begin to Render      | Default for Impression Type = Resold                                                           |
| Native       | Viewable Impression  | Default for Impression type = Kept Default for Impression type = Resold (limited DSP partners) |
| Native       | Begin to Render      | Default for Impression Type = Resold                                                           |
| Interstitial | Count on Render      | Default                                                                                        |
| Video        | Count on Video Start | Default                                                                                        |

## Viewability and impression counting

Viewability and impression counting are two different entities. Impression counting measures if an ad is served whereas viewability measures a whole lot of analytics like how long the ad was viewed by the user, what actions the user took, etc. to give better picture for the advertiser to serve better.
The definition of impression counting definition has evolved over the years. Initially an impression was counted when it was rendered on the page or it was downloaded to the user page. However, it was not necessary that the ad was viewed though it was downloaded. So even if the ad was downloaded in the background the impression count was considered.  
This method of impression counting becomes irrelevant as advertisers want accurate counts to understand how many ads are actually served the user which means how many ads are actually downloaded as well as viewed by the user. This is what viewable impression counts. Viewable impression counting applies for all managed demand and for certain bidders like DV 360 who count only viewable impressions.  
The logic applies only for mobile app impressions and not for mobile web or web pages as these still count when the ad is rendered or downloaded to the page.
