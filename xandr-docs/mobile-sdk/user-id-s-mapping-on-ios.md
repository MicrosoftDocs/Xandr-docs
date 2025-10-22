---
title: User ID(s) Mapping on iOS
description: Send Publisher First party ID and User ID(s) in iOS ad requests. Set User ID(s) once per app session for global use, not stored across sessions.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# User ID(s) mapping on iOS

> [!NOTE]
> This offering is currently in Alpha and is subject to changes or deprecation without notice.

## Overview

Xandr offers you the option of sending **Publisher First party ID** and **User ID(s)** from third party sources
in ad requests. They are global settings and it is sufficient to set the User ID(s) once per app session as these values would be used in all consecutive ad requests in the same session. Please note that, Xandr does not store these values across different app sessions.

## Mobile SDK structure

### Publisher first party ID

> > [!NOTE]
>**Deprecation Notice**:
>
>**`The` `externalUid`** property of **`ANBannerAdView`**, **`InterstitialAdView`**, **`ANNativeAdRequest`** and **`ANInstreamVideoAd`** class is now deprecated. You can use **`publisherUserId`** property described below in **`ANSDKSettings`** class instead. The deprecated methods will be removed in SDK v8.0.

You can set **Publisher First Party ID** using the `publisherUserId` property of  `ANSDKSettings` in Mobile SDK API. </br>

| Property        | Type     | Attribute | Description                                                                                |
|-----------------|----------|-----------|--------------------------------------------------------------------------------------------|
| `publisherUserId` | `NSString` | readwrite | Specifies a string that corresponds to the Publisher User ID for current application user. |

**IDFV as publisher first party ID**

Due to introduction of App Tracking Transparency (ATT) changes in iOS 14.5 and above, Xandr Mobile SDK offers the publishers to use **Identifier for Vendors (IDFV)** of the device in cases where there is no in-house **Publisher First Party ID** and **Identifier for Advertisers (IDFA)** is available. This feature facilitates the publishers to pass IDFV in the ad requests automatically whenever both of the Publisher First Party ID and IDFA is absent. This feature is enabled by default and if the publishers want to turn it off, they can use `disableIDFVUsage` property of  `ANSDKSettings` in Mobile SDK API.

| Property | Type | Attribute | Description |
|--|--|--|--|
| `disableIDFVUsage` | `BOOL` | readwrite | Specifies a boolean value which exclude the IDFV field in ad request. Default value of the property is set to **NO** and IDFV will be used in cases where both IDFV and Publisher First Party ID are not present for a given ad request. |

```
/**
An AppNexus disableIDFVUsage  is a boolean value which exclude the IDFV field in ad request. Default value of disableIDFVUsage is set to NO and IDFV will be used in cases where IDFV and Publisher First Party ID is not present.
*/
@property (nonatomic, readwrite) BOOL disableIDFVUsage;
```

**User ID**

> [!NOTE]
>
> **Deprecation Notice**:
>
>The property \`**ANSDKSettings.externalUserIdArray**\` and \`**ANExternalUserId**\` class are now deprecated and will be removed in SDK v8.0. You can use the equivalent property \`**ANSDKSettings.userIdArray**\`  and \`**ANUserId**\` class described below instead as a replacement.

Xandr supports User ID(s) from the below external sources:

- NetID
- Utiq
- ID5
- Criteo
- Unified ID 1.0 Trade Desk ID
- Hydron ID (Audigent)
- Publink (Epsilon)
- SharedID
- EUID
- Yahoo Connect ID
- Panorama ID
- The Trade Desk
- NetID
- LiveRamp  
- UID 2.0
- Publisher Provided Id / PPID (publishers can register their own source via API and can pass the user id).

You can set **User ID** by

- creating an array of **ANUserId** objects, and
- assigning the array of objects to the **`userIdArray`** property
  of `ANSDKSettings` in Mobile SDK API.

| Property     | Type    | Attribute | Description                                                             |
|-------------|---------|-----------|-------------------------------------------------------------------------|
| `userIdArray` | `NSArray` | readwrite | Specifies a dictionary containing objects that hold User ID parameters. |

```
// In ANSDKSettings.h: 
/**
 A Dictionary containing objects that hold UserId parameters.
 */ 
@property (nonatomic, readwrite, strong, nullable) NSArray<ANUserId *>  *userIdArray ;
```

```
// In ANUserId.h
 
/*
 *  Supported Third Party ID Sources
 * */
typedef NS_ENUM(NSUInteger, ANUserIdSource) {
    ANUserIdSourceLiveRamp,
    ANUserIdSourceNetId,
    ANUserIdSourceCriteo,
    ANUserIdSourceTheTradeDesk,
    ANUserIdSourceUID2
};
 
 
/**
 Defines the User Id Object from an Extended Third Party Source
 */
@interface ANUserId : NSObject
 
/**
 Source of the User Id
 */
@property (nonatomic, readwrite, strong, nonnull) NSString *source;
 
/**
 The User Id String
 */
@property (nonatomic, readwrite, strong, nonnull) NSString *userId;
 
 
- (nullable instancetype)initWithSource:(ANUserIdSource)source userId:(nonnull NSString *)userId; 
- (nullable instancetype)initWithStringSource:(nonnull NSString *)source userId:(nonnull NSString *)userId isFirstParytId:(BOOL)firstParytId;   
@end
```

## Examples of use

```
// iOS: ObjC to show a banner ad
#import "MyViewController.h"
#import "ANBannerAdView.h"
@interface MyViewController ()
@property (nonatomic, strong)  ANBannerAdView *banner;
@end
  
@implementation MyViewController
ANBannerAdView *banner = nil;
  
- (void) viewDidLoad
  
{
     
    // User Id from External Third Party Sources     
NSMutableArray<ANUserId *>  *userIdArray  = [[NSMutableArray<ANUserId *> alloc] init];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceNetId userId:@"userid-netid-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceTheTradeDesk userId:@"userid-ttd-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceUID2 userId:@"userid-uid2-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceCriteo userId:@"userid-Criteo-foobar"]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceLiveRamp userId:@"userid-liveramp-foobar" ]]; 
[userIdArray addObject:[[ANUserId alloc] initWithStringSource:@“Generic Source” userId:@“userid-generic-foobar” isFirstParytId:true]];    
ANSDKSettings.sharedInstance.userIdArray = userIdArray;
 
    // Publisher User Id
    ANSDKSettings.sharedInstance.publisherUserId = @"foobar-publisherfirstpartyid";      
        // IDFV as Publisher User Id
        ANSDKSettings.sharedInstance.disableIDFVUsage = NO;     
        // Load Banner Ad
    CGSize  size = CGSizeMake(300, 250); 
    // NOTE  Setting size is necessary only for fetching banner and video ad objects.
    // This field is ignored when the placement returns a native ad object.
    CGRect someRect = CGRectMake(...);
    // Create the banner ad view here, but wait until the delegate fires before displaying.
  
    self.banner = [ANBannerAdView adViewWithFrame:someRect placementId:@"13572468" adSize:size];
    //... Needed Setup
    // Load an ad!
    [self.banner loadAd];
  
}
  
@end
```
