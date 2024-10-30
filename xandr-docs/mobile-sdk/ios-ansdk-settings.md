---
title: iOS ANSDK Settings
description: In this article, find information about the various iOS ANSDK settings to help you in the development of your app. 
ms.custom: ios-sdk
ms.date: 04/22/2024
ms.author: shsrinivasan
---

# iOS ANSDK settings

Xandr Mobile SDK provides various settings you can use to help you in the development of your app. In this article, find details about the methods or properties, input parameters, returned values, restrictions, guidelines, and examples for the iOS ANSDK settings.

| Property | Description |
|--|--|
| `(void) optionalSDKInitialization:(sdkInitCompletion _Nullable)success` | Pre-configures common settings such as checking the presence of the User Agent during initialization, preparing a WebView, etc. <br><br> See [Initialize SDK Settings](#initialize-sdk-settings) below for more details. |
| `NSString *publisherUserId` | Specifies the Publisher User ID for current application user. <br><br> See [User ID(s) Mapping](#user-ids-mapping) below for more details. |
| `NSArray<ANUserId *> *userIdArray` | Specifies a dictionary containing objects that hold User ID parameters. <br><br> See User ID(s) Mapping below for more details. |
| `BOOL disableIDFVUsage` | Includes or excludes the IDFV field in ad request. <br><br> See [User ID(s) Mapping](#user-ids-mapping) below for more details. |
| `NSString *geoOverrideCountryCode` | Assigns a country code. <br><br> See [Support for Overriding Country Codes and Zip Codes](#support-for-overriding-country-codes-and-zip-codes) below for more details. |
| `NSString *geoOverrideZipCode` | Assigns a zip code. <br><br> See [Support for Overriding Country Codes and Zip Codes](#support-for-overriding-country-codes-and-zip-codes) below for more details. |
| `(void)setLocationWithLatitude:(CGFloat)latitude longitude:(CGFloat)longitude timestamp:(nullable NSDate *)timestamp horizontalAccuracy:(CGFloat)horizontalAccuracy precision:(NSInteger)precision` | Controls how accurate the location data is that you pass to the ad server. <br><br> See [Location Controls](#location-controls) below for more details. |
| `BOOL locationEnabledForCreative` | Controls the location access for creatives. <br><br> See [Location Controls](#location-controls) below for more details. |
| `BOOL doNotTrack` | Indicates if you have information in the app about user opt-out. <br><br> See [Publisher Side User Opt-Out](#publisher-side-user-opt-out) below for more details. |
| `BOOL disableIDFAUsage` | Excludes the IDFA field in ad request. <br><br> See [Set IDFA usage](#set-idfa-usage) below for more details. |
| `NSUInteger auctionTimeout` | Sets the timeout period in milliseconds. <br><br> See [Set the Auction Timeout](#set-the-auction-timeout) below for more details. |
| `BOOL enableTestMode` | Sets YES or NO for the AdRequests to be executed in the test mode. <br><br> See [Set Test Mode](#set-test-mode) below for more details. |
| `BOOL enableOMIDOptimization` | Enables Open-Measurement Optimization. <br><br> See [OMID Optimization](#omid-optimization) below for more details. |
| `NSString *contentlanguage` | Sets the code for the content's language. <br><br> See [Set Content Language](#set-content-language) below for more details. |

## Initialize SDK settings

| Method | Description |
|--|--|
| `(void) optionalSDKInitialization:(sdkInitCompletion _Nullable)success` | Method that allows you to pre-configure common settings such as checking the presence of the User Agent during SDK initialization, preparing a WebView etc. <br> The completion block of this Property returns **“true”** if SDK initialization completes successfully and **“false”** if it fails. |

### Example

#### [Objective C](#tab/objectivec1)

```
[[ANSDKSettings sharedInstance] optionalSDKInitialization:^(BOOL isSDKInitialized) {
 if(isSDKInitialized){
      NSLog(@"SDK Initialized");
    }else{
      NSLog(@"SDK did not initialize");
    }
  }];
```

#### [Swift](#tab/swift1)

```
ANSDKSettings.sharedInstance().optionalSDKInitialization { (isSDKInitialized) in
       print("SDK Initialized \(isSDKInitialized)")
}
```

---

## User ID(s) mapping

> [!IMPORTANT]
>
> - This offering is currently in Alpha and is subject to changes or deprecation without notice.
> - The externalUid property of `ANBannerAdView`, `InterstitialAdView`, `ANNativeAdRequest` and `ANInstreamVideoAd` class is now deprecated. You can use `publisherUserId` property described below in `ANSDKSettings` class instead. The deprecated properties will be removed in SDK v8.0.
> - The property `ANSDKSettings.externalUserIdArray` and `ANExternalUserId` class are now deprecated and will be removed in SDK v8.0. You can use the equivalent property `ANSDKSettings.userIdArray` and `ANUserId` class described below instead as a replacement.

| Property | Description |
|--|--|
| `NSString *publisherUserId` | Specifies a string that corresponds to the Publisher User ID for current application user. |
| `NSArray<ANUserId *> *userIdArray` | Specifies a dictionary containing objects that hold User ID parameters. <br><br> Xandr supports User ID(s) from the below external sources: <br> - Criteo <br> - The Trade Desk <br> - NetID <br> - LiveRamp <br> - UID 2.0 <br> - Publisher Provided Id / PPID (publishers can register their own source via API and can pass the user id) <br><br> You can set **User ID** by - <br> - creating an array of **ANUserId** objects, and <br> - assigning the array of objects to the **userId Array** property of **ANSDKSettings** in MobileSDK API. |
| `BOOL disableIDFVUsage` | Specifies a boolean value which exclude the IDFV field in ad request. Default value of the property is set to NO. <br><br> Due to introduction of App Tracking Transparency (ATT) changes in iOS 14.5 and above, publishers can use Identifier for Vendors (IDFV) of the device in cases where there is no in-house Publisher First Party ID and Identifier for Advertisers (IDFA) is available. <br><br> IDFV will be used in cases where both IDFV and Publisher First Party ID are not present for a given ad request. |

> [!NOTE]
>
> - Publisher ID and User ID are global settings.
> - It is sufficient to set the User ID(s) once per app session as these values would be used in all consecutive ad requests in the same session.
> - Xandr does not store these values across different app sessions.

### Example

#### [Objective C](#tab/objectivec2)

```
// User Id from External Third Party Sources
NSMutableArray<ANUserId *>  *userIdArray  = [[NSMutableArray<ANUserId *> alloc] init];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceNetId userId:@"userid-netid-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceTheTradeDesk userId:@"userid-ttd-foobar" ]];
ANSDKSettings.sharedInstance().disableIDFAUsage = true[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceUID2 userId:@"userid-uid2-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceCriteo userId:@"userid-Criteo-foobar"]];
[userIdArray addObject:[[ANUserId alloc] initWithANUserIdSource:ANUserIdSourceLiveRamp userId:@"userid-liveramp-foobar" ]];
[userIdArray addObject:[[ANUserId alloc] initWithStringSource:@"Generic Source" userId:@"userid-generic-foobar" isFirstParytId:true]];
ANSDKSettings.sharedInstance.userIdArray = userIdArray;
 
// Publisher User Id
ANSDKSettings.sharedInstance.publisherUserId = @"foobar-publisherfirstpartyid";
 
// IDFV as Publisher User Id
ANSDKSettings.sharedInstance.disableIDFVUsage = NO;
```

#### [Swift](#tab/swift2)

```
// User Id from External Third Party Sources
var userIdArray: [ANUserId] = []
if let netIdUser = ANUserId(anUserIdSource: .netId, userId: "userid-netid-foobar") {
    userIdArray.append(netIdUser)
}
if let ttdUser = ANUserId(anUserIdSource: .theTradeDesk, userId: "userid-ttd-foobar") {
   userIdArray.append(ttdUser)
}
if let uid2User = ANUserId(anUserIdSource: .UID2, userId: "userid-uid2-foobar") {
   userIdArray.append(uid2User)
}
if let criteoUser = ANUserId(anUserIdSource: .criteo, userId: "userid-Criteo-foobar") {
   userIdArray.append(criteoUser)
}
if let liveRampUser = ANUserId(anUserIdSource: .liveRamp, userId: "userid-liveramp-foobar") {
   userIdArray.append(liveRampUser)
}
if let genericUser = ANUserId(stringSource: "Generic Source", userId: "userid-generic-foobar", isFirstParytId: true) {
   userIdArray.append(genericUser)
}
ANSDKSettings.sharedInstance().userIdArray = userIdArray
 
// Publisher User Id
ANSDKSettings.sharedInstance().publisherUserId = "foobar-publisherfirstpartyid"
 
// IDFV as Publisher User Id
ANSDKSettings.sharedInstance().disableIDFVUsage = false
```

---

## Support for overriding country codes and zip codes

The SDK uses City/DMA/Country information from standard feed (log level data) for reporting purposes. However, these values need to be overwritten from reverser geocoded latitude and longitude data to keep the data sanity intact. If those values are not overwritten, log level data will point to the IP-address based locations and eventually will project wrong data set, especially with mobile data.

| Property | Description |
|--|--|
| `NSString *geoOverrideCountryCode` | Indicates a string value to override country code. |
| `NSString *geoOverrideZipCode` | Indicates a string value to override zip code. |

### Example

#### [Objective C](#tab/objectivec3)

```
//Set
ANSDKSettings.sharedInstance.geoOverrideCountryCode = @"US";
ANSDKSettings.sharedInstance.geoOverrideZipCode = @"10010";
.......
//Get
NSString* countryCode = ANSDKSettings.sharedInstance.geoOverrideCountryCode;
NSString* zipCode = ANSDKSettings.sharedInstance.geoOverrideZipCode
```

#### [Swift](#tab/swift3)

```
//Set
ANSDKSettings.sharedInstance().geoOverrideCountryCode = "US"
ANSDKSettings.sharedInstance().geoOverrideZipCode = "10010"
.......
//Get
let countryCode = ANSDKSettings.sharedInstance().geoOverrideCountryCode;
let zipCode = ANSDKSettings.sharedInstance().geoOverrideZipCode
```

---

## Location controls

| Property | Description |
|--|--|
| `(void)setLocationWithLatitude:(CGFloat)latitude longitude:(CGFloat)longitude timestamp:(nullable NSDate *)timestamp horizontalAccuracy:(CGFloat)horizontalAccuracy precision:(NSInteger)precision` | Method to control how accurate the location data is that you pass to the ad server. Better location data may lead to better monetization of your ads. |
| `BOOL locationEnabledForCreative` | Property to control the location access for creatives. Default is YES. NO disables the location from the creative. <br><br> Creatives rendered in a WebView can access a user's location through HTML5 location APIs. <br><br> **Note**: <br> - By default, when a creative asks for location, a popup is displayed to the users asking for explicit permission to use the location. <br> - When location access is disabled, popups won't be shown to the users and the creative will receive a PERMISSION_DENIED error for HTML5 location API calls. |

The `precision` parameter will cause all location information to be internally rounded to the specified number of digits after the decimal before being passed to the ad server. The correlation between the value of `precision` and location accuracy distance is as follows:

| Precision (Integer) | Resolution Accuracy |
|--|--|
| 2 | Approx. 1 kilometer |
| 3 | Approx. 100 meters |
| 4 | Approx. 10 meters |
| -1 | Full resolution is passed |

### Example

#### [Objective C](#tab/objectivec4)

```
CLLocation *location = [locationManager location];
NSDate *now = [NSDate date];
[banner.setLocationWithLatitude:location.coordinate.latitude
  longitude:location.coordinate.longitude
  timestamp: now
  horizontalAccuracy: location.horizontal_accuracy
  precision: 4];
```

#### [Swift](#tab/swift4)

```
if let location = locationManager.location {
    let now = Date()
    banner.setLocationWithLatitude(
    location.coordinate.latitude,
    longitude: location.coordinate.longitude,
    timestamp: now,
    horizontalAccuracy: location.horizontalAccuracy,
    precision: 4
 )
}
 
ANSDKSettings.sharedInstance().locationEnabledForCreative = false
```

---

## Publisher side user opt-out

For any AdRequest, Xandr Mobile SDK checks in the device or OS environment level and populates the value for limitAdTracking (LMT) in the background automatically. If LMT=true, it indicates that the user opts out from tracking at the device or OS settings. However, the publishers retain information about their users' opt-in/out of tracking and thus are required to pass that information if their user has opted out to comply with their privacy regulations. To facilitate this, publisher side user opt-out feature has been introduced to the Mobile SDK.

| Property | Description |
|--|--|
| `BOOL doNotTrack` | Indicates if you have information in the app about user opt-out. If set to YES, tracking cookies and IDFA will be disabled for all future auctions. Default value is NO. |

### Example

#### [Objective C](#tab/objectivec5)

```
[ANSDKSettings sharedInstance].doNotTrack = YES;
```

#### [Swift](#tab/swift5)

```
ANSDKSettings.sharedInstance().doNotTrack = true
```

---

## Set IDFA usage

The Identifier for Advertisers (IDFA) is an Apple provided ID to track the users with their consent for advertising purposes by the publishers who have an app on the Apple App Store. An API is introduced in Xandr mobile SDK to enable or disable IDFA usage by including or excluding the IDFA field in the ad request.

| Property | Description |
|--|--|
| `BOOL disableIDFAUsage` | Property to exclude the IDFA field in ad request. Default value is NO. |

### Example

#### [Objective C](#tab/objectivec6)

```
[ANSDKSettings sharedInstance].disableIDFAUsage = YES;
```

#### [Swift](#tab/swift6)

```
ANSDKSettings.sharedInstance().disableIDFAUsage = true
```

---

## Set the auction timeout

| Property | Description |
|--|--|
| `NSUInteger auctionTimeout` | Sets the time period, in milliseconds, to wait for a bidder to respond to a bid request. <br><br> If the bidder fails to respond within the value set for time out period (for example, 500 milliseconds), the bid request would result in failure. |

### Example

#### [Objective C](#tab/objectivec7)

```
[[ANSDKSettings sharedInstance] setAuctionTimeout:500];
```

#### [Swift](#tab/swift7)

```
ANSDKSettings.sharedInstance().auctionTimeout = 500
```

---

## Set test mode

| Property | Description |
|--|--|
| `BOOL enableTestMode` | Sets YES or NO for the AdRequests to be executed in the test mode for debugging or testing. Default value is NO. <br><br> **Note**: The scope of setting the test mode for AdRequest execution as YES is limited to debugging/development or testing purpose only, and not to be used in a production environment. Enabling the test mode in a production environment leads to unintended consequences and impacts the monetization of your app. |

### Example

#### [Objective C](#tab/objectivec8)

```
ANSDKSettings.sharedInstance.enableTestMode = YES;
```

#### [Swift](#tab/swift8)

```
ANSDKSettings.sharedInstance().enableTestMode = true
```

---

## OMID Optimization

The Open Measurement Software Development Kit (OM SDK) from the IAB enables third-party viewability and verification for ads in mobile app environments. The Open Measurement Interface Definition (OMID) facilitates the collection of data regarding ad viewability on mobile devices. Certain UI elements, such as close buttons and logos, are excluded from viewability calculations. This exclusion ensures accurate measurement while preserving the integrity of essential ad components. For more details, visit the IAB [OM SDK page](https://iabtechlab.com/standards/open-measurement-sdk/).

The Open Measurement Software Development Kit (OM SDK) is designed to facilitate third party viewability and verification measurement for ads served to mobile app environments without requiring multiple Ad Verification Service Providers (Measurement Provider) SDKs.

Open Measurement Interface Definition (OMID) is an open measurement API provided by IAB. In short, it enables a publisher to get data on the viewability of an ad within a mobile device. For more detailed information about OMID, visit the IAB site [here](https://iabtechlab.com/standards/open-measurement-sdk/).

<!-- Friendly obstructions are the views that OMID will exclude from all viewability calculations when added to the OMID Session. When a UI element needs to be considered as a part of the ad, that can be added as a friendly obstruction to prevent it from counting towards coverage of the ad. For example, any native element such as a close button, some logo text, or other object that needs to be considered as a part of an ad (and not be counted for viewability measurement) should be registered as a friendly obstruction. This applies to any ancestor or peer views in the view hierarchy.!-->

The OMID API enables:

- Adding a friendly obstruction
- Removing a friendly obstruction
- Removing all friendly obstructions

In addition to the above-mentioned functionalities, the OM SDK facilitates a property (`enableOMIDOptimization`) that enables optimization.

To add a friendly obstruction, remove a friendly obstruction, or remove all friendly obstruction for Banner, Interstitial, and Video AdUnits, you need to pass the view as an argument to the API.

> [!NOTE]
> Native AdUnits do not support remove API.

| Property | Description |
|--|--|
| `BOOL enableOMIDOptimization` | Indicates if Open-Measurement Optimization for viewability and verification measurement for ads served is enabled and if not, enable the same. Default value is NO. <br><br> When set as "YES", the OM SDK takes care of performing Open-Measurement Optimization. Here, as part of optimization, viewability is tracked until an ad is fully visible to the user. Once the ad ceases to be visible, viewability tracking stops. <br><br> **Note**: This API supports only banner and native ad types. |

### Example

#### [Objective C](#tab/objectivec9)

```
ANSDKSettings.sharedInstance.enableOMIDOptimization = true;
 
```

#### [Swift](#tab/swift9)

```
ANSDKSettings.sharedInstance().enableOMIDOptimization = true
 
```

## Set content language

| Property | Description |
|--|--|
| `NSString *contentlanguage` | Sets the two-letter ANSI code for the content's language; for example, `EN`. |

### Example

#### [Objective C](#tab/objectivec10)

```
ANSDKSettings.sharedInstance.contentLanguage = @"EN";
```

#### [Swift](#tab/swift10)

```
ANSDKSettings.sharedInstance().contentLanguage = "EN"
```

---
