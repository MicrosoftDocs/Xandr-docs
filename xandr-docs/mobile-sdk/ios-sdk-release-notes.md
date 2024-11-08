---
title: iOS SDK Release Notes
description: Explore information about the iOS SDK release notes.
ms.custom: ios-sdk
---

# iOS SDK release notes

<!-- [!NOTE]
> Please visit [https://github.com/appnexus/mobile-sdk-ios/releases](https://github.com/appnexus/mobile-sdk-ios/releases)for our most recent release notes for iOS SDK.-->

## 9.2.0

### Improvement/Bug Fixes

- 8196240: Added support for [Global Placement ID (GPID)](ios-sdk-code-samples-set-gpid.md).
- 8191691: Addressed several memory leaks.

## 9.1.1

### Improvement/Bug Fixes

- 8213496: Resolved issues causing crashes in AdFetcher when utilizing MultiAdRequest.
- 8235734: Fixed an issue where both adDidReceivedAd and adDidReceiveNativeAd callbacks were triggered for Banner Native ads.

## 9.1.0

### New feature

- 7601090: Support for VAST Video Ads in Interstitial Ad Unit.

### Improvement/Bug fixes

- 7931257: ANSDKResources.bundle causing Unexpected CFBundleExecutable Key issue during AppStore upload.
- 7905366: Warnings as Errors causes build failure in Swift.
- 6525343: Can't import Google mediation adapter classes when using Swift Package Manager + Swift.
- 8098254: Upgrade of the Facebook Audience Network to version 6.15.1.
- 8082032: Addressed crash where adWillClose is required for interstitial banner.
- 8179513: Addresses an issue with Banner Video displaying black in iOS18.
- 8202865: Updated SmartAdServer dependency to 7.24.2.

## 9.0.0

> [!NOTE]
> As of v9.0.0 release, the source code is moved to private repositories as already announced. You can refer to the [migration guide](migrating-ios-sdk-v8.x.y-to-v9.x.y.md) to understand how to utilize the binary framework.

### New feature

- 5736950: Made our webview inspectable when log level is set to debug or higher.

### Improvement/Bug fixes

- 746525343: Fixed Google Adapter Bug - Accessing Files.
- 6892506: Fixed drop in (OMID) viewability events.
- 6891512: Fixed Cocoapod integration in Flutter environment.

## 8.11.4

### Improvement/Bug fixes

- 7295371: Privacy Manifest update and fixed issues with Cocoapods for [privacy manifest files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files?language=swift).

## 8.11.3

### Improvement/Bug fixes

- 7295362: Privacy Manifest update.

## 8.11.2

### Improvement/Bug fixes

- 7112599: Fixed issues with Cocoapods for [privacy manifest files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files?language=swift).

## 8.11.1

### Improvement/Bug fixes

- 5663009: Added support for [privacy manifest files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files?language=swift).

### Mediation partner updates

- 7151757: Upgrade of the Facebook Audience Network to version 6.15.0.
- 7151765: Upgraded Google AdMob SDK from 10.10.0 to 11.2.0.

## 8.11.0

### Announcement

This marks the final minor release within SDK v8.x. Looking ahead, SDK v9.0.0 will be our next major release. As previously announced, we will discontinue the practice of releasing source code updates for iOS and Android Mobile SDKs on Github. It's important to note that this is not a deprecation of our SDKs; rather, it pertains to the open-source aspect as we transition our Android and iOS Mobile SDKs to private repositories. There will be no disruptive changes from v8.x to v9.0.0, although it's worth noting that any future functional enhancements will be exclusively developed within the v9.x series.

### New feature

- 6273926 - [Support for Digital Services Act (DSA)](sdk-privacy-for-ios.md)

## 8.10.0

### New feature

- 6029394 - Added support for setting content language in Ad Request. New API introduced in SDKSettings setContentLanguage(String contentLanguage).

### Improvement/Bug fixes

- 6015112: Upgraded OMSDK from 1.4.8 to 1.4.9 (Microsoft namespace).
- 5766029: Resolve the issue with the OutStream iPad video of size 400x980 not rendering properly.
- 5992098: Optimise user agent synchronisation to minimise delays Mediation partner updates MS-5392 Upgrade of the Facebook Audience Network to version 6.14.0.

## 8.9.0

### Improvement/Bug fixes

- 5663106: Upgraded OMSDK from 1.4.2 to 1.4.8.
- 5732707: Addressed issue with Video Orientation Sizes getting applied to HTML Banner creatives.

### Mediation partner updates

- 5622329: Upgraded Google AdMob SDK from 10.3.0 to 10.10.0.
- 5622334: Upgraded Smart Ad Server SDK from 7.17.1 to 7.22.0.

## 8.8.1

### Improvement/Bug fixes (8.8.1)

- MS-5384: Addressed issue while installing SDK via Swift Package Manager.
- MS-5385: Addressed issue while installing SDK via Cocoapods.

## 8.8.0

### New features (8.8.0)

- MS-5345: Enabled lazy loading for banner native rendering.
- MS-5351: Support both static and dynamic AppNexus SDK framework/library.

### Improvement/Bug fixes (8.8.0)

- MS-5348: Addressed issue where creative failed to render when scrolled in a collection view.
- MS-5266: Addressed issue where impression tracker did not fire when creative is scrolled in a collection view.

## 8.7.0

### Improvement/Bug fixes (8.7.0)

- MS-5346: Fixed issue where only last ad is rendered in a multi ad request for Banner Native Rendering.
- MS-5206: Added support for setting player size and getting video creative width and height for BannerVideo. New API introduced in ANBannerAdView landscapeBannerVideoPlayerSize, portraitBannerVideoPlayerSize, squareBannerVideoPlayerSize, getVideoWidth, getVideoHeight and In ANVideoAdPlayer getVideoWidth and getVideoHeight.
- MS-5344: Gracefully handle error to avoid crash during fetch User agent String.
- MS-5340: Fixed ModuleMap XCFramework Warning.

## 8.6.0

### Improvement/Bug fixes (8.6.0)

- MS-5281: Added Swift Package Manager support for Google Mediation Adapter.

### Mediation/CSR partner updates

- Upgraded Google AdMob SDK from 9.14.0 to 10.3.0.

## 8.5.0

### Improvement/Bug fixes (8.5.0)

- MS-5227: Fixed issue with loading multiple outstream video ads simultaneously.

## 8.4.0

Update version to match Android SDK. No changes from 8.3.0.

## 8.3.0

### Improvement/Bug fixes (8.3.0)

- MS-5208, MS-5214: Upgraded OMSDK from 1.3.31 to 1.4.2.
- MS-5197: Added iPad multiwindow support for Google AdMob mediation. For more information, see [Mediate with iOS](mediate-with-ios.md).

### Mediation/CSR partner updates (8.3.0)

- MS-5210, MS-5213: Upgraded Google AdMob SDK from 9.4.0 to 9.14.0.

## 8.2.0

### Improvement/Bug fixes (8.2.0)

- MS-5172: Support for Global Privacy Platform (GPP) ([SDK Privacy for iOS](sdk-privacy-for-ios.md)).
- MS-5112: Update PPID API to indicate if it is first party ID ([User ID(s) Mapping on iOS](user-id-s-mapping-on-ios.md)).
- MS-5183: Fixed Completion handler callback issues in XandrAd.init().

### Mediation/CSR partner updates (8.2.0)

- MS-5195: Upgraded Facebook Audience Network SDK from 6.5.0 to 6.12.0.

## 8.1.1

### Improvement/Bug fixes for macOS SDK (8.1.1)

- MS-5127: Added Impression tracking API for NSView registerViewTracking.
- MS-5128: Code optimizations.
- MS-5149: Fixed Impression tracking issue when app is on secondary displays.

## 8.1.0

### New feature (8.1.0)

- MS-5102: Added a new MacOS Target supporting Native Ad's.

### Improvement/Bug fixes (8.1.0)

- MS-5080: Enable support for high impact media type creatives in BannerAdView.
- MS-5108: Added localization configuration option for SDK browser dismiss button "OK" (Github PR #80).

## 8.0.0

### Announcements

We have completed the removal of the APIs referenced in the 7.21.0 release. Note that there are breaking changes to some of our APIs, particularly for our init methods which is required for ad calls to be successful-[[XandrAd sharedInstance] initWithMemberID:1 preCacheRequestObjects:true completionHandler:nil];. For further details, see our [8.0 integration guide](ios-sdk-integration-instructions.md), as well as our [SDK initialization guide](ios-sdk-initialization-v8-0.md).

### Improvement/Bug fixes (8.0.0)

- MS-5011: Updated impression counting methodology. See our new [Impression Counting Methodology Guide](updated-impression-counting-mechanism-mobile-sdk-v8-0-and-above.md).
- MS-4978: Fixed custom adapter issues in Swift. (Github Issue #71).
- MS-5007: Removed all discontinued mediation adapters.
- MS-5013: Upgraded to OMSDK v1.3.31.

## 7.22.0

### Announcements (7.22.0)

This will be the last major release in SDK v7.x.x series.

The next major release will be SDK v8.0.0 which will include some breaking changes as proposed in Intent to Implement's listed below along with other changes.

1. Xandr SDK v8.0.0 Removal Notice for Deprecated APIs ([Github Issue #77](https://github.com/appnexus/mobile-sdk-ios/issues/77)).
1. Xandr will be moving toward counting "Viewable Impressions - for Direct-Sold Inventory" ([Github Issue #79](https://github.com/appnexus/mobile-sdk-ios/issues/79)).

### Improvement/Bug fixes (7.22.0)

- MS-4389: Fixed ads render after expiry time reset issue.
- MS-4999: Remove the RendererID deprecation notice.
- MS-5005: Added onAdImpression callback for the Banner and Interstitial Ads ([iOS SDK Ad Units](ios-sdk-ad-units.md)).

### Mediation partner updates (7.22.0)

- MS-4874: Upgraded Google Play Services Ads SDK from 8.5.0 to 9.4.1.
- MS-4873: Upgraded Smart Ad Server SDK from 7.10.1 to 7.17.1.
- Discontinued support for Facebook SDK mediation Adapter.

## 7.21.0

### Announcements (7.21.0)

We intend to remove all the deprecated API's listed below in Xandr SDK v8.0. If you are using any of the below API's, we request to migrate to their supported equivalent. If you have any questions reach out to [Xandr support](https://help.xandr.com/s/login/).

| Class | Property(s) and Method(s) |
|--|--|
| ANBannerAdView | **Property**: externalUid, adType, nativeAdRendererId, creativeId <br> **Method**: (void)setAllowNativeDemand:(BOOL)nativeDemand withRendererId:(NSInteger)rendererId; |
| ANInterstitialAd | **Property**: externalUid, adType, creativeId |
| ANInstreamVideoAd | **Property**: externalUid, adType, creativeId |
| ANMultiAdRequest | **Property**: externalUid, adType, creativeId |
| ANExternalUserId | **Property**: source, userId <br> **Method**: (nullable instancetype)initWithSource:(ANExternalUserIdSource)source userId:(nonnull NSString *)userId; |
| ANNativeAdRequest | **Property**: rendererId, adType, externalUid |
| ANNativeAdResponse | **Property**: creativeId |
| ANSDKSettings | **Property**: HTTPSEnabled, externalUserIdArray, useAdnxsSimpleDomain |
| ANTargetingParameters | **Property**: externalUid |

### Improvement/Bug fixes (7.21.0)

- MS-4954: Added support for passing Publisher/Extended User Id(s) via ANSDKSettings.userIdArray. ([User ID(s) Mapping on iOS](user-id-s-mapping-on-ios.md)).

### Deprecated APIs

`ANSDKSettings.externalUserIdArray` property and `ANExternalUserId` class are now deprecated, use the equivalent `ANSDKSettings.userIdArray` property and `ANUserId` class instead.

## 7.20.0

### Improvement/Bug fixes (7.20.0)

- MS-4952: Check navigationType when opening a URL (Github PR #73).
- MS-4851: Improved OMSDK performance.

## 7.19.0

### Improvement/Bug fixes 7.19.0

- MS-4884: Improved impression tracking methodology for Native Ads, trackers to be fired on render.

## 7.18.0

### New features (7.18.0)

- MS-4710: Make bid price available as part of AdResponseInfo ([Ad Response Info Class for iOS](ad-response-info-class-for-ios.md)).
- MS-4759: Automatically pass Identifier for Vendors (IDFV) in Ad request. ([Set IDFA usage for iOS](set-idfa-usage-for-ios.md)).

## 7.17.0

### New features (7.17.0)

- MS-4839: TTL SDK expiry listener logic for Index Exchange.
- MS-4841: TTL SDK expiry listener logic for InMobi.

### Bug fixes (7.17.0)

- MS-4849: Use retain instead of assign (Github #69).
- MS-4828: Memory leak related to 1 pixel tracking.

## 7.16.0

### Bug fixes/changes (7.16.0)

#### Fixed

- MS-4820: SDK version warning for Swift Package Manager (Github #68).

#### Changed

- MS-4802: ANSDKSettings.optionalSDKInitialization API ([Initialize SDK Settings in iOS](initialize-sdk-settings-in-ios.md)).

## 7.15.1

### Improvements/Bug fixes (7.15.1)

- MS-4818: Fixed Swift package manager installation error (Github issue #67).

## 7.15

### New feature (7.15)

- MS-4749: Added support for Unified ID 2.0 (UID2) ([User ID(s) Mapping on iOS](user-id-s-mapping-on-ios.md)).
- MS-4760: Added support for Google Additional Consent field.
- MS-4772: Added a new API in ANMultiAdRequest to stop the Ad Request ([Multi Ad Request for iOS](multi-ad-request-for-ios.md)).
- MS-4558: Added support for Swift Package Manager for SDK integration ([iOS SDK Integration Instructions](ios-sdk-integration-instructions.md)).
- MS-4784: Added XCFramework support for SDK integration ([iOS SDK Integration Instructions](ios-sdk-integration-instructions.md)).

### Mediation partner updates (7.15)

- MS-4778: Upgraded Google Play Services Ads SDK from 8.0.0 to 8.5.0.
- MS-4780: Upgraded Facebook SDK from 6.2.1 to 6.5.0.
- MS-4782: Upgraded Smart Ad Server SDK from 7.8.0 to 7.10.1.

### Improvements/Bug fixes (7.15)

- MS-4766: Updated Open Measurement SDK to v1.3.20.
- MS-4777: Added initialization check before fetching Bidder Token from Facebook SDK ([Get Facebook Demand for Native on iOS](get-facebook-demand-for-native-on-ios.md)).

## 7.14

### New feature (7.14)

- MS-4761: Added a new API to enable subscription to SDK logs for debugging/troubleshooting purposes. ([Configure SDK Logging on iOS](configure-sdk-logging-on-ios.md)).
- MS-4711: Exposed API in Custom element to support clickUrl and clickFallbackUrl for Native Ad. ([Show Native Ads on iOS](show-native-ads-on-ios.md)).

### Improvements/Bug fixes (7.14)

- MS-4753: Resolved a stability issue in Interstitial Ad due to `UIApplication.windows` being nil during Application launch.
- MS-4769: Removed duplicate calls to dispatch_async function from a couple of places.

## 7.13

### New feature (7.13)

- MS-4693: Added support for Cookieless domain requests.
- MS-4618: Fixed issue where the OMID SDK was causing high CPU usage for certain Ad formats - Github issue #57.

## 7.12

### Improvements/Bug fixes (7.12)

- MS-4719: Disabled autoplay for HTML5 Banner Video Ads.
- MS-4731: Fixed issue with OutStream Video that was preventing videos from playing.
- MS-4730: Fixed issue with OMID Tracker not firing for BannerAds in some cases.
- MS-4704: Added support for OMID containerGeometry and onScreenContainerGeometry for Instream & OutStream Video Ads.
- MS-4727: Added support for custom assets in Native Assembly Renderer.
- MS-4729: Removed strong reference on views to avoid cyclic reference for NativeAds.

## 7.11

### Improvements/Bug fixes (7.11)

- MS-4714: Added improvement for Ad Expiry events for Native Ads.
- MS-4685: Added API to disable tracking cookies during auction.
- (Github PR #61): Fixed race condition where ads load blank occasionally.

### Mediation partner updates (7.11)

- MS-4656: Upgraded Google AdMob SDK from v7.69.0 to v8.0.0.

## 7.10

### New feature (7.10)

- MS-4659, MS-4674: Added support for User ID from external sources(Criteo, NetID, LiverRamp, The Trade Desk) ([User ID(s) Mapping on iOS](user-id-s-mapping-on-ios.md)).
- MS-4657: Changes to support AppTrackingTransparency ([iOS 14.0 FAQ](ios-14-0-faq.md)).

### Improvements/Bug fixes (7.10)

- MS-4671: Added minimum threshold of 100ms for callSetMraidRefreshFrequency.

### Deprecated API

- externalUid property in ANAdProtocol has been deprecated, use publisherUserId in ANSDKSettings instead ([Publisher ID for iOS](publisher-id-for-ios.md)).

## 7.9

### New feature (7.9)

- MS-4388: Support to disable passing device IDs in bid requests.

### Mediation partner updates (7.9)

- MS-4663: Upgraded Google AdMob SDK from v7.67.0 to v7.69.0.
- MS-4664: Upgraded Facebook SDK from v6.2.0 to v6.2.1.

### Improvements/Bug fixes (7.9)

- MS-3911: Fetch SDK Version Dynamically in ad request.
- MS-4633: Moved User-Agent/WebView caching from load() to ANSDKSettings.optionalSDKInitialization().

## 7.8

### New feature (7.8)

- MS-4387: Added support to pass traffic source and external inventory codes in Ad Request ([Support to Pass Traffic Source and External Inventory Codes in Ad Request for iOS](support-to-pass-traffic-source-and-external-inventory-codes-in-ad-request-for-ios.md)).
- MS-4517: Added support for overriding Country and Zip Codes ([Support for Overriding Country and Zip Codes for iOS](support-for-overriding-country-and-zip-codes-for-ios.md)).

### Mediation partner updates (7.8)

- MS-4426: Upgraded Facebook SDK to v6.2.0.
- MS-4499: Upgraded SmartAd Server SDK to v7.8.0.
- MS-4498: Upgraded Google AdMob SDK to v7.67.0.

### Improvements/Bug fixes

- MS-4557: Resolved issue with BannerAd not rendering on the first load.
- MS-4587: Fixed issue with OMID sessionFinish event not being returned for Native ads.

## 7.7.1

### Improvements/Bug fixes (7.7.1)

- MS-4573: Fixed banner refresh on Lazyload.
- MS-4574: Add support for Cocoapods version 1.10.0.

## 7.7

### New feature (7.7)

- MS-4412: Added support for listening to Ad Expiry events for Native Ads ([Listener for AdAboutToExpire on iOS](listener-for-adabouttoexpire-on-ios.md)).
- MS-4449: Added support for setting test flags to bypass request filtering (for testing purposes only) ([Set Test Mode for iOS](set-test-mode-for-ios.md)).
- MS-4459: AuctionId information is now available through AdResponseInfo class.

### Mediation partner updates (7.7)

- MS-4426: Upgraded Facebook SDK to v6.0.0.
- MS-4499: Upgraded SmartAd Server SDK to v7.6.2.
- MS-4498: Upgraded Google AdMob SDK to v7.66.0.
- MS-4418: Discontinued support for Amazon, inMobi, Millennial Media and Mopub adapters. (Github Intent to Implement #53).

### Improvements/Bug fixes (7.7)

- MS-4550: Updated GDPR logic. Now priority will be given to IAB TCF2.0 strings.
- MS-4543: Fixed scrolling for Native Assembly WebView.
- MS-4522: Fixed caching issues with ANAdvertisingIdentifier. Now it will be fetched for every single request.

## 7.6.2

### New feature (7.6.2)

- MS-4433: Support for determining app-tracking permission status based on trackingAuthorizationStatus enum values (authorized, denied) ([iOS 14.0 FAQ](ios-14-0-faq.md)).

### Improvements/Bug fixes (7.6.2)

- MS-4523: Changed sizesThatShouldConstrainToSuperview to a block (Github #54).

## 7.6.1

### Improvements/Bug fixes (7.6.1)

- MS-4520: Rollback iOS 14 AppTrackingTransparency changes. For the latest updates on Xandr Mobile SDK's support for iOS 14, see [iOS 14.0 FAQ](ios-14-0-faq.md).

## 7.6

### New features (7.6)

- MS-4433: Support for iOS 14 ([iOS 14.0 FAQ](ios-14-0-faq.md)).
- MS-4268: Support for Open Measurement SDK Open RTB Signals.
- MS-4473: Added support for forcing the creative ID in Ad request for test/debug purposes.
- MS-4361: Added onAdImpression callback for the Native Ads ([Listen to Native Ad Events on iOS](listen-to-native-ad-events-on-ios.md)).

### Mediation partner upgrade

- MS-4497: Upgraded Google AdMob SDK to v7.64.0.

### Improvements/Bug fixes (7.6)

- MS-4362: Ad ResultCode is now a class instead of enum - this fixes issue with result codes getting overridden for concurrent Ad requests.

## 7.5

### New feature (7.5)

- MS-4384: Added support for Auction timeout ([Set the Auction Timeout for iOS](set-the-auction-timeout-for-ios.md)).

### Mediation partner upgrade (7.5)

- MS-4450 : Updated FacebookAd SDK to v5.10.1.

### Improvements/Bug fixes (7.5)

- MS-4233: Updated Open Measurement SDK to v1.3.7.
- MS-4301: Minor performance tweaks to Banner Ad rendering.
- MS-4405: Fixed issue with NSHTTPCookieStorage being set based on purposeConsent value.

## 7.4.1

### Improvements/Bug fixes (7.4.1)

- MS-4435: Fixed crash when using TCF 2.0 purpose consent strings.
- MS-4437: Fixed cocoapods build for Facebook CSR Adapter.

## 7.4

### New feature (7.4)

- MS-4214: Added support for loading the Ad lazily ([Lazy Load for iOS](lazy-load-for-ios.md)).

### Mediation partner upgrade (7.4)

- FacebookAd SDK v5.9.0

### Improvements/Bug fixes (7.4)

- MS-4231: Added support to respect timeout set in Console.
- MS-4284: Implemented support for MRAID v3.0 audioVolumeChange event.
- MS-4290: Added support to get Custom Keywords in the JavaScript layer via ANJAM.
- MS-4319: Added support to disable Banner demand for BannerAdView.
- MS-4335: Improved Banner Ad performance.

## 7.3.2

### Improvements/Bug fixes (7.3.2)

- MS-4352: Fixed NSHTTPCookieStorage setting.

## 7.3.1

### Improvements/Bug fixes (7.3.1)

- MS-4326: Fix for ANMultiAdRequest crashes when UT Response is not received due to Internet connectivity issues/device being offline.

## 7.3

### New feature (7.3)

- MS-4266: Added API to support Friendly Obstruction for Open Measurement.
- MS-4223: Added Client Side Rendering for FB mediated Ads.

### Improvements/Bug fixes (7.3)

- MS-4275: Fixed BannerAd OMID session tracker firing.

## 7.2

### Improvements/Bug fixes (7.2)

- MS-4200: Support IAB Europe Transparency & Consent Framework v2.0.
- MS-4267: All network calls will be made only using secure endpoint.

## 7.1

### New feature (7.1)

- MS-3956: Added ANAdResponseInfo to return associated data with Ad response.

### Mediation partner upgrade (7.1)

- Google AdMob SDK v7.55.0

### Improvements/Bug fixes (7.1)

- MS-3882: Added option to include "publisher_id" in Ad request.
- MS-3896: Fixed bug on Interstitial Video Ad close feature.
- MS-4166: Fixed VideoAd OMID session tracker firing bug.

## 7.0

### New feature (7.0)

- MS-3885: Added support for Multi Ad Request (MAR) ([Multi Ad Request for iOS](multi-ad-request-for-ios.md)).

### Mediation partner upgrade (7.0)

- Smart Server SDK v7.3.0

### Improvements/Bug fixes (7.0)

- MS-4122: Fixed potential memory leak issue caused by improper deallocation of InstreamVideoAd object.
- MS-4094: Code clean up to fix issue with OMID SDK video implementation.

## 6.2

### New features (6.2)

- MS-4097: California Consumer Privacy Act (CCPA) Support ([SDK Privacy for iOS](sdk-privacy-for-ios.md)).

### Bug fixes (6.2)

- MS-4124: Special characters not rendering over native assembly.
- MS-4084: VideoAd Object not getting deallocated.
- MS-4095: Updated OMID partner name.

## 6.1.2

### Improvements/Bug fixes (6.1.2)

- MS-4092: Fix for SKStoreProductViewController crash on iOS 13.

## 6.1.1

### New features (6.1.1)

- MS-3923: Added new API to get SDK version.

### Improvements/Bug fixes (6.1.1)

- MS-4091: Improved DFP second price option.

## 6.1

### New features (6.1)

- MS-3983: Added new API to Pause/Resume VideoAd ([Show Instream Video Ads on iOS](show-instream-video-ads-on-ios.md)).
- MS-4057: Official release for iOS 13 support.

### Mediation partner upgrades (6.1)

- Smart Server SDK v7.2.
- FacebookAd SDK v5.5.1 (has breaking changes, look at [iOS Mediation](ios-mediation.md) for updated integration instruction).
- Google AdMob SDK v7.50.

### Improvements/Bug fixes (6.1)

- MS-3915, MS-3916: Improved Banner Ad performance.
- MS-3948: Removed AppNexusSDKResources.Bundle.
- MS-3951: Fixed open measurement geometry change events for VideoAd.
- MS-3976: Fixed escape character breaking VideoAd load.
- MS-3987: Upgraded to OMSDK v1.2.19.
- MS-4004: Fixed VideoAd's pause issue when application state changes.
- MS-4023: Removed usage of UIWebView.
- MS-4036: Fixed interstitial crash on orientation change if orientation not supported by host application (Github #47).

## 6.0

At Xandr we listen to our users' feedback to help us develop the products that provide the best solutions for their needs. Based on that feedback, we are proud to announce the release of v6.0, a major upgrade to our iOS Mobile SDK.

### Breaking changes

Some changes made in v6.0 are breaking and may require existing users who wish to upgrade from previous versions to follow our [migration guide](ios-mediation.md).

### New features (6.0)

#### Change to the directory structure

Notable changes include:

- BinaryProjects/ANSDK.xcodeproject has been renamed and moved to sdk/AppNexusSDK.xcodeproject.
- Mediation Adapter targets have been removed from AppNexusSDK.xcodeproject.
- ANSDK target has been removed from AppNexusSDK.xcodeproject.

#### Mediation adapters are now available only via our source or CocoaPods

This will enable publishers to select the mediation networks they need for their inventory strategies.

#### Third party mediation network libraries have been removed from code

Publishers integrating mediation via source will need to include the libraries themselves.

A list of supported versions of [third-party mediation networks](mediate-with-ios.md) is available in our public documentation.

### Upgrades

#### Mediation partner upgrades

- Mopub SDK v5.8.0
- InMobi SDK v7.3.1
- Google AdMob SDK v7.48.0
- Smart Server SDK v7.1.1

> [!WARNING]
> If you are currently using a static library version of AppNexus SDK(libANSDK.a) or a mediation adapter follow our [migration guide](ios-mediation.md).

## 6.0-Beta

> [!NOTE]
> This is a beta release of the AppNexus SDK, and will be open for feedback/comments for at least the next 14 days.

### New features (6.0-Beta)

- SDK-Lite(6.0-Beta) bring in changes to directory structure. Some notable changes include:
  - BinaryProjects/ANSDK.xcodeproject has been renamed and moved to sdk/AppNexusSDK.xcodeproject.
  - Mediation Adapter targets have been removed from AppNexusSDK.xcodeproject.
  - ANSDK target has been removed from AppNexusSDK.xcodeproject.

- Mediation adapters are now available only via source or CocoaPods.

This will enable publishers to select the mediation networks they need for their inventory strategies.

- Third Party Mediation Network Libraries have been removed from code. Publishers integrating mediation via source need to include the libraries themself.

A list of supported versions of [third-party mediation networks](mediate-with-ios.md) is available in the public documentation.

- If you are currently using Static Library version of AppNexus SDK(libANSDK.a) / Mediation adapter follow Migration Steps found [here](ios-mediation.md).

> [!NOTE]
> Cocoapods integration remains the same from v5.x:> 6.X so it has not been included as a part of Beta release. But will be available as a part of final release.

## 5.5.1

### New features (5.5.1)

- MS-3778: Added new API to get Video Orientation for BannerVideo and Video Ads.

### Mediation partner upgrades/changes

- Removed support for the following mediation Adapter:

  - AdColony SDK
  - AdMarvel SDK
  - Chartboost SDK
  - Vdopia SDK
  - Vungle SDK
  - Yahoo SDK

### Improvements/Bug fixes (5.5.1)

- MS-3902: Removed deprecated APIs.
- MS-3311: Improved Objective-C API Declarations for Swift compatibility.

## 5.4

### New features (5.4)

- MS-3730: Support Rendering for Banner Native ads.

### Mediation partner upgrades/changes (5.4)

- MS-3495: Upgraded Mopub framework to v5.6.0.

### Improvements/Bug fixes (5.4)

- MS-3873: Improved ExposureChange on scroll.
- MS-3194: Removed UIWebView support.
- MS-3798: Added new API to enable publishers to configure skip options for video player.
- Improved Open Measurement Event(Session Finish) for RTB ads.

## 5.3

### New features (5.3)

- MS-3789: Ability to customize Video Player Options.

### Mediation partner upgrades/changes (5.3)

- MS-3803: Upgraded Google AdMob adapter SDK v7.43.0.

### Improvement/Bug fixes (5.3)

- MS-3774: Improved Open Measurement Event (Session Finish) for BannerAds.
- MS-3712: Resize BannerAd API for Mediation ads.
- MS-3808: Removed videoAdDidClose method to prevent Video Player removal (Github #22).

## 5.2

### New features (5.2)

- MS-3720: Open Measurement SDK support for Native Ads.

## 5.1.2

### New features (5.1.2)

- Added new API for setting Custom User Agent.

## 5.1.1

### Mediation partner SDK upgrades/changes

- Upgraded Smart Server SDK v7.0.2.
- Made SmartAdAdapter Podspec to be dependent on Smart-Display-SDK Pods.

Known issue: Apps integrating Smart Adapter from Code/Binary need to remove i386 and x86_64 architectures in order to be able to push to appstore. Cocoapods integration will work as-is.

## 5.1

### New features (5.1)

- Support for Carthage using script : carthageAppNexusSDK.sh.

### Mediation partner SDK upgrades/changes (5.1)

- Updated Google AdMob adapter to support GADUnifiedNativeAd and GADMediaView requirements.
- Upgraded Smart Server SDK v7.0.

### Bug fixes

- MS-3695: Refactored loadAd and setAutoRefreshInterval: to provide a single code-path for requesting an ad.
- MS-3707: Fixed bug in how Open Measurement JavaScript is injected into creative html content.
- MS-3598, MS-3599: Fixed MRAID and Video Ads to respect Safe Area on Top notch devices when running in FullScreen/Expanded mode.

## 5.0.1

### Bug fix (5.0.1)

- Allow ANNativeAdRequest to download image assets in background (MS-3714).

## 5.0

### New features (5.0)

- Universal Tags version 3, including support for Native ad objects.
- Support for Native Video.
- Open Measurement SDK support for video ads (MS-3388).
- New delegate method allowing ANBannerAdView object to be paired with ANNativeAdResponse object upon successful load of native ad (MS-3596).

### Mediation partner upgrades/changes (5.0)

- Upgrade GoodleAds SDK v7.35.1.
- Remove support for Rubicon SDK (MS-3682).

### Bug fixes (5.0)

- Prevent crashes by preventing ANBannerAdView from loading when width or height are improperly configured (MS-3685).

## 4.12

### New features and bug fixes (4.12)

- MS-3606: Updated Smart Adapter to v6.10.
- MS-3495: Updated Google Play Ad Adapter (AdMob & DFP) to v7.35.1.
- MS-3633: Added new APIs that expose additional description (`desc2`) and main image size for Native Ads.
- MS-3439: Added the option to send content_url string in Google Mediation requests, use key: `content_url`.
- MS-3583: Ability to pass second_price value to Google DFP Banner Ads. Beta release - contact your Account Manager for more information about this feature.

Known Issue: Rubicon Mediation Adapter compatibility issues with iOS 12.0 - to be fixed in a future release.

## 4.11.1

### New features and bug fixes (4.11.1)

- MS-3527: Attempt to prevent crash in OMIDAppnexusScriptInjector by error checking all MobileSDK inputs and by serializing global properties shared between threads.
- MS-3461: Update logic to center video display when video player is expanded to fill the full screen of the device.

## 4.11

### New features and bug fixes (4.11)

- MS-3401: Added an API for enabling/disabling the location access to the creative.
- MS-3518: Updated the AppNexus GDPR constants to avoid namespace collisions with other SDKs implementing GDPR.
- MS-3323: Updated SDK Localization for In-app browser's "OK" Button.
- MS-3462: Fixed video completion tracker not firing consistently.
- MS-3406: Updated the Mobile Vast Player.

## 4.10

### New features and bug fixes (4.10)

- MS-3181: Allow ANInstreamVideoAd to be initialized with inventoryCode and memberId.
- MS-3409: Repair SDK build errors highlighted by Xcode 10beta4.
- MS-3324: Allow designation of arbitrary sizes to trigger full view constraints on banner ad instances.
- MS-3427: Update Banner Native such that mainImage and iconImage are never downloaded automatically.
- MS-3199: Add impression count API for Mediated Native creatives.
- MS-3444: Add API to restrict allowed media types for Banner Ad.

## 4.9

### New features (4.9)

- MS-3234: Open Measurement SDK Support for HTML Banner Ads.

## 4.8

### New features (4.8)

- MS-3083: Native for Banner Ad View.
- MS-3115: Function to set external user ID in the SDK for user syncing.
- MS-3279: Expose click through URL for banner, native, interstitial & video.

### Bug fixes (4.8)

- MS-3186: Incorrect logic in AdMob mediation code - iOS - native.

### Mediation partner updates (4.8)

- MS-3257: Update Facebook Audience Network SDK to latest version.
- MS-3075: Update inMobi client side adapter to support latest inMobi SDK.

### Versions of updated Mediation SDK

- InMobi 7.1.1
- FacebookSDK 4.28.1

## 4.7.1

### New features and bug fixes (4.7.1)

- MS-3227: GDPR support for SDK
- MS-3193: [iOS SDK] crash

## 4.6

### New features (4.6)

- MS-2113: Support autocollapse of interstitials.
- MS-3178: Implement exposureChange event.

## 4.5

### New features (4.5)

- Banner Video

## 4.4.2

### Bug fixes (4.4.2)

- MS-3200: Fixed ANLocalizations overriding parent app localizations.

## 4.4.1

### Bug fixes (4.4.1)

- MS-3197: Fixed a crash in Creative ID changeset.

## 4.4

### Updates (4.4)

- MS-2132: The in-app browser localisations added for different localisations (French, German, Spanish, Swedish, and Danish).
- MS-3096: Ability to get Creative ID in the SDK from response.
- MS-3187: iPhone X : WKWebView scrollView gets undesired insets fixed.

## 4.3

### Updates (4.3)

- MS-3142: App crashing on iOS 9 when tapping on Native Ad.
- MS-3060: Mobile SDK: Close Interstitial when it is clicked.
- MS-3087: iOS Pre-Roll Placement Video Completion Tracker Not Firing Consistently.
- VID-3227: Pre-roll video serving mid-roll.
- MS-3101: Update Rechability Code.
- MS-3170: SDK Crash.

## 4.2

### Updates (4.2)

- MS-3097: Instream Video new API's to provide info on the video creatives loaded & playing.

## 4.1

### Updates (4.1)

- AppNexusSDK will now support iOS 9.0 & above only.

### Bug fixes (4.1)

- MS-3085: Update SDK to respect safe area on iPhone X/iOS 11.
- MS-2985: `NSURLConnection` has deprecated methods that are currently in use by the AppNexus SDK.
- MS-2983: `MPMoviePlayerViewController` has been deprecated as per iOS 9 but is being used in ANMRAIDUtil.

## 4.0.1

### Bug fixes (4.0.1)

- Resolve CocoaPods build issues.

## 4.0

### New features (4.0)

- MS-2964: Replace usage of /mob with /ut in SDK.

### Bug fixes (4.0)

- MS-1891: Address Facebook SDK star rating deprecation.
- MS-2862: Support newly added standard fields on the native creative object.
- MS-2915: Send SDK version on /ut requests.
- MS-2931: Product Request: Allow device permissions on iOS to be disabled.
- MS-3077: Add better support for rotation on iOS.
- MS-3078: Add support for loading 1x1 creatives in a banner.
- (Github Issue #13): Stop using EKEventStore.

## 3.6

### Mediated SDKs

- Updated the following mediation adapters which were updated to support iOS 11:

  - AdMobSDK v7.24.1
  - MillenialMediaSDK v6.6.0
  - RubiconSDK v6.4.0
  - AmazonSDK v2.2.15.1
  - FacebookSDK v4.26.0

## 3.5.1

### Bug fixes and updates (3.5.1)

- Removed files related to AdColony Native Mediation. It is no longer supported.

## 3.5

### Bug fixes and updates (3.5)

- Instream video is only supported in iOS 9 and above.
- MS-3041: Allow to configure app access rights in SDK.

### Mediated SDKs (3.5)

- AdColony SDK v3.1.1

## 3.4

### Bug fixes and updates (3.4)

- MS-3026: Add support for about:srcdoc.

### Mediated SDKs (3.4)

- Facebook SDK v4.24.0

## 3.3

### Bug fixes and updates (3.3)

- MS-2828: VPAID support for Instream-Video.

## 3.2.1

### Bug fixes and updates (3.2.1)

- MS-3016: Fixed podspec configuration and fake framework import issue in Rubicon mediation adapter.

## 3.2

### Bug fixes and updates (3.2)

- Fixed AdMarvel banner ad misalignment.

### Mediated SDKs (3.2)

- Rubicon SDK v6.3.0

## 3.1.2

### Bug fixes (3.1.2)

- MS-2984: Video Rendering issue on iOS 10.3.

## 3.1

### Bug fixes and updates (3.1)

- MS-2630: Support for new sizes when mediating Facebook banners.
- MS-2853: Engineer ANJAM so that getCurrentPosition() get the position on-the-fly.
- MS-2954: Add Google adapter subspec to Cocoapods.
- PR-12: Integrate third party PR: Fix reachability leak.

#### Instream video ads

- Modify the parent controller that is being set to load the click through URL.
- Update the custom targeting params format.

## 3.0

### New features (3.0)

- Support for instream video.

### Bug fixes and updates (3.0)

- Remove iAd.
- Minimum supported iOS version is now v8.0.

## 2.14

### Mediated SDKs (2.14)

- AdMarvel v4.2.0
- Rubicon v6.1.0
- SmartAd Server v6.6
- Millenial Media v6.3.1
- AdMob v6.4.1

### Bug fixes (2.14)

- MS-2839: Fix Anjam and Sdk communication for creative served in iframe.
- MS-2856: Error building with Carthage.
- MS-2841: Add a "ping" feature to the SDK without anjam.js injection.

## RC 2.13.2

### Bug fixes (RC 2.13.2)

- MS-2212: Allow RTB banners to fit full screen. New BOOL property: shouldResizeAdToFitContainer.
- MS-2820: Support multiple sizes in SDK ad request.
- PR-10: Integrate third party PR: project and schema updates per Xcode 8.

## RC 2.13.1

- Expose ANAdAdapterMillennialMediaBase.h In ANSDKMillennialMediaAdapter Binary Target.
- Expose ANSDKSettings.h In ANSDK Binary Target.

## RC 2.13

### New features (RC 2.13)

- MS-2580: Added switch to enable HTTPS in SDK for calls made by the AppNexus SDK.

  - Currently, ad calls may not always be ATS compliant. The AppNexus ad server will be fully ATS compliant by the end of 2016 without the need for an SDK change.
  - Because the AppNexus SDK does not control ad calls made by mediated SDKs, ATS compliance for mediated SDKs is the responsibility of each respective vendor. As mediated SDKs become ATS compliant the AppNexus SDK will be upgraded to support them.
- MS-2584: Added static method to pass Nexage Site ID into Millennial SDK mediated adapter.

### Bug fixes (RC 2.13)

- MS-2664: Fixed click-through issue affecting some ads loading in WKWebView.
- MS-2227: Multiple values for a single key now supported for AppNexus ad serving.

### Mediated SDKs (RC 2.13)

- Amazon SDK v2.2.15
- AdColony SDK v2.6.2
- AdMob SDK v7.10.1
- Chartboost SDK v6.4.7
- Facebook SDK v4.15.0
- Millennial Media SDK v6.3.0
- MoPub SDK v4.9.0
- Vungle SDK v4.0.5
- Yahoo Flurry SDK v7.6.4

## RC 2.12.1

### Mediated SDKs (RC 2.12.1)

- Facebook SDK Version 4.14.0

## RC 2.12

### Bug fixes (RC 2.12)

- MS-2382: Allow numbers passed as strings in mraid.js resizeProperties & expandProperties.
- MS-2332: Load interstitial full-screen ads in a web view the size of the screen.
- Updated client testing endpoints to ib-test.adnxs.com.
- Load MRAID/ANJAM scripts only in main frame.
- Open default browser only for a new window navigation.

### Mediated SDKs (RC 2.12)

No change.

## RC 2.11

### New features (RC 2.11)

- MS-2211: Use WKWebView for the in-app browser on iOS 8+.
- MS-2214: Suppress user selection of ads.

### Bug fixes (RC 2.11)

- MS-2163: Schedule NSURLConnection of ANAdFetcher in the current run loop for mode NSRunLoopCommonModes.
- MS-2163: Fully load WKWebView in the background before sending the `[ANAdDelegate adDidReceiveAd]` callback.
- MS-2214: Allow the app user to dismiss the in-app App Store window even if the ad view which presented it has been deallocated.
- MS-2214: Disable video autoplay on iPhones running iOS 9 and below.

### Mediated SDKs (RC 2.11)

No change.

## RC 2.10

### New features (RC 2.10)

- MS-2251: Banner ads are rendered in a WKWebView instead of UIWebView in iOS 8+.
- MS-2307: Ability to traffic full-screen interstitial creatives.

MS-2316 contains the following mediated SDKs:

- AdMob SDK Version 7.8.1
- Facebook SDK Version 4.12.0
- Amazon SDK Version 2.2.14
- Millennial Media SDK Version 6.1.0
- MoPub SDK Version 4.6.0
- InMobi SDK Version 5.3.1
- VDOPIA Lightweight SDK v1.4
- Vungle SDK 3.2.1
- AdColony SDK 2.6.1
- Chartboost SDK 6.4.4
- Yahoo Flurry SDK 7.6.3

## RC 2.9

### New features (RC 2.9)

- MS-2031: AdMob Native Mediation.

### Bug fixes (RC 2.9)

- Improved behavior for ANJAM window listener.

MS-1913 contains the following mediated SDKs:

- AdMob SDK Version 7.6.0
- Facebook SDK Version 4.9.1
- Amazon SDK Version 2.2.13
- Millennial Media SDK Version 6.1
- MoPub SDK Version 4.1.0
- InMobi SDK Version 5.2.0
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.2.0
- AdColony SDK 2.6.1
- Chartboost SDK 6.2.1
- Yahoo Flurry SDK 7.3.0

## RC 2.8

### New features (RC 2.8)

- MS-1701: Added public API to support passing inventory code and member ID in lieu of placement ID.

MS-1712 contains the following mediated SDKs:

- AdMob SDK Version 7.5.2
- Amazon SDK Version 2.2.11
- Facebook SDK Version 4.8.0
- Millennial Media SDK Version 6.1.0
- MoPub SDK Version 4.1.0
- InMobi SDK Version 5.0.2
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.2.0
- AdColony SDK 2.6.0
- Chartboost SDK 6.0.1
- Yahoo Flurry SDK 7.3.0

### Known issues

- Amazon SDK 2.2.11 emits warnings in Xcode 7 of the following kind: "Warning: Could not resolve external type c:objc(cs)". These will be addressed in a subsequent release.

## ~~RC 2.7~~

## RC 2.6

### Bug fixes (RC 2.6)

- MS-1573: Improve how location is passed on a native ad request URL.

### Other changes (RC 2.6)

- MS-1389: Updated test project & sample app for Xcode 7 / iOS 9.
- MS-1389: Bitcode ANSDK binary can be built by running "./buildANSDK.sh -b".

MS-1654 contains the following mediated SDKs:

- AdMob SDK Version 7.5.1
- Amazon SDK Version 2.2.10
- Facebook SDK Version 4.7.0
- Millennial Media SDK Version 6.1.0
- MoPub SDK Version 3.11.0
- InMobi SDK Version 4.5.3
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.2.0
- AdColony SDK 2.6.0
- Chartboost SDK 5.5.3
- Yahoo Flurry SDK 7.2.1

## RC 2.5

### Bug fixes (RC 2.5)

- MS-1503: Fixed customEventInterstitialWillPresent call in ANGADCustomInterstitialAd.m.

### Other changes (RC 2.5)

- MS-1511: Xcode 7 / iOS 9 updates.
- MS-1371: Increase interstitial timeout to 4.5 minutes.

MS-1519 contains the following mediated SDKs:

- AdMob SDK Version 7.4.1
- Amazon SDK Version 2.2.10
- Facebook SDK Version 4.5.1
- Millennial Media SDK Version 6.0.1
- MoPub SDK Version 3.11.0
- InMobi SDK Version 4.5.3
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.1.2
- AdColony SDK 2.5.3
- Chartboost SDK 5.5.3
- Yahoo Flurry SDK 7.0.0

## RC 2.4

### Bug fixes (RC 2.4)

- MS-1365: Fix handling of custom keywords on ANNativeAdRequest.
- MS-1306: Improved handling of clickable elements for native ad views.
- MS-1331: Expose ANAdAdapterNativeInMobi header in binary output.

### Other changes/additions (RC 2.4)

- MS-1238: Added request, response notification broadcasts.
- MS-1366: Removed old ANGender enum values & banner resize callbacks.
- MS-1333: Improved Binary Build Script.

### New mediation adapters (RC 2.4)

- MS-1321: Yahoo Flurry Banner, Interstitial, Native.
- MS-1413: Millennial Banner, Interstitial (rewritten for MMAdSDK 6.0.1).

MS-1413 contains the following mediated SDKs:

- AdMob SDK Version 7.3.1
- Amazon SDK Version 2.2.8
- Facebook SDK Version 4.4.0
- Millennial Media SDK Version 6.0.1
- MoPub SDK Version 3.9.0
- InMobi SDK Version 4.5.3
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.1.2
- AdColony SDK 2.5.3
- Chartboost SDK 5.5.1
- Yahoo Flurry SDK 6.5.0

## RC 2.3.1

### Bug fixes (RC 2.3.1)

- MS-1317: Addressed iPad in-app browser compile issue.

## RC 2.3

### Bug fixes (RC 2.3)

- MS-1219: Removed OpenUDID dependency.
- MS-1265: Move location of kANAdFetcherDidReceiveResponseNotification.
- MS-1267: Testing improvements.

### New mediation adapters (RC 2.3)

- MS-1107: AdColony Native

Contains the following mediated SDKs:

- AdMob SDK Version 7.3.1
- Amazon SDK Version 2.2.8
- Facebook SDK Version 4.2.0
- Millennial Media SDK Version 5.4.1
- MoPub SDK Version 3.8.0
- InMobi SDK Version 4.5.3
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.0.13
- AdColony SDK 2.5.1
- Chartboost SDK 5.4.0

## RC 2.2

### Feature additions (RC 2.2)

- MS-910: Interstitials with transparent backgrounds now supported on iOS 8.
- MS-941: Enhanced user interaction detection on ad views.
- MS-982: Auto-detect a banner root view controller if one isn't provided.

### Bug fixes (RC 2.2)

- MS-882: Handle banner, interstitial, native invalid network detection separately.
- MS-970, MS-1038: Binary build scripts now work in directories where the file path contains one or more spaces.
- MS-971: Fixed native ad click fallback behavior.
- MS-1000: Fire adWillClose and adDidClose on ANInterstitialAd.

### Internal improvements (RC 2.2)

- MS-540: Add ANLogging support in ANMoPubMediationBanner & ANMoPubMediationInterstitial.
- MS-962: Simplify IDFA retrieval based on 6.0 deployment target.
- MS-976, MS-1042, MS-1055: Break apart ANAdResponse into ANAdServerResponse & ANAdFetcherResponse.
- MS-975: Improved AdFetcher error handling.
- MS-1022, MS-1054: Added AN namespace to all category methods.
- MS-1024: Removed ANBasicConfig.

### Mediation adapter bug fixes (RC 2.2)

- MS-963: Fix for isReady in Amazon interstitial adapter.
- MS-1113: Silence warning in Millennial adapters when compiling for iOS 8.3.
- MS-1186: Address deprecated methods in ANGADCustomBannerAd & ANGADCustomInterstitialAd from Google AdMob SDK 7.2.1.
- MS-1188: Simplify iAd adapters based on 6.0 deployment target.
- MS-1193: Improved error code handling for MoPub & Millennial adapters.

### New mediation adapters (RC 2.2)

- MS-942: InMobi Banner, Interstitial, Native
- MS-1045: AdColony Interstitial
- MS-1047: Vungle Interstitial
- MS-1048: VDOPIA Banner, Interstitial
- MS-1071: Chartboost Interstitial

Contains the following mediated SDKs:

- AdMob SDK Version 7.2.1
- Amazon SDK Version 2.2.6
- Facebook SDK Version 4.1.0
- Millennial Media SDK Version 5.4.1
- MoPub SDK Version 3.7.0
- InMobi SDK Version 4.5.1
- VDOPIA Lightweight SDK Version 4
- Vungle SDK 3.0.13
- AdColony SDK 2.5.0
- Chartboost SDK 5.2.1

## RC 2.1

- MS-856, MS-868, MS-875, MS-916, MS-918, MS-925: Implemented AppNexus Native Ad Console Support.
- MS-932: Introduced namespaced `ANGender` enum values (e.g. `ANGenderMale`). Deprecated existing values (e.g. `MALE`).
- Updated to meet MRAID 2.0 compliance standards.

### Other feature additions (RC 2.1)

- MS-868: Added dependency on StoreKit framework, App Store URLs will open directly in the app instead of opening in the AppStore app when `opensInNativeBrowser` is set to `NO` on the ad view.
- MS-900: Added dependency on EventKitUI framework, user will be presented with a calendar event edit screen if an ad calls `mraid.createCalendarEvent`.
- UIWebView performance enhancements.

### Bug fixes (RC 2.1)

- MS-888: Clear AmazonAdView delegate on dealloc.
- MS-902: Fixed malformed URL issue caused by mediated networks not present in app.
- MS-934: Allow background color for banner to be set from .nib file or storyboard.

Includes the following mediated network SDKs:

- Google SDK Version 7.0.0
- Amazon SDK Version 2.1.9
- Facebook SDK Version 3.23
- Millennial Media SDK Version 5.4.1
- MoPub SDK Version 3.4.0

> [!NOTE]
> The AdMob and DFP mediation adapters have been updated to work with the new framework distribution mechanism for the Google Ads SDK (in version 7.0.0).

## RC 1.21 (2.0)

- AppNexus Native API 1.0, with support for MoPub and Facebook mediation.

### Other bug fixes (RC 1.21 (2.0))

- ANLocation formatting on the ad call.
- KVO removeObserver exceptions.
- MRAID ad with custom close in expanded state did not correctly collapse back to default state.
- Improved importing of SDK bundle resources.

### 3rd party SDK updates

- AdMob 6.12.2
- Amazon 2.1.4
- Facebook 3.20
- MoPub 3.2.0

## RC 1.20

- `ANAdProtocol landingPageLoadsInBackground`: Controls the SDK's behavior when an ad is clicked. The default behavior (`YES`) is to load the landing page in the background until the initial payload finishes loading and then present a fully rendered page to the user. Setting this to `NO` will cause the in-app browser to immediately become visible and display the unrendered landing page. Note that setting this to `NO` when an ad redirects to the app store may cause the in-app browser to briefly flash on the screen.
- `ANAdProtocol setLocationWithLatitude:longitude:timestamp:horizontalAccuracy:precision:`: Provide a precision parameter when passing a user's location from a `CoreLocation` instance that will cause all location information to be internally rounded to the specified number of digits after the decimal before being passed to the ad server. The nominal resolution of digits after the decimal to distance is 2 digits to ~1 km, 3 digits to ~100m, 4 digits to ~10m. If set to -1, then full resolution is passed.
- `ANBannerView (ANBannerViewAdAlignment) alignment`: Overrides the alignment of the ad unit within the banner view, in the event the banner view frame is larger than the ad. The default alignment is `ANBannerViewAdAlignmentCenter`. Set this property to align the ad to the top left, top center, top right, center left, center right, bottom left, bottom center or bottom right.

### Other feature additions

- Amazon mediation adapters.
- Adopted Objective-C Modern Best Practices in Public APIs.
- Simple banner app.

### Bug fixes (RC 1.20)

- Removed support for DFP Swipeable Banner, a deprecated API.
- MRAID viewability timer reference set to strong.
- ANWebView delegate set to `nil` on dealloc.

### 3rd party SDK updates (RC 1.20)

- MoPub 3.0.0
- Amazon 2.1.2
- Google 6.12.0
- FB Audience Network 3.18.2
- Millennial Media 5.4.1

Minimum deployment target is iOS 6.0.

### Notes

To enable Amazon monetization, your app must register itself with Amazon when your application starts in your main app delegate:

```
#include "ANAdAdapterBaseAmazon.h"



...



[ANAdAdapterBaseAmazon setAmazonAppKey: "YOUR APP KEY"];
```
