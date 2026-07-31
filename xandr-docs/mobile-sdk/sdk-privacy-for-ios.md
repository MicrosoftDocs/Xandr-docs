---
title: SDK Privacy for iOS
description: iOS SDK includes client support for Global Privacy Platform, General Data Protection Regulations, the California Consumer Privacy Act, and the Children's Online Privacy Protection Act.
ms.date: 07/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank

---

# SDK Privacy for iOS

The iOS SDK includes client support for Global Privacy Platform (GPP), the [General Data Protection Regulations](https://gdpr-info.eu/) (GDPR), and the [California Consumer Protection Act](https://oag.ca.gov/privacy/ccpa) (CCPA) and [Digital Services Act](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/europe-fit-digital-age/digital-services-act_en) (DSA).

The Global Privacy Platform (GPP) enables advertisers, publishers and technology vendors to adapt to regulatory demands across markets. GDPR provides regulations for the processing, movement, and protection of personal data within the European Union. CCPA creates new consumer rights relating to the access to, deletion of, and sharing of personal information that is collected by organizations. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

> [!WARNING]
> This resource should not be construed as legal advice and Microsoft makes no guarantees about compliance with any law or regulation. Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
>
> [!NOTE]
> Publishers are responsible for providing notice, transparency, and choice and for collecting consent from their users in accordance with the [Framework policies](https://iabeurope.eu/transparency-consent-framework/), either using their own Consent Management Provider or working with a vendor.
>
> - [Register your own CMP](https://register.consensu.org/CMP)
> - [List of registered CMPs](https://iabeurope.eu/cmp-list/)
>
> - Note our Service Policies (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.
> - All vendor SDKs (including mediation SDKs) are responsible for looking up approved vendor and consent information on their own; Microsoft Monetize does not pass this information to these SDKs.

## General data protection regulations (GDPR)

In order for our clients to meet their transparency, notice and choice/consent requirements under the GDPR and the existing ePrivacy Directive, Microsoft Monetize supports [the IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/)(the "Framework").

This is a reference for mobile app publishers using the iOS SDK to surface notice, transparency and choice to end users located in the EEA and signal approved vendors and, where necessary, pass consent, to Microsoft Monetize and demand sources and their vendors through the Monetize platform.

The iOS SDK provides three APIs for mobile app publishers to use the Framework. These APIs allow you to:

- define whether the user is located in the European Economic Area (the "EEA") and that European privacy regulations should apply
- set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/commit/a32574941ce201708e30e78702278efe1ce6cd59)(IAB) consent string

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by [Mobile In-App CMP API v2.0: Transparency &amp; Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/README.md)) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

Use the following methods on `ANGDPRSettings`:

| Method | Description |
|:---|:---|
| `+ (void)setConsentRequired:(nonnull NSNumber *)consentRequired` | Set whether the user is subject to GDPR regulations. |
| `+ (void)setConsentString:(nonnull NSString *)consentString` | Set the IAB Base64-encoded consent string. |
| `+ (void)setPurposeConsents:(nonnull NSString *)purposeConsents` | Set the IAB purpose consents binary string. `'0'` or `'1'` at position `n` (indexing from 0) indicates the consent status for purpose ID `n+1`. |

### [Swift](#tab/swift1)

```
// Set whether the user is subject to GDPR regulations
ANGDPRSettings.setConsentRequired(true)

// Set the IAB Base64-encoded consent string
ANGDPRSettings.setConsentString("BOMyQRvOMyQRvABABBAAABAAAAAAEA")

// Set the IAB purpose consents (binary string; '1' at index n = consent for purpose ID n+1)
ANGDPRSettings.setPurposeConsents("10101001")
```

### [Objective-C](#tab/objectivec1)

```
// Set whether the user is subject to GDPR regulations
[ANGDPRSettings setConsentRequired:1];

// Set the IAB Base64-encoded consent string
[ANGDPRSettings setConsentString:@"BOMyQRvOMyQRvABABBAAABAAAAAAEA"];

// Set the IAB purpose consents (binary string; '1' at index n = consent for purpose ID n+1)
[ANGDPRSettings setPurposeConsents:@"10101001"];
```

---

> [!NOTE]
> To ensure proper monetization and relevant targeting, the SDK should be enabled to send the device information. Setting the `consentRequired` and `purposeConsents` flag correctly will help ensure proper device information is sent. Refer to the table below to determine whether the device details will be passed or not.

### Consent and device information logic

The table below describes the actions taken for the different `purposeConsents` values in combination with `consentRequired` values.

| deviceAccessConsent|deviceAccessConsent = true|deviceAccessConsent = false| deviceAccessConsent = undefined|
|--|--|--|--|
| `consentRequired=undefined<br>(gdprApplies = undefined)` | The SDK will read and pass IDFA/AAID info to server.| The SDK will **not** read and pass IDFA/AAID info to server.| The SDK will read and pass IDFA/AAID info to server.|
|`consentRequired=true<br>(gdprApplies = true)`| The SDK will read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server.|
| `consentRequired=false<br>(gdprApplies = false)`| The SDK will read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. |

The iOS SDK provides three APIs that enable SDK users to set, retrieve and clear U.S. Privacy User Signal Mechanism controls. The IAB Tech Lab has formalized and adopted the "us_privacy" string as the mechanism to encode data about the information disclosed to the user and user elections under various US privacy laws, starting with the CCPA.

## California Consumer Privacy Act (CCPA)

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.  

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by IAB's CCPA Compliance Mechanism) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

Use the following methods on `ANUSPrivacySettings`:

| Method | Description |
|:---|:---|
| `+ (void)setUSPrivacyString:(nonnull NSString *)privacyString` | Set the IAB US Privacy String in the SDK. |
| `+ (nonnull NSString *)getUSPrivacyString` | Get the IAB US Privacy String currently in the SDK. |
| `+ (void)reset` | Reset the previously set IAB US Privacy String. |

### [Swift](#tab/swift2)

```
// Set the IAB US Privacy String in the SDK
ANUSPrivacySettings.setUSPrivacyString("1YNN")

// Get the IAB US Privacy String currently in the SDK
let privacyString: String? = ANUSPrivacySettings.getUSPrivacyString()

// Reset the previously set IAB US Privacy String
ANUSPrivacySettings.reset()
```

### [Objective-C](#tab/objectivec2)

```
// Set the IAB US Privacy String in the SDK
[ANUSPrivacySettings setUSPrivacyString:@"1YNN"];

// Get the IAB US Privacy String currently in the SDK
NSString *privacyString = [ANUSPrivacySettings getUSPrivacyString];

// Reset the previously set IAB US Privacy String
[ANUSPrivacySettings reset];
```

---

## Children's Online Privacy Protection Act (COPPA)

The [U.S. Children's Online Privacy Protection Act](https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa) (COPPA) applies when your app's ad requests are directed to children under the age of 13. When COPPA is enabled, the SDK sends `user.coppa = true` in the ad request so downstream systems can restrict the collection of personal information for those users.

Set the `coppa` property on `[ANSDKSettings sharedInstance]` to signal that the current session is subject to COPPA. The value is applied to every subsequent ad request until it is changed. Default value is `NO`.

Use the following property on `ANSDKSettings`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `coppa` | `BOOL` | readwrite | Signal that the current session is subject to COPPA. Default value is `NO`. |

### [Swift](#tab/swift3)

```
// Enable or disable COPPA for the current session
ANSDKSettings.sharedInstance().coppa = true

// Check whether COPPA is currently enabled
let coppa: Bool = ANSDKSettings.sharedInstance().coppa
```

### [Objective-C](#tab/objectivec3)

```
// Enable or disable COPPA for the current session
[ANSDKSettings sharedInstance].coppa = YES;

// Check whether COPPA is currently enabled
BOOL coppa = [ANSDKSettings sharedInstance].coppa;
```

---

## Global Privacy Platform (GPP)

[Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Core/CMP%20API%20Specification.md#in-app-details) is a single protocol designed to streamline transmitting privacy, consent, and consumer choice signals from websites and apps to ad tech providers. These signals are packaged in a standardized, easily communicated payload called a GPP String. The pre-parsed GPP data as well as the GPP string shall be stored under [NSUserDefaults](https:/ developer.apple.com/documentation/foundation/nsuserdefaults#1664798?language=objc) (iOS). This will allow the following:

- Vendors to easily access GPP data.
- GPP data to persist across app sessions.
- GPP data to be portable between CMPs to provide flexibility for a publisher to exchange one CMP SDK for another.
- Vendors within an app to avoid code duplication, by not requiring to include a GPP string decoder while still enabling all typical use cases.  

  > [!NOTE]
  > If a Publisher chooses to remove a CMP SDK from their app they are responsible for clearing all IABGPP\_\* vestigial values for users so that vendors do not continue to use the GPP data therein.

  The iOS SDK will then read the values from NSUserDefault which is then passed to the ad call. Following are the strings SDK will query from :

  | Key Name | Data type | Description |
  |--|--|--|
  | `IABGPP_HDR_GppString` | string | Full consent string in its encoded form. e.g "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN" |
  | `IABGPP_GppSID` | string | Section ID(s) considered to be in force. Multiple IDs are separated by underscore, e.g. “2_3” |  

## Digital Services Act (DSA)

The Digital Services Act (DSA) oversees online intermediaries and platforms, where its primary objective is to curb illegal and harmful activities on the internet and to mitigate the dissemination of disinformation. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

### Set and retrieve DSA values in the SDK

The SDK passes these values to the ad call.

Use the following properties on `ANDSASettings`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `dsaRequired` | `NSInteger` | readwrite, assign | DSA information requirement. `0` = Not required, `1` = Supported, `2` = Required, `3` = Required + Publisher is an Online Platform. |
| `pubRender` | `NSInteger` | readwrite, assign | Whether the publisher renders DSA transparency info. `0` = Publisher can't render, `1` = Publisher could render depending on adrender, `2` = Publisher will render. |
| `transparencyList` | `NSArray<ANDSATransparencyInfo *> *` | strong, nullable | Transparency list of `ANDSATransparencyInfo` entries. |

#### [Swift](#tab/swift4)

```
// Set DSA information requirement (0=Not required, 1=Supported, 2=Required, 3=Required + Online Platform)
ANDSASettings.sharedInstance().dsaRequired = 1

// Set publisher render behavior (0=Can't render, 1=Depends on adrender, 2=Will render)
ANDSASettings.sharedInstance().pubRender = 0

// Set the transparency list
ANDSASettings.sharedInstance().transparencyList = [
    ANDSATransparencyInfo(domain: "example.com", andDSAParams: [1, 2, 3]),
    ANDSATransparencyInfo(domain: "example.net", andDSAParams: [4, 5, 6])
]
```

#### [Objective-C](#tab/objectivec4)

```
// Set DSA information requirement (0=Not required, 1=Supported, 2=Required, 3=Required + Online Platform)
[ANDSASettings.sharedInstance setDsaRequired:1];

// Set publisher render behavior (0=Can't render, 1=Depends on adrender, 2=Will render)
[ANDSASettings.sharedInstance setPubRender:0];

// Set the transparency list
ANDSASettings.sharedInstance.transparencyList = @[
    [[ANDSATransparencyInfo alloc] initWithDomain:@"example.com" andDSAParams:@[@1, @2, @3]],
    [[ANDSATransparencyInfo alloc] initWithDomain:@"example.net" andDSAParams:@[@4, @5, @6]]
];
```

---

### Retrieve DSA Response values

Use the following properties on `ANDSAResponseInfo`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `behalf` | `NSString *` | readwrite, strong, nullable | On whose behalf the ad is displayed. |
| `paid` | `NSString *` | readwrite, strong, nullable | Who paid for the ad. |
| `transparencyList` | `NSMutableArray<ANDSATransparencyInfo *> *` | strong, nullable | Transparency user parameters info. |
| `adRender` | `NSInteger` | readwrite, assign | Whether the buyer/advertiser will render DSA transparency info. `0` = will not render, `1` = will render. |

#### [Swift](#tab/swift5)

```
banner = ANBannerAdView(frame: CGRect(x: 0, y: 0, width: 300, height: 250), placementId: "1")
banner?.delegate = self
banner?.loadAd()

func adDidReceiveAd(_ ad: Any) {
    //   The example uses `banner`. For other ad units, use:
    //   interstitialAd?.adResponseInfo?.dsaResponseInfo
    //   videoAd?.adResponseInfo?.dsaResponseInfo
    //   nativeAdResponse.adResponseInfo?.dsaResponseInfo  (in ANNativeAdRequestDelegate.adRequest(_:didReceiveResponse:))
    if let info = banner?.adResponseInfo?.dsaResponseInfo {
        let behalf = info.behalf                   // Advertised on behalf of
        let paid = info.paid                       // Paid by
        let adRender = info.adRender               // 0 = won't render, 1 = will render
        for t in info.transparencyList ?? [] {
            let domain = t.domain
            let params = t.dsaparams as? [NSNumber]
        }
    }
}
```

#### [Objective-C](#tab/objectivec5)

```
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:CGRectMake(0, 0, 300, 250) placementId:@"1"];
banner.delegate = self;
[banner loadAd];
self.banner = banner;

- (void)adDidReceiveAd:(id)ad {
    ANBannerAdView *banner = self.banner;
    //   The example uses `banner`. For other ad units, use:
    //   interstitialAd.adResponseInfo.dsaResponseInfo
    //   videoAd.adResponseInfo.dsaResponseInfo
    //   nativeAdResponse.adResponseInfo.dsaResponseInfo  (in [ANNativeAdRequestDelegate adRequest:didReceiveResponse:])
    ANDSAResponseInfo *info = banner.adResponseInfo.dsaResponseInfo;
    if (info) {
        NSString *behalf = info.behalf;            // Advertised on behalf of
        NSString *paid = info.paid;                // Paid by
        NSInteger adRender = info.adRender;        // 0 = won't render, 1 = will render
        for (ANDSATransparencyInfo *t in info.transparencyList) {
            NSString *domain = t.domain;
            NSArray<NSNumber *> *params = t.dsaparams;
        }
    }
}
```

---


## Apple privacy manifest

The Apple Privacy Manifest describes the data your app or third-party SDK collects. The iOS SDK includes support for the Apple Privacy Manifest file requirement for third-party SDKs, and the Privacy Manifest file is delivered automatically with the SDK. For more information, see [Apple privacy manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files?language=swift).

## Related

- [Publisher-side user opt-out (Do Not Track) for iOS](publisher-side-user-opt-out-for-ios.md)
