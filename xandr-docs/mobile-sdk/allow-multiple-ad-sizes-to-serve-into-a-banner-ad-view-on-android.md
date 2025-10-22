---
title: Allow Multiple Ad Sizes to Serve into a Banner Ad View on Android
description: In this article, learn how to allow multiple ad sizes to serve into a banner ad view on Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Allow multiple ad sizes to serve into a banner ad view on Android

Banner ads with a fixed size may not get as much demand as you'd like. To open up a banner ad view to more demand, and hopefully more revenue, you can allow more than one ad size to serve.

Follow the instructions below to allow multiple ad sizes to serve into your banner ad views.

To allow multiple ad sizes to serve into a banner ad view on Android, use the following methods on `BannerAdView`:

- `setAdSizes(ArrayList<AdSize> adSizes)`: Takes a list of the platform ad sizes that may be inserted into the current banner ad view.
- `getAdSizes()`: Returns the sizes allowed to be displayed in the current banner ad view.

## Example

```
// Create the AdView and set its placement ID.
BannerAdView bav = new BannerAdView(this);
bav.setPlacementID("1326299");

// Build up ad sizes array.
ArrayList<AdSize> sizes = new ArrayList<AdSize>();
sizes.add(new AdSize(300,  50));
sizes.add(new AdSize(300, 250));

// Pass ad sizes array to banner ad view.
bav.setAdSizes(sizes);

// Add AdView to our layout.
FrameLayout layout = (FrameLayout)findViewById(android.R.id.content);
layout.addView(bav);

// Load an ad
bav.loadAd();
```
