---
Title : Show Banners on iOS
Description : This page has instructions and code samples for showing banner ads.
ms.custom : android-ios
---


# Show Banners on iOS



This page has instructions and code samples for showing banner ads.

To show banner ads, include our banner ad view header file. Then, create
a banner ad view object; you'll need to pass in a frame, placement ID,
and size. Add it as a subview of the current view, and you should start
seeing ads.

This simple example doesn't take advantage of all of the capabilities
provided by the SDK - for example, you can also pass in the user's age
and gender, as well as whether an ad click should open the device's
native browser.



<b>Note:</b> You can use member ID and
inventory code instead of a placement ID

The banner code sample below shows how to request ads using the
placement ID. Beginning with version RC2.8, you can initialize banners
using a combination of member ID and inventory code instead (placement
ID is still supported). Here are the methods:

``` pre
// iOS: ObjC code that uses inventory code and member ID instead of placement ID (optional)
-(instancetype)initWithFrame:(CGRect)frame memberId:(NSInteger)memberId inventoryCode:(NSString *)inventoryCode;
-(instancetype)initWithFrame:(CGRect)frame memberId:(NSInteger)memberId inventoryCode:(NSString *)inventoryCode adSize:(CGSize)size;
```



``` pre
// iOS: ObjC to show a banner ad
#import "ViewController.h"
#import "ANBannerAdView.h"
@interface ViewController ()
@end
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    // Get the screen size so we can center our 300x50 example ad
    CGRect screenRect = [[UIScreen mainScreen] bounds];
    CGFloat centerX = (screenRect.size.width / 2) - 150;
    CGFloat centerY = (screenRect.size.height / 2) - 25;
    
    // Set up some sizing variables we'll need when we create our ad view
    CGRect rect = CGRectMake(centerX, centerY, 300, 50);
    CGSize size = CGSizeMake(300, 50);
    
    // Create the banner ad view and add it as a subview
    ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"1326299" adSize:size];
    banner.rootViewController = self;
    banner.autoRefreshInterval = 60; // Set to 0 to disable auto-refresh
    [self.view addSubview:banner];
    
    // Load an ad!
    [banner loadAd];
}
@end
```

Swift developers will want to use the following code:

``` pre
// iOS: Swift to show a banner ad
// Import ANBannerAdView.h in the bridging header.
class MyViewController: UIViewController
{
    override func  viewDidLoad()
    {
        super.viewDidLoad()
 
        // Get the screen size so we can center our 300x50 example ad.
        let  screenRect  = UIScreen.main.bounds
        let  centerX     = (screenRect.size.width / 2) - 150
        let  centerY     = (screenRect.size.height / 2) - 25
 
        // Set up some sizing variables we'll need when we create our ad view.
        let  rect  = CGRect(x:centerX, y:centerY, width:300, height:50)
        let  size  = CGSize(width:300, height:50)
 
        // Create the banner ad view and add it as a subview.
        let  banner  = ANBannerAdView(frame:rect, placementId:"1326299", adSize:size)
        banner.rootViewController = self;
        banner.autoRefreshInterval = 60   // Set to 0 to disable auto-refresh.
        self.view.addSubview(banner)
 
        // Load an ad!
        banner.loadAd()
    }
}
```




