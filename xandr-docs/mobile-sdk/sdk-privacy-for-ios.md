---
title: SDK Privacy for iOS
description: This page provides an overview on Global Privacy Platform (GPP), General Data Protection Regulations and California Consumer Protection Act.  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan

---

# SDK Privacy for iOS

Xandr's mobile SDKs include client support for Global Privacy Platform (GPP), the [General Data Protection Regulations](https://gdpr-info.eu/) (GDPR), and the [California Consumer Protection Act](https://oag.ca.gov/privacy/ccpa) (CCPA) and [Digital Services Act](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/europe-fit-digital-age/digital-services-act_en) (DSA).

The Global Privacy Platform (GPP) enables advertisers, publishers and technology vendors to adapt to regulatory demands across markets. GDPR provides regulations for the processing, movement, and protection of personal data within the European Union. CCPA creates new consumer rights relating to the access to, deletion of, and sharing of personal information that is collected by organizations. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

> [!WARNING]
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation. Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
>
> [!NOTE]
> Publishers are responsible for providing notice, transparency, and choice and for collecting consent from their users in accordance with the [Framework policies](https://iabeurope.eu/transparency-consent-framework/), either using their own Consent Management Provider or working with a vendor.
>
> - [Register your own CMP](https://register.consensu.org/CMP)
> - [List of registered CMPs](https://iabeurope.eu/cmp-list/)
>
> - Note our Service Policies (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.
> - All vendor SDKs (including mediation SDKs) are responsible for looking up approved vendor and consent information on their own; Xandr does not pass this information to these SDKs.

## General data protection regulations (GDPR)

In order for our clients to meet their transparency, notice and choice/consent requirements under the GDPR and the existing ePrivacy Directive, Xandr supports [the IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/)(the "Framework").

This is a reference for mobile app publishers using Xandr's Mobile SDK to surface notice, transparency and choice to end users located in the EEA and signal approved vendors and, where necessary, pass consent, to Xandr and demand sources and their vendors through the Xandr platform.

Xandr provides three APIs in the Mobile SDK for mobile app publishers to use the Framework. (These  APIs are available in Mobile SDK version 4.8+ for Android and 4.7.1+ for iOS.) These APIs allow you to:

- define whether the user is located in the European Economic Area (the "EEA") and that European privacy regulations should apply
- set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/commit/a32574941ce201708e30e78702278efe1ce6cd59)(IAB) consent string

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by [Mobile In-App CMP API v2.0: Transparency &amp; Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/README.md)) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

```
/** * Set the consentRequired value in the SDK
 *
 * @param true if subject to GDPR regulations, false otherwise
 */
 [ANGDPRSettings setConsentRequired:1];
      
/**
 * Set the consent string in the SDK
 *
 * @param A valid Base64 encode consent string as per https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework
 */
[ANGDPRSettings setConsentString:@"BOMyQRvOMyQRvABABBAAABAAAAAAEA"];
/**
 * Set the purpose consents in the SDK
 *
 * @param A valid Binary String: The '0' or '1' at position n – where n's indexing begins at 0 – indicates the consent status for purpose ID n+1; false and true respectively. eg. '1' at index 0 is consent true for purpose ID 1
 */
[ANGDPRSettings setPurposeConsents:@"10101001"];
```

> [!NOTE]
> To ensure proper monetization and relevant targeting, the SDK should be enabled to send the device information. Setting the `consentRequired` and `purposeConsents` flag correctly will help ensure proper device information is sent. Refer to the table below to determine whether the device details will be passed or not.

### Consent and device information logic

The table below describes the actions taken for the different `purposeConsents` values in combination with `consentRequired` values.

| deviceAccessConsent|deviceAccessConsent = true|deviceAccessConsent = false| deviceAccessConsent = undefined|
|--|--|--|--|
| `consentRequired=undefined<br>(gdprApplies = undefined)` | The SDK will read and pass IDFA/AAID info to server.| The SDK will **not** read and pass IDFA/AAID info to server.| The SDK will read and pass IDFA/AAID info to server.|
|`consentRequired=true<br>(gdprApplies = true)`| The SDK will read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server.|
| `consentRequired=false<br>(gdprApplies = false)`| The SDK will read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. |

Xandr provides three APIs that enable SDK users to set, retrieve and clear U.S. Privacy User Signal Mechanism controls. The IAB Tech Lab has formalized and adopted the "us_privacy" string as the mechanism to encode data about the information disclosed to the user and user elections under various US privacy laws, starting with the CCPA.

## California Consumer Privacy Act (CCPA)

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.  

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by IAB's CCPA Compliance Mechanism) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

``` 
/**
 * Set the IAB US Privacy String in the SDK
 */
[ANUSPrivacySettings setUSPrivacyString:@"1YNN"];
 
 
 
/**
 * Get the IAB US Privacy String in the SDK.
*/
[ANUSPrivacySettings getUSPrivacyString]
 
 
 
/**
 * Reset the value of IAB US Privacy String that was previously set using setUSPrivacyString
*/
[ANUSPrivacySettings reset];
```

## Global Privacy Platform (GPP)

[Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Core/CMP%20API%20Specification.md#in-app-details) is a single protocol designed to streamline transmitting privacy, consent, and consumer choice signals from websites and apps to ad tech providers. These signals are packaged in a standardized, easily communicated payload called a GPP String. The pre-parsed GPP data as well as the GPP string shall be stored under [NSUserDefaults](https:/ developer.apple.com/documentation/foundation/nsuserdefaults#1664798?language=objc) (iOS). This will allow the following:

- Vendors to easily access GPP data.
- GPP data to persist across app sessions.
- GPP data to be portable between CMPs to provide flexibility for a publisher to exchange one CMP SDK for another.
- Vendors within an app to avoid code duplication, by not requiring to include a GPP string decoder while still enabling all typical use cases.  

  > [!NOTE]
  > If a Publisher chooses to remove a CMP SDK from their app they are responsible for clearing all IABGPP\_\* vestigial values for users so that vendors do not continue to use the GPP data therein.

  Xandr SDK will then read the values from NSUserDefault which is then passed to the ad call. Following are the strings SDK will query from :

  | Key Name | Data type | Description |
  |--|--|--|
  | `IABGPP_HDR_GppString` | string | Full consent string in its encoded form. e.g "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN" |
  | `IABGPP_GppSID` | string | Section ID(s) considered to be in force. Multiple IDs are separated by underscore, e.g. “2_3” |  

## Digital Services Act (DSA)

The Digital Services Act (DSA) oversees online intermediaries and platforms, where its primary objective is to curb illegal and harmful activities on the internet and to mitigate the dissemination of disinformation. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

### Set DSA Values in SDK:

SDK will then pass these values to the ad call.

### Code sample

#### [Objective C](#tab/objectivec1)

```
/**
 * Set the DSA information requirement.
 * 0 = Not required
 * 1 = Supported, bid responses with or without DSA object will be accepted
 * 2 = Required, bid responses without DSA object will not be accepted
 * 3 = Required, bid responses without DSA object will not be accepted, Publisher is an Online Platform
 */
[ANDSASettings.sharedInstance setDsaRequired:1];
 
/**
 * Set if the publisher renders the DSA transparency info.
 * 0 = Publisher can't render
 * 1 = Publisher could render depending on adrender
 * 2 = Publisher will render
 */
[ANDSASettings.sharedInstance setPubRender:0];
 
/**
Set the transparency list using the provided list of ANDSATransparencyInfo.
Initializes an ANDSATransparencyInfo instance with the specified domain and params.
*/
NSMutableArray<ANDSATransparencyInfo *> *transparencyList = [NSMutableArray array];
[transparencyList addObject:[[ANDSATransparencyInfo alloc] initWithDomain:@"example.com" andDSAParams:@[@1, @2, @3]]];
[transparencyList addObject:[[ANDSATransparencyInfo alloc] initWithDomain:@"example.net" andDSAParams:@[@4, @5, @6]]];
 
[ANDSASettings.sharedInstance setTransparencyList:transparencyList];
```

#### [Swift](#tab/swift1)

```
/**
 * Set the DSA information requirement.
 * 0 = Not required
 * 1 = Supported, bid responses with or without DSA object will be accepted
 * 2 = Required, bid responses without DSA object will not be accepted
 * 3 = Required, bid responses without DSA object will not be accepted, Publisher is an Online Platform
 */
ANDSASettings.sharedInstance().dsaRequired = 1
  
/**
 * Set if the publisher renders the DSA transparency info.
 * 0 = Publisher can't render
 * 1 = Publisher could render depending on adrender
 * 2 = Publisher will render
 */
ANDSASettings.sharedInstance().pubRender = 0
  
/**
Set the transparency list using the provided list of ANDSATransparencyInfo.
Initializes an ANDSATransparencyInfo instance with the specified domain and params.
*/
var transparencyList : [ANDSATransparencyInfo] = []
  
let info1 = ANDSATransparencyInfo(domain: "example.com", andDSAParams: [1, 2, 3])
transparencyList.append(info1)
  
let info2 = ANDSATransparencyInfo(domain: "example.net", andDSAParams: [4, 5, 6])
transparencyList.append(info2)
  
ANDSASettings.sharedInstance().transparencyList = transparencyList
```

### Retrieve DSA values set in SDK

```
// Objective C
NSInteger dsaRequired = ANDSASettings.sharedInstance.dsaRequired;
NSInteger pubRender = ANDSASettings.sharedInstance.pubRender;
NSMutableArray<ANDSATransparencyInfo *> *transparencyList = [ANDSASettings.sharedInstance.transparencyList mutableCopy];
for (ANDSATransparencyInfo *transparencyInfo in transparencyList) {
NSString *domain = transparencyInfo.domain ?: @"";
NSArray<NSNumber *> *params = transparencyInfo.dsaparams ?: @[];
}

// Swift
let dsaRequired = ANDSASettings.sharedInstance().dsaRequired
let pubRender = ANDSASettings.sharedInstance().pubRender

if let transparencyList = ANDSASettings.sharedInstance().transparencyList {
for transparencyInfo in transparencyList {
let domain = transparencyInfo.domain ?? ""
let params = transparencyInfo.dsaparams ?? []
}
}
```

### Retrieve DSA Response values:

#### [Objective C](#tab/objectivec2)


```
- (void)requestBannerAd
{
// Make a banner ad view.
self.banner = [ANBannerAdView adViewWithFrame:CGRectMake(0, 0, 300, 250) placementId:@“1” adSize:CGSizeMake(300,250)];
self.banner.delegate = self;
//... Add required configurations
[self.banner loadAd];
}
// On Ad Loaded
- (void)adDidReceiveAd:(id)ad {
NSLog(@“Ad did receive ad”);

/**
* Retrieve on whose behalf the ad is displayed.
*/
NSString *behalf = self.banner.adResponseInfo.dsaResponseInfo.behalf;

/**
* Retrieve who paid for the ad.
*/
NSString *paid = self.banner.adResponseInfo.dsaResponseInfo.paid;

/**
* Retrieve the transparency user parameters info
*/
for (ANDSATransparencyInfo *transparencyInfo in self.banner.adResponseInfo.dsaResponseInfo.transparencyList) {
NSString *domain = transparencyInfo.domain;
NSArray<NSNumber *> *params = transparencyInfo.dsaparams;
}

/**
* Retrieve indicating if the buyer/advertiser will render DSA transparency info.
* 0 = buyer/advertiser will not render
* 1 = buyer/advertiser will render
*/
NSInteger adRender = self.banner.adResponseInfo.dsaResponseInfo.adRender;
}

```

#### [Swift](#tab/swift2)

```

func requestBannerAd() {
// Make a banner ad view.
self.banner = ANBannerAdView(frame: CGRect(origin: CGPoint(x: 0,y :0), size: CGSize(width: 300, height: 250)), placementId: “1”, adSize: CGSize(width: 300, height: 250))
self.banner!.rootViewController = self
self.banner!.delegate = self
//... Add required configurations
self.banner!.loadAd()
}
// On Ad Loaded
func adDidReceiveAd(_ ad: Any) {
print(“Ad did receive ad”)
 
/**
 * Retrieve on whose behalf the ad is displayed.
 */
let behalf : String = (self.banner?.adResponseInfo?.dsaResponseInfo?.behalf)!
 
/**
 * Retrieve who paid for the ad.
 */
let paid : String = (self.banner?.adResponseInfo?.dsaResponseInfo?.paid)!
 
/**
 * Retrieve the transparency user parameters info
 */
if let transparencyList = self.banner?.adResponseInfo?.dsaResponseInfo?.transparencyList as? [ANDSATransparencyInfo] {
 for transparencyInfo in transparencyList {
 let domain = transparencyInfo.domain
 let params = transparencyInfo.dsaparams as? [Int]
 }
}
 
/**
 * Retrieve indicating if the buyer/advertiser will render DSA transparency info.
 * 0 = buyer/advertiser will not render
 * 1 = buyer/advertiser will render
 */
let adRender : NSInteger = (self.banner?.adResponseInfo?.dsaResponseInfo?.adRender)!
}
```

> [!NOTE]
> ANDSAResponseInfo can be retrieved using VideoAd instance, Interstitial Ad View instance and Native Ad Response also apart from Banner Ad View

### Code sample

#### [Objective C](#tab/objectivec3)

```

// For interstitialAd once adDidReceiveAd is callback
NSString* interstitialAdDSAResponseInfo = self.interstitialAd.adResponseInfo.dsaResponseInfo; // same will be followed to get other dsaResponseInfo from interstitialAd
// For videoAd once adDidReceiveAd is callback
NSString* videoAdDSAResponseInfo = self.videoAd.adResponseInfo.dsaResponseInfo; // same will be followed to get other dsaResponseInfo from videoAd
// For nativeAd once didReceiveResponse is callback
ANAdResponseInfo nativeAdResponseInfo = nativeAdResponse;
NSString* nativeAdDSAResponseInfo = nativeAdResponseInfo.dsaResponseInfo; // same will be followed to get other dsaResponseInfo from videoAd
```

#### [Swift](#tab/swift3)

```

// For interstitialAd once adDidReceiveAd is callback
let interstitialAdDSAResponseInfo? : String = (self.interstitialAd.?.adResponseInfo?.dsaResponseInfo?)! // same will be followed to get other dsaResponseInfo from interstitialAd
// For videoAd once adDidReceiveAd is callback
let videoAdDSAResponseInfo? : String = (self.videoAd.?.adResponseInfo?.dsaResponseInfo?)! // same will be followed to get other dsaResponseInfo from videoAd
// For nativeAd once didReceiveResponse is callback
let nativeAdDSAResponseInfo : String = (self.nativeAdResponse.?.adResponseInfo?.dsaResponseInfo?)! // same will be followed to get other dsaResponseInfo from nativeAd
```

## Apple privacy manifest

Apple privacy manifest describe the data your app or third-party SDK collects. Starting with SDK version 8.11.4, we have added support for the Apple Privacy Manifest file requirement for third-party SDKs. To automatically receive the Privacy Manifest file, publishers' apps must use SDK version 8.11.4 or higher. For more information, see [Apple privacy manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files?language=swift)