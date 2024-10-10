---
title: Resize the Banner Ad View to the Size of the Winning Creative on iOS
description: Resize the banner ad view on iOS to the size of the winning creative using methods for height and width retrieval.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Resize the banner ad view to the size of the winning creative on iOS

When you win a bid, you may want to resize the banner ad view to the size of the winning creative.

To retrieve the height and width of the winning creative, use the `loadedAdSize` method.

## `loadedAdSize` method

| Parameter | Description |
|:---|:---|
| `width` | The width of the creative for the banner ad view. |
| `height` | The height of the creative for the banner ad view. |

## Example

```
- (void)loadBannerAd
{ 
// Create the banner ad view and add it as a subview.
self.banner = [ANBannerAdView adViewWithFrame:rect placementId:@"1326299"];
self.banner.rootViewController = self;
   
// Fill in the ad sizes array.
CGSize size1 = CGSizeMake(300,  50);
CGSize size2 = CGSizeMake(300, 250);
NSArray *sizes = @[[NSValue valueWithCGSize:size1], [NSValue valueWithCGSize:size2]];
   
// Pass the ad sizes array to the banner ad view.
[self.banner setAdSizes:sizes];
   
[self.view addSubview:self.banner];
   
// Load an ad!
[self.banner loadAd];
}
  
#pragma mark - ANBannerAdViewDelegate
  
-(void)adDidReceiveAd:(id)ad{
    // Once the ad is loaded successfully, use the following to retrieve the ad sizes.
    NSLog(@"BannerAd's width %.2f ",self.banner.loadedAdSize.width )
    NSLog(@"BannerAd's height %.2f ",self.banner.loadedAdSize.height )
    }
```
