---
title: Initialize SDK Settings in iOS
description: In this article, learn how to initialize SDK settings on iOS devices using a method and an example for better understanding.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Initialize SDK settings in iOS

SDKSettings in Xandr Mobile SDK contains the method `optionalSDKInitialization()`, which allows you to pre-configure common settings such as checking the presence of the User Agent during initialization, preparing a WebView etc. The completion block of this method returns `true` if SDK initialization completes successfully and `false` if it fails.

## Method
The following methods are supported in this feature:

### optionalSDKInitialization

Checks the availability of User Agent and returns a Boolean value accordingly during SDK initialization.

``` 
- (void) optionalSDKInitialization:(sdkInitCompletion _Nullable)success
```

## Example

``` 
[[ANSDKSettings sharedInstance] optionalSDKInitialization:^(BOOL isSDKInitialized) {
 if(isSDKInitialized){
      NSLog(@"SDK Initialized");
    }else{
      NSLog(@"SDK did not initialize");
    }
  }];
```
