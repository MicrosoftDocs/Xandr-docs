---
title: Resize Ads to Fit Screen or Banner Ad View on iOS
description: Learn how to expand ad creative to fit banner ad view and device screen width with instructions provided in this article.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Resize ads to fit screen or banner ad view on iOS

Depending on where advertising fits into your application, you might want to expand the ad creative to fill the banner ad view in which it's displayed, or to fit the device's screen width.

## Resize ad to fit banner ad view


### Properties

| Property | Description |
|:---|:---|
| `shouldResizeAdToFitContainer` | Determines whether the creative should resize to fill the banner ad view in which it's displayed. This feature ensures ad creatives that are smaller than the view size to 'stretch' to the current size. This may cause image quality degradation for the benefit of having an ad occupy the entire ad view. Defaults to `NO`. |

### Example

```
// Create the banner ad view and add it as a subview
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"1326299" adSize:size];
banner.rootViewController = self;
// Ad should resize to fit the container
banner.shouldResizeAdToFitContainer = YES;
[self.view addSubview:banner];
// Load an ad!
[banner loadAd];
```

## Constrain to container's view

By default `ANBannerAdView` is set to constrain to the size of the creative that is returned. But for some custom sizes you might want the `ANBannerAdView` to be constrained to its superview.

By adding the custom sizes to `sizesThatShouldConstrainToSuperview` array you can instruct the SDK to set the right constraints for you.

> [!NOTE]
> `sizesThatShouldConstrainToSuperview` is a global setting and will be applied to all of the Banner Ad Views in your app.

### Properties

| Property | Description |
|:---|:---|
| `sizesThatShouldConstrainToSuperview` | Special ad sizes for which the `ANBannerAdView` should be constrained to its super view. |

### Example

```
NSArray *customSizes = @[[NSValue valueWithCGSize:CGSizeMake(3, 3)],[NSValue valueWithCGSize:CGSizeMake(4, 4)]];// Special ad sizes for which the ANBannerAdView should be constrained to its super view.
ANSDKSettings.sharedInstance.sizesThatShouldConstrainToSuperview  = customSizes;
 
 
// Create the banner ad view and add it as a subview
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:adID adSize:CGSizeMake(3, 3)];
banner.rootViewController = self;
  
[self.view addSubview:banner];
  
// Load an ad!
[banner loadAd];
```
