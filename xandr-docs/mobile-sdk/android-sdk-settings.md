---
title: Android SDK Settings
description: In this article, find information about the various Android SDK settings to help you in the development of your app. 
ms.custom: android-sdk
ms.date : 04/22/2024
ms.author: shsrinivasan
---

# Android SDK settings

Xandr Mobile SDK provides various settings you can use to help you in the development of your app. In this article, find details about the methods, input parameters, returned values, restrictions, guidelines, and examples for the Android SDK settings.

| Function | Description |
|--|--|
| `void init()` | Activates OMID, fetches User Agent and AAID (Google Advertising ID) for devices. <br><br> See [Initialize SDK Settings](#initialize-sdk-settings) below for more details. |
| `void setPublisherUserId(String publisherUserId)` | Sends Publisher First party ID and User ID(s) from third party sources in ad requests. <br><br> See [User ID(s) Mapping](#user-ids-mapping) below for more details. |
| `void setUserIds(List<ANUserId> userIdList)` | Sets User ID in ANSDKSettings class. <br><br> See [User ID(s) Mapping](#user-ids-mapping) below for more details. |
| `void setGeoOverrideCountryCode(String countryCode)` | Assigns a country code. <br><br> See [Support for Overriding Country Codes and Zip Codes](#support-for-overriding-country-codes-and-zip-codes) below for more details. |
| `void setGeoOverrideZipCode(String zipCode)` | Assigns a zip code. <br><br> See [Support for Overriding Country Codes and Zip Codes](#support-for-overriding-country-codes-and-zip-codes) below for more details. |
| `void setLocationDecimalDigits(int digitsAfterDecimal)` | Controls how accurate the location data is that you pass to the ad server. <br><br> See [Location Controls](#location-controls) below for more details. |
| `void setLocationEnabledForCreative(Boolean enabled)` | Controls the location access for creatives. <br><br> See [Location Controls](#location-controls) below for more details. |
| `void enableBackgroundThreading(Boolean enable)` | Enables or disables the Background Threading feature flag. <br><br> See [Background Threading](#background-threading) below for more details. |
| `void setDoNotTrack(Boolean dnt)` | Enables the publisher side user opt-out feature. <br><br> See [Publisher Side User Opt-Out](#publisher-side-user-opt-out) below for more details. |
| `void disableAAIDUsage(Boolean disable)` | Enables or disables the disableAAIDUsage. <br><br> See [Set AAID usage](#set-aaid-usage) below for more details. |
| `void setAuctionTimeout(long auctionTimeout)` | Sets the timeout period in milliseconds. <br><br> See [Set the Auction Timeout](#set-the-auction-timeout) below for more details. |
| `void enableTestMode(Boolean enabled)` | Sets true or false for the AdRequests to be executed in the test mode. <br><br> See [Set Test Mode](#set-test-mode) below for more details. |
| `void setContentLanguage(String contentLanguage)` | Sets the code for the content's language. <br><br> See [Set Content Language](#set-content-language) below for more details. |

## Initialize SDK settings

| Function | Description |
|--|--|
| `void init(Context context, final InitListener listener)` <br><br> **Overloaded method**: <br> `void init(final Context context, final InitListener listener, final boolean fetchUserAgent, final boolean fetchAAID, final boolean enableWarmUpAdCall, final boolean preFetchWebView)` | Method that activates OMID, fetch User Agent, AAID (Google Advertising ID), enables `WarmUpAdCall` and prefetch WebView for devices. <br><br> Additionally, the overloaded `init()` method optionally disables fetching of AAID, UserAgent, `enableWarmUpAdCall`, and `preFetchWebView`. It requires enable/disable booleans for `fetchUserAgent`, `fetchAAID`, `enableWarmUpAdCall`, and `preFetchWebView` as arguments. |

### Example

#### [Java](#tab/java1)

##### Regular Init method

```
SDKSettings.init(this, new SDKSettings.InitListener() {
    @Override
    public void onInitFinished() {
        // Initialisation finished
    }
});
```

##### Overloaded Init method with flexibility to enable / disable fetching of User Agent, AAID, WarmUpAdCall and Prefetch WebView

```
SDKSettings.init(this, new SDKSettings.InitListener() {
    @Override
    public void onInitFinished() {
        // Initialisation finished
    }
}, false, true, false, false);
//Boolean values false/true are optional and as per usage
```

#### [Kotlin](#tab/kotlin1)

##### Regular Init method

```
SDKSettings.init(this) {
       // Initialization finished
}
```

##### Overloaded init method

```
SDKSettings.init(this, {
     // Initialization finished
}, false, true, false, false)
```

---

## User ID(s) mapping

> [!IMPORTANT]
>
> - This offering is currently in Alpha and is subject to changes or deprecation without notice.
> - The `setExternalUid` and `getExternalUid` methods available in `NativeAdRequest`, `VideoAd`, `BannerAdView`, and `InterstitialAdView` classes are deprecated. You can use `setPublisherUserId` and `getPublisherUserId` described below in `SDKSettings` class instead. The deprecated methods will be removed in SDK v8.0.
> - The `setExternalUserIds` and `getExternalUserIds` methods available in `SDKSettings` class and `ANExternalUserIdSource` class are now deprecated and will be removed in SDK v8.0. You can use `setUserIds` and `getUserIds` methods in `SDKSettings` class and `ANUserId` class described below instead as a replacement.

| Function  | Description  |
|---|---|
| `void setPublisherUserId(String publisherUserId)`  | Method that sets Publisher (First Party) User ID in `SDKSettings` class in MobileSDK API.   |
| `void setUserIds(List<ANUserId> userIdList)` | Method that sets User ID in `ANSDKSettings` class in MobileSDK API. <br><br> You can set User ID by – <br> - creating a List of `ANUserId` objects, and <br> - assigning the List to the `setUserIds()` method in `ANSDKSettings`. <br><br> Xandr supports User ID(s) from the below sources: <br> - Criteo <br> - The Trade Desk <br> - NetID <br> - LiveRamp <br> - UID 2.0 <br> - Publisher Provided Id / PPID (publishers can register their own source via API and can pass the user id). |

> [!NOTE]
>
> - Publisher ID and User ID are global settings.
> - It is sufficient to set the User ID(s) once per app session as these values would be used in all consecutive ad requests in the same session.
> - Xandr does not store these values across different app sessions.

### Example

#### [Java](#tab/java2)

```
List<ANUserId> userIds = new ArrayList<>();
ANUserId tradeDeskUserID = new ANUserId(ANUserId.Source.THE_TRADE_DESK, "userid-ttd-foobar");
userIds.add(tradeDeskUserID);
ANUserId criteoUserId = new ANUserId(ANUserId.Source.CRITEO, "userid-Criteo-foobar");
userIds.add(criteoUserId);
ANUserId netIdUserID = new ANUserId(ANUserId.Source.NETID, "userid-netid-foobar");
userIds.add(netIdUserID);
ANUserId liveRampUserID = new ANUserId(ANUserId.Source.LIVERAMP, "userid-liveramp-foobar");
userIds.add(liveRampUserID);
ANUserId UID2UserId = new ANUserId(ANUserId.Source.UID2, "userid-uid2-foobar");
userIds.add(UID2UserId);
ANUserId genericUserID = new ANUserId("Generic Source", "userid-generic-foobar");
userIds.add(genericUserID);
 
// Set User Id from External Sources
SDKSettings.setUserIds(userIds);
 
// Setting Publisher First Party Id
SDKSettings.setPublisherUserId("PublisherUserId-foobar");
```

#### [Kotlin](#tab/kotlin2)

```
val userIds: MutableList<ANUserId> = ArrayList()
val tradeDeskUserID = ANUserId(ANUserId.Source.THE_TRADE_DESK, "userid-ttd-foobar")
userIds.add(tradeDeskUserID)
val criteoUserId = ANUserId(ANUserId.Source.CRITEO, "userid-Criteo-foobar")
userIds.add(criteoUserId)
val netIdUserID = ANUserId(ANUserId.Source.NETID, "userid-netid-foobar")
userIds.add(netIdUserID)
val liveRampUserID = ANUserId(ANUserId.Source.LIVERAMP, "userid-liveramp-foobar")
userIds.add(liveRampUserID)
val UID2UserId = ANUserId(ANUserId.Source.UID2, "userid-uid2-foobar")
userIds.add(UID2UserId)
val genericUserID = ANUserId("Generic Source", "userid-generic-foobar")
userIds.add(genericUserID)
 
// Set User Id from External Sources
SDKSettings.setUserIds(userIds)
 
// Setting Publisher First Party Id
SDKSettings.setPublisherUserId("PublisherUserId-foobar")
```

---

## Support for overriding country codes and zip codes

The SDK uses City/DMA/Country information from standard feed (log level data) for reporting purposes. However, these values need to be overwritten from reverser geocoded latitude and longitude data to keep the data sanity intact. If those values are not overwritten, log level data will point to the IP-address based locations and eventually will project wrong data set, especially with mobile data.

| Function | Description |
|--|--|
| `void setGeoOverrideCountryCode(String countryCode)` | Method which assigns a country code. It will pass the country code string as the argument in the method. |
| `void setGeoOverrideZipCode(String zipCode)` | Method which assigns a zip code. It will pass the zip code string as the argument in the method. |

### Example

#### [Java](#tab/java3)

```
//Setter
SDKSettings.setGeoOverrideCountryCode("US");
SDKSettings.setGeoOverrideZipCode("10010");
  
//Getter
SDKSettings.getGeoOverrideCountryCode();
SDKSettings.getGeoOverrideZipCode();
```

#### [Kotlin](#tab/kotlin3)

```
//Setter
SDKSettings.setGeoOverrideCountryCode("US")
SDKSettings.setGeoOverrideZipCode("10010")
 
//Getter
SDKSettings.getGeoOverrideCountryCode()
SDKSettings.getGeoOverrideZipCode()
```

---

## Location controls

| Function | Description |
|--|--|
| `void setLocationDecimalDigits(int digitsAfterDecimal)` | Method to control how accurate the location data is that you pass to the ad server. Better location data may lead to better monetization of your ads. |
| `void setLocationEnabledForCreative(boolean enabled)` | Method to control the location access for creatives. Default is true. False disables the location pop-up from the creative. <br><br> Creatives rendered in a WebView can access a user's location through HTML5 location APIs. <br><br> **Note**: <br> - By default, when a creative asks for location, a popup is displayed to the users asking for explicit permission to use the location. <br> - When location access is disabled, popups won't be shown to the users and the creative will receive a PERMISSION_DENIED error for HTML5 location API calls. |

The `digitsAfterDecimal` argument will cause all location information to be internally rounded to the specified number of digits after the decimal before being passed to the ad server. The correlation between the value of `digitsAfterDecimal` and location accuracy distance is as follows:

| Digits after Decimal | Resolution Accuracy |
|--|--|
| 2 | Approx. 1 kilometer |
| 3 | Approx. 100 meters |
| 4 | Approx. 10 meters |
| -1 | Full resolution is passed |

### Example

#### [Java](#tab/java4)

```
SDKSettings.setLocationDecimalDigits(2);
SDKSettings.setLocationEnabledForCreative(false);  
```

#### [Kotlin](#tab/kotlin4)

```
SDKSettings.setLocationDecimalDigits(2)
SDKSettings.setLocationEnabledForCreative(false)
```

---

## Background threading

> [!IMPORTANT]
> This offering is currently in Alpha and is subject to change.

| Function | Description |
|--|--|
| `void enableBackgroundThreading(boolean enable)` | Method used to enable or disable the Background Threading feature flag. Enabling this feature enables MobileSDK to execute the ad requests for different AdUnits like banner, interstitial, native, and videos as a background thread instead of a UI thread. <br><br> By default the boolean value for the method is set to false (which uses AsyncTask of Android). <br><br> To enable the feature of background threading, the value needs to be set as true in the method. <br><br> **Note**: This method should be called before the `init()` method. |

### Example

#### [Java](#tab/java5)

```
// enable the Background threading
SDKSettings.enableBackgroundThreading(true);
```

#### [Kotlin](#tab/kotlin5)

```
// enable the Background threading
SDKSettings.enableBackgroundThreading(true)
// call init before requesting the Ad
SDKSettings.init(this) {      
 // Initialization finished
}
```

---

## Publisher side user opt-out

For any AdRequest, Xandr Mobile SDK checks in the device or OS environment level and populates the value for limitAdTracking (LMT) in the background automatically. If LMT=true, it indicates that the user opts out from tracking at the device or OS settings. However, the publishers retain information about their users' opt-in/out of tracking and thus required to pass that information if their user has opted out to comply with their privacy regulations. To facilitate the same, publisher side user opt-out feature is introduced in Mobile SDK.

| Function | Description |
|--|--|
| `void setDoNotTrack(boolean dnt)` | Method which enables the publisher side user opt-out feature. |

### Example

#### [Java](#tab/java6)

```
//Setter
SDKSettings.setDoNotTrack(true);
//Getter
SDKSettings.getDoNotTrack();
```

#### [Kotlin](#tab/kotlin6)

```
//Setter
SDKSettings.setDoNotTrack(true)
//Getter
SDKSettings.getDoNotTrack()
```

---

## Set AAID usage

The Google Advertising ID (AAID) for devices is an Android provided ID to track the users with their consent for advertising purposes by the publishers who have an app on the Google Play Store. An API is introduced in Xandr mobile SDK to enable or disable AAID usage by including or excluding the AAID field in the ad request.

| Function | Description |
|--|--|
| `void disableAAIDUsage(boolean disable)` | Method to enable/disable the disableAAIDUsage. Default value is false. |

### Example

#### [Java](#tab/java7)

```
// To Set the disableAAIDUsage
SDKSettings.disableAAIDUsage(false);
// To Get the disableAAIDUsage status
SDKSettings.isAAIDUsageDisabled()
```

#### [Kotlin](#tab/kotlin7)

```
// To Set the disableAAIDUsage
SDKSettings.disableAAIDUsage(false)
// To Get the disableAAIDUsage status
SDKSettings.isAAIDUsageDisabled()
```

---

## Set the auction timeout

| Function | Description |
|--|--|
| `void setAuctionTimeout(long auctionTimeout)` | Defines the timeout period, in milliseconds, to wait for a bidder to respond to a bid request. <br><br> If the bidder fails to respond within the value set for the timeout period (for example, 500 milliseconds), the bid request would result in failure. |

### Example

#### [Java](#tab/java8)

```
SDKSettings.setAuctionTimeout(500)
```

#### [Kotlin](#tab/kotlin8)

```
SDKSettings.setAuctionTimeout(500)
```

---

## Set test mode

| Function | Description |
|--|--|
| `void enableTestMode(Boolean enabled)` | Sets true or false for the AdRequests to be executed in the test mode for debugging or testing. Default value is false. <br><br> **Note**: The scope of setting the test mode for AdRequest execution as true is limited to debugging/development or testing purpose only, and not to be used in a production environment. Enabling the test mode in a production environment leads to unintended consequences and impacts the monetization of your app. |

### Example

#### [Java](#tab/java9)

```
SDKSettings.enableTestMode(true);
```

#### [Kotlin](#tab/kotlin9)

```
SDKSettings.enableTestMode(true)
```

---

## Set content language

| Function | Description |
|--|--|
| `void setContentLanguage(String contentLanguage)` | Sets the two-letter ANSI code for the content's language; for example, `EN`. |

### Example

#### [Java](#tab/java10)

```
SDKSettings.setContentLanguage("EN")
```

#### [Kotlin](#tab/kotlin10)

```
SDKSettings.setContentLanguage("EN")
```

---
