# Allow Multiple Ad Sizes to Serve into a Banner Ad View on iOS

<div class="body">

Banner ads with a fixed size may not get as much demand as you'd like.
To open up a banner ad view to more demand, and hopefully more revenue,
you can allow more than one ad size to serve.

Follow the instructions below to allow multiple ad sizes to serve into
your banner ad views.

<div class="p">

To allow multiple ad sizes to serve into a banner ad view on iOS, use
the `setAdSizes`method:

``` pre
- (void)setAdSizes:(NSArray<NSValue *> *)adSizes
```

</div>

<div class="p">

As shown in the example below, the sizes array needs to be
an `NSArray` of `NSValue` objects wrapping `CGSize` structs, as
described in the <a
href="https://developer.apple.com/documentation/foundation/nsvalue/1624511-valuewithcgsize"
class="xref" target="_blank">NSValue documentation</a>:

``` pre
// Create the banner ad view and add it as a subview
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"1326299" adSize:size];

banner.rootViewController = self;
// Fill in the ad sizes array.
CGSize size1 = CGSizeMake(300,  50);
CGSize size2 = CGSizeMake(300, 250);
NSArray *sizes = @[[NSValue valueWithCGSize:size1], [NSValue valueWithCGSize:size2]];

// Pass the ad sizes array to the banner ad view.
[banner setAdSizes:sizes];
[self.view addSubview:banner];

// Load an ad!
[banner loadAd];
```

</div>

</div>

<div class="related-links">

<div class="familylinks">

<div class="parentlink">

**Parent topic:**
<a href="ios-sdk-code-samples.html" class="link">iOS SDK Code
Samples</a>

</div>

</div>

</div>
