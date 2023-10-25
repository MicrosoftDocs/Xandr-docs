---
Title : User ID(s) Mapping on iOS
Description : <b>Note:</b> This offering is currently in
Alpha and is subject to changes or deprecation without notice.
ms.custom : android-ios
---


# User ID(s) Mapping on iOS





<b>Note:</b> This offering is currently in
Alpha and is subject to changes or deprecation without notice.





## Overview

Xandr offers you the option of sending
**Publisher First party ID** and **User ID(s)** from third party sources
in ad requests. They are global settings and it is sufficient to set the
User ID(s) once per app session as these values would be used in all
consecutive ad requests in the same session. Please note that,
Xandr does not store these values across
different app sessions.





## Mobile SDK Structure

**Publisher First Party ID**



<b>Note:</b> Deprecation Notice

**`The` `externalUid`** property
of **`ANBannerAdView`**, **`InterstitialAdView`**, **`ANNativeAdRequest`** and **`ANInstreamVideoAd`** class
is now deprecated. You can use **`publisherUserId`** property described
below in **`ANSDKSettings`** class instead. The deprecated methods will
be removed in SDK v8.0.



You can set **Publisher First Party ID** using
the `publisherUserId` property of  `ANSDKSettings` in MobileSDK API.

<table class="table">
<thead class="thead">
<tr class="header row">
<th id="ID-00003485__entry__1"
class="entry colsep-1 rowsep-1">Property</th>
<th id="ID-00003485__entry__2" class="entry colsep-1 rowsep-1">Type</th>
<th id="ID-00003485__entry__3"
class="entry colsep-1 rowsep-1">Attribute</th>
<th id="ID-00003485__entry__4"
class="entry colsep-1 rowsep-1">Description</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__1"><code
class="ph codeph">publisherUserId</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__2"><code
class="ph codeph">NSString</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__3">readwrite</td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__4">Specifies a string that corresponds to
the Publisher User ID for current application user.</td>
</tr>
</tbody>
</table>

**IDFV as Publisher First Party ID**

Due to introduction of App Tracking Transparency (ATT) changes in iOS
14.5 and above, Xandr Mobile SDK offers the
publishers to use **Identifier for Vendors (IDFV) **of the device in
cases where there is no in-house **Publisher First Party
ID** and **Identifier for Advertisers (IDFA)** is available.
This feature facilitates the publishers to pass IDFV in the ad requests
automatically whenever both of the Publisher First Party ID and IDFA is
absent. This feature is enabled by default and if the publishers want to
turn it off, they can use `disableIDFVUsage` property
of  `ANSDKSettings` in MobileSDK API.

<table class="table">
<thead class="thead">
<tr class="header row">
<th id="ID-00003485__entry__9"
class="entry colsep-1 rowsep-1">Property</th>
<th id="ID-00003485__entry__10"
class="entry colsep-1 rowsep-1">Type</th>
<th id="ID-00003485__entry__11"
class="entry colsep-1 rowsep-1">Attribute</th>
<th id="ID-00003485__entry__12"
class="entry colsep-1 rowsep-1">Description</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__9"><code
class="ph codeph">disableIDFVUsage</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__10"><code
class="ph codeph">BOOL</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__11">readwrite</td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__12">Specifies a boolean value which exclude
the IDFV field in ad request. Default value of the property is set
to <strong>NO </strong>and IDFV will be used in cases where both IDFV
and Publisher First Party ID are not present for a given ad
request.</td>
</tr>
</tbody>
</table>

``` pre
/**
An AppNexus disableIDFVUsage  is a boolean value which exclude the IDFV field in ad request. Default value of disableIDFVUsage is set to NO and IDFV will be used in cases where IDFV and Publisher First Party ID is not present.
*/
@property (nonatomic, readwrite) BOOL disableIDFVUsage;
```

  
**User ID**



<b>Note:</b> Deprecation Notice

The
 property \`**ANSDKSettings.externalUserIdArray**\` and \`**ANExternalUserId**\` class
are now deprecated and will be removed in SDK v8.0. You can use the
equivalent
property \`**ANSDKSettings.userIdArray**\`  and \`**ANUserId**\` class
described below instead as a replacement.



Xandr supports User ID(s) from the below
external sources:

- Criteo
- The Trade Desk
- NetID
- LiveRamp  
- UID 2.0
- Publisher Provided Id / PPID (publishers can register their own source
  via API and can pass the user id)

You can set **User ID** by

- creating an array of **ANUserId** objects, and
- assigning the array of objects to the **userId`Array`** property
  of `ANSDKSettings `in MobileSDK API  
    

<table class="table">
<thead class="thead">
<tr class="header row">
<th id="ID-00003485__entry__17"
class="entry colsep-1 rowsep-1">Property</th>
<th id="ID-00003485__entry__18"
class="entry colsep-1 rowsep-1">Type</th>
<th id="ID-00003485__entry__19"
class="entry colsep-1 rowsep-1">Attribute</th>
<th id="ID-00003485__entry__20"
class="entry colsep-1 rowsep-1">Description</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__17"><code
class="ph codeph">userIdArray</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__18"><code
class="ph codeph">NSArray</code></td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__19">readwrite</td>
<td class="entry colsep-1 rowsep-1"
headers="ID-00003485__entry__20">Specifies a dictionary containing
objects that hold User ID parameters.</td>
</tr>
</tbody>
</table>

``` pre
// In ANSDKSettings.h: 
/**
 A Dictionary containing objects that hold UserId parameters.
 */ 
@property (nonatomic, readwrite, strong, nullable) NSArray<ANUserId *>  *userIdArray ;
```

``` pre
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





## Examples of Use

``` pre
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






