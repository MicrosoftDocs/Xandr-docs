---
title: Xandr Mobile SDKs
description: Learn Xandr's Mobile SDKs streamline app monetization with open-source code, extensive documentation, MRAID 2.0 support, and efficient mediation options.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Overview: Xandr mobile SDKs

Xandr's Mobile SDKs give app developers a fast, convenient way to monetize their apps.

## Features of the mobile SDK

<!-- - Open-source code (including release notes) available on [GitHub](https://github.com/appnexus). -->
<!-- - [Support forum](https://groups.google.com/forum/#%21forum/appnexussdk) for direct engineering support. -->
<!-- - Dedicated [Android](https://play.google.com/store/apps/details?id=com.appnexus.opensdkapp) and [iOS](https://itunes.apple.com/us/app/appnexus-sdk-app/id736869833?mt=8) apps integrate the SDK and allow you to test your campaigns and creatives in real environments. -->
- Extensive documentation.
- Complete support of [MRAID 2.0](https://www.iab.com/guidelines/mobile-rich-media-ad-interface-definitions-mraid/) for rich media creatives.
- Mediation is managed by the network through Xandr, removing the burden from the publisher.
- SDK can mediate or be mediated by any other SDK with mediation capabilities.
- Pre-built adaptors for mediating third party SDKs.
- Rapid integration.

## Supported creative formats

- Banners
- Interstitials
- Rich media ads using MRAID can serve on banners or interstitials
- Video ads using MRAID can serve on interstitials
- Native
- Vast Video

## Getting started

- Android: [Android SDK Integration](android-sdk-integration-instructions.md)
- iOS: [iOS SDK Integration](ios-sdk-integration-instructions.md)

## Ad types

| Platform | Ad Types                                                                                                            |
|----------|---------------------------------------------------------------------------------------------------------------------|
| Android  | - [Show Banners](show-banners-on-android.md) <br> - [Show Interstitials](show-interstitials-on-android.md) <br> - [Show Banner Video/OutStream Ads on Android](show-banner-video-outstream-ads-on-android.md) <br> - [Show Native Ads](show-native-ads-on-android.md) <br> - [Show Banner Native](show-banner-native-on-android.md) <br> - [Show Instream Video](show-instream-video-ads-on-android.md) |
| iOS      | - [Show Banners](show-banners-on-ios.md)<br> - [Show Interstitials](show-interstitials-ads-on-ios.md)<br> - [Show Banner Video/OutStream Ads on iOS](show-multi-format-banner-ads-on-ios.md)<br> - [Show Native Ads](show-native-ads-on-ios.md)<br> - [Show Banner Native](show-banner-native-on-ios.md)<br> - [Show Instream Video](show-instream-video-ads-on-ios.md) |

## Targeting

| Platform | Targeting                                                        |
|----------|------------------------------------------------------------------|
| Android  | - [Add Targeting Parameters](add-targeting-parameters-on-android.md)<br> - [Pass Custom Keywords](pass-custom-keywords-on-android.md)<br> - [Set Reserve Prices](set-reserve-prices-on-android.md) |
| iOS      | - [Add Targeting Parameters](add-targeting-parameters-on-ios.md)<br> - [Pass Custom Keywords](pass-custom-keywords-on-ios.md)<br> - [Set Reserve Prices](set-reserve-prices-on-ios.md) |

## Mediation

| Platform | Targeting                                                     |
|----------|---------------------------------------------------------------|
| Android  | - [Mediate with Android SDK Instructions](mediate-with-android-sdk-instructions.md)<br> - [Android Custom Adaptors](android-custom-adaptors.md) |
| iOS      | - [Mediate with iOS](mediate-with-ios.md)<br> - [iOS Custom Adaptors](ios-custom-adaptors.md)                          |

## Configuration

| Platform | Configuration |
|----------|---------------|
| Android | - [Allow Multiple Ad Sizes to Serve into a Banner Ad View](allow-multiple-ad-sizes-to-serve-into-a-banner-ad-view-on-android.md)<br> - [Add a Transition Animation](add-a-transition-animation-on-android.md)<br> - [ANJAM User Guide](anjam-user-guide.md)<br> - [Configure SDK Logging](configure-sdk-logging-on-android.md)<br> - [Control Ad Unit Alignment](control-ad-unit-alignment-on-android.md)<br> - [Control Landing Page Loading Visibility](control-landing-page-load-visibility-on-android.md)<br> - [Control Location Accuracy](location-controls-on-android.md)<br> - [Customize Video Player Options](customize-video-player-options-on-android.md)<br> - [Dismiss Interstitials on User Click](dismiss-interstitials-on-user-click.md)<br> - [Show Banner Video/OutStream Ads on Android](show-banner-video-outstream-ads-on-android.md)<br> - [Open Ad Clicks in the Native Browser](open-ad-clicks-in-the-native-browser-on-android.md)<br> - [Toggle PSAs](toggle-psas-on-android.md)<br> - [Receive Ad View Status Events](receive-ad-view-status-events-on-android.md)<br> - [Resize Ads to fit the Screen or Banner Ad View](resize-ads-to-fit-the-screen-or-banner-ad-view-on-android.md)<br> - [Resize the Banner Ad View to the Size of the Winning Creative](resize-the-banner-ad-view-to-the-size-of-the-winning-creative-on-android.md)<br> - [Request Ads over HTTPS](request-ads-over-https-on-android.md) | 
| iOS | - [Allow Multiple Ad Sizes to Serve into a Banner Ad View](allow-multiple-ad-sizes-to-serve-into-a-banner-ad-view-on-ios.md)<br> - [Add a Transition Animation](add-a-transition-animation-on-ios.md)<br> - [ANJAM User Guide](anjam-user-guide.md)<br> - [Configure SDK Logging](configure-sdk-logging-on-ios.md)<br> - [Control Ad Unit Alignment](control-ad-unit-alignment-on-ios.md)<br> -  [Control Landing Page Loading Visibility](control-landing-page-load-visibility-on-ios.md)<br> - [Control Location Accuracy](location-controls-on-ios.md)<br> - [Customize Video Player Options](configure-video-player-options-on-ios.md)<br> - [Multi-Format Banner and Video Ad Support](show-multi-format-banner-ads-on-ios.md)<br> - [Open Ad Clicks in the Native Browser](open-ad-clicks-in-the-native-browser-on-ios.md)<br> - [Toggle PSAs](toggle-psas-on-ios.md)<br> - [Receive Ad View Status Events](receive-ad-view-status-events-on-ios.md)<br> - [Resize Ads to fit the Screen or Banner Ad View](resize-ads-to-fit-the-screen-or-banner-ad-view-on-ios.md)<br> - [Resize the Banner Ad View to the Size of the Winning Creative](resize-the-banner-ad-view-to-the-size-of-the-winning-creative-on-ios.md)<br> - [Request Ads over HTTPS](request-ads-over-https-on-ios.md) |

## Impression tracking

[Mobile SDK: Impression Counting Methods](impression-counting-methods.md)

<!-- ## Apps
[Xandr SDK App](xandr-sdk-app.md) -->

## Ad ops guides

- [Ad Ops - Set up Static Image Banners](ad-ops-set-up-static-image-banners.md)
- [Ad Ops - Set Up HTML Responsive Interstitials(non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)
- [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
- [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)

## Support

The [Xandr Customer Support Portal](https://support.ads.microsoft.com) is for issues that must be addressed by our Support team.
Examples of issues that should be submitted to the [Xandr Customer Support Portal](https://support.ads.microsoft.com) include:

- Only PSAs are returned
- Incorrect ad quality settings for the publisher
- Creative delivery issues

## Licensing

All of Xandr Mobile SDK <!-- code --> is released under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)license. <!-- License information can be found in our Github repositories of [iOS](https://github.com/appnexus/mobile-sdk-ios) and [Android](https://github.com/appnexus/mobile-sdk-android) SDK. -->

Third-party components are included in Xandr Mobile SDKS under the licenses specified by their respective authors. For information about these licenses, refer to the source files in the Xandr Mobile SDK.
