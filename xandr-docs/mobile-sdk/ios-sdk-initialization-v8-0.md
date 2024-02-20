---
title: iOS SDK Initialization v8.0
description: In this article, learn about iOS SDK initialization v8.0, API signatures, and examples for better understanding.
ms.custom: ios-sdk
ms.date : 10/28/2023
---

# iOS SDK initialization v8.0

Publishers with iOS SDK v8.0, are required to initialize Mobile SDK before making an ad request. When using Mobile SDK for iOS SDK v8, the init() method must be called prior to any other SDK operations. Without this initialization no Ad request will go through and the SDK would throw an exception.

## API signature

The API signature for initializing the SDK is exposed using Xandr Ad. For example:

```
/**
 * Initialize Xandr Ads SDK
 * @param memberId for initializing the Xandr SDK
 * @param preCacheRequestObjects provides flexibility to pre-cache content, such as fetch userAgent, fetch IDFA and activate OMID. Pre-caching will make future ad requests faster.
 * @param completionHandler The completion handler to call when the init request is complete
 * */
- (void)initWithMemberID:(NSInteger) memberId
        preCacheRequestObjects:(BOOL)preCacheRequestObjects
        completionHandler: (XandrAdInitCompletion _Nullable)completionHandler;
```

## Examples

### Objective-C

```
@implementation AppDelegate
 
 
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
     
    // ideally initialize Xandr SDK inside AppDelegate before calling any other SDK methods
    [[XandrAd sharedInstance] initWithMemberID:1234 preCacheRequestObjects:YES completionHandler:^(BOOL success) {
            if(success){
                NSLog(@"XandrAd init Complete");
            }
    }];
    return YES;
}
```

### Swift

```
class AppDelegate: UIResponder, UIApplicationDelegate {
 
    var window: UIWindow?
 
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
 
        // ideally initialize Xandr SDK inside AppDelegate before calling any other SDK methods
        XandrAd.sharedInstance().initWithMemberID(1234, preCacheRequestObjects: true) { initComplete in
            if(initComplete){
                print("XandrAd init Complete")
            }
        }
        return true
    }
}
```
