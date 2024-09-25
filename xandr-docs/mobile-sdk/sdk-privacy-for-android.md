---
title: SDK Privacy for Android
description: Mobile SDKs include client support for Global Privacy Platform, General Data Protection Regulations, and the California Consumer Protection Act.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# SDK privacy for Android

Xandr's mobile SDKs include client support for Global Privacy Platform (GPP), the [General Data Protection Regulations](https://gdpr-info.eu/) (GDPR), and the [California Consumer Protection Act](https://oag.ca.gov/privacy/ccpa) (CCPA) and [Digital Services Act](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/europe-fit-digital-age/digital-services-act_en) (DSA).

The Global Privacy Platform (GPP) enables advertisers, publishers and technology vendors to adapt to regulatory demands across markets. GDPR provides regulations for the processing, movement, and protection of personal data within the European Union. CCPA creates new consumer rights relating to the access to, deletion of, and sharing of personal information that is collected by organizations. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

> [!WARNING]
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation. Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
> [!NOTE]
> - Publishers are responsible for providing notice, transparency, and choice and for collecting consent from their users in accordance with the [Framework policies](https://iabeurope.eu/transparency-consent-framework/), either using their own Consent Management Provider or working with a vendor.
    > - [Register your own CMP](https://register.consensu.org/CMP)
    > - [List of registered CMPs](https://iabeurope.eu/cmp-list/)
>
> - Our Service Policies (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.
> - All vendor SDKs (including mediation SDKs) are responsible for looking up approved vendor and consent information on their own; Xandr does not pass this information to these SDKs.

## General Data Protection Regulations (GDPR)

In order for our clients to meet their transparency, notice and choice/consent requirements under the GDPR and the existing ePrivacy Directive, Xandr supports the [IAB Europe Transparency & Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) (the "Framework").

This is a reference for mobile app publishers using Xandr's Mobile SDK to surface notice, transparency and choice to end users located in the EEA and signal approved vendors and, where necessary, pass consent, to Xandr and demand sources and their vendors through the Xandr platform.

Xandr provides three APIs in the Mobile SDK for mobile app publishers to use the Framework. These  APIs are available in Mobile SDK version 4.8+ for Android and 4.7.1+ for iOS. These APIs allow you to:

- Define whether the user is located in the European Economic Area (the "EEA") and that European privacy regulations should apply
- Set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/commit/a32574941ce201708e30e78702278efe1ce6cd59) (IAB) consent string
- Set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md) (IAB) purpose consents

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by [Mobile In-App CMP API v2.0: Transparency & Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/README.md)) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

```
/** * Set the consentRequired value in the SDK
 *
 * @param true if subject to GDPR regulations, false otherwise
 */
ANGDPRSettings.setConsentRequired(context,true);
   
   
/**
 * Set the consent string in the SDK
 *
 * @param A valid Base64 encode consent string as per 
 * https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework
 */
ANGDPRSettings.setConsentString(context,"BOMyQRvOMyQRvABABBAAABAAAAAAEA");
/**
 * Set the purpose consents in the SDK
 *
 * @param A valid Binary String: The '0' or '1' at position n – where n's indexing begins at 0 – indicates the consent status for purpose ID n+1; false and true respectively. eg. '1' at index 0 is consent true for purpose ID 1
 */
ANGDPRSettings.setPurposeConsents(context,"101010001");
```

> [!NOTE]
> To ensure proper monetization and relevant targeting, the SDK should be enabled to send the device information. Setting the `consentRequired` and `purposeConsents` flag correctly will help ensure proper device information is sent. Refer to the table below to determine whether the device details will be passed or not.

The table below describes the actions taken for the different `purposeConsents` values in combination with `consentRequired` values.

|  | true | false | undefined |
|:---|:---|:---|:---|
| `consentRequired=false` | The SDK will pass device info. | The SDK will **not** pass device info. | The SDK will pass device info. |
| `consentRequired=true` | The SDK will pass device info. | The SDK will **not** pass device info. | The SDK will **not** pass device info. |
| `consentRequired=undefined` | The SDK will pass device info. | The SDK will **not** pass device info. | The SDK will pass device info. |

## California Consumer Privacy Act (CCPA)

Xandr provides three APIs that enable SDK users to set, retrieve and clear U.S. Privacy User Signal Mechanism controls. The IAB Tech Lab has formalized and adopted the `"us_privacy"` string as the mechanism to encode data about the information disclosed to the user and user elections under various US privacy laws, starting with the CCPA.

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.  

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by IAB's CCPA Compliance Mechanism) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

```
/**
     * Set the IAB US Privacy String in the SDK
     *
     * @param privacyString will be set and pass string to Ad Server
     */
ANUSPrivacySettings.setUSPrivacyString(context,"1YNN");
 
 
    /**
     * Get the IAB US Privacy String  that will be sent in the request.
     *
     * @param context
     * @return Return IAB US Privacy String set by Publisher
     */
ANUSPrivacySettings.getUSPrivacyString(context);
 
 /**
     * Clear the value of IAB US Privacy String that was previously set using setUSPrivacyString
     *
     * @param context
     */
ANUSPrivacySettings.reset(context);
```

## Global Privacy Platform (GPP)

[Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Core/CMP%20API%20Specification.md#in-app-details) is a single protocol designed to streamline transmitting privacy, consent, and consumer choice signals from websites and apps to ad tech providers. These signals are packaged in a standardized, easily communicated payload called a GPP String. The pre-parsed GPP data as well as the GPP string shall be stored under [SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences.html) (Android). This will allow the following:

- Vendors to easily access GPP data.
- GPP data to persist across app sessions.
- GPP data to be portable between Consent Management Platforms (CMPs) to provide flexibility for a publisher to exchange one CMP SDK for another.
- Vendors within an app to avoid code duplication, by not requiring to include a GPP string decoder while still enabling all typical use cases.

> [!NOTE]
> If a Publisher chooses to remove a CMP SDK from their app they are responsible for clearing all IABGPP\_\* vestigial values for users so that vendors do not continue to use the GPP data therein.

Xandr SDK will then read the values from [SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences.html) which is then passed to the ad call. Following are the strings SDK will query from:

| Key Name | Data type | Description  |
|:---|:---|:---|
| `IABGPP_HDR_GppString` | string | Full consent string in its encoded form. e.g `"DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN"` |
| `IABGPP_GppSID` | string | Section ID(s) considered to be in force. Multiple IDs are separated by underscore, e.g. `“2_3”` |

## Digital Services Act (DSA)

The Digital Services Act (DSA) oversees online intermediaries and platforms, where its primary objective is to curb illegal and harmful activities on the internet and to mitigate the dissemination of disinformation. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

### Set DSA Values in the SDK

- SDK passes values to ad call

```
/**
 * Set the DSA information requirement.
 * 0 = Not required
 * 1 = Supported, bid responses with or without DSA object will be accepted
 * 2 = Required, bid responses without DSA object will not be accepted
 * 3 = Required, bid responses without DSA object will not be accepted, Publisher is an Online Platform
 *
 * @param dsaRequired The DSA information requirement value to be set.
 */
ANDSASettings.setDSARequired(1);
  
/**
 * Set if the publisher renders the DSA transparency info.
 * 0 = Publisher can't render
 * 1 = Publisher could render depending on adrender
 * 2 = Publisher will render
 *
 * @param pubRender The value indicating whether the publisher renders DSA transparency info.
 */
ANDSASettings.setPubRender(0);
  
/**
* Set the transparency list using the provided list of ANDSATransparencyInfo.
*
* @param domain The domain of the entity that applied user parameters.
* @param params The list of user parameters used for the platform or sell-side.
*/
ArrayList<ANDSATransparencyInfo> transparencyList = new ArrayList<>();
transparencyList.add(new ANDSATransparencyInfo("example.com", new ArrayList<>(Arrays.asList(1, 2, 3))));
transparencyList.add(new ANDSATransparencyInfo("example.net", new ArrayList<>(Arrays.asList(4, 5, 6))));
  
ANDSASettings.setTransparencyList(transparencyList);
```

- Retrieve DSA values set in SDK

```
ANDSASettings.getDSARequired()
ANDSASettings.getPubRender()
ANDSASettings.getTransparencyList()
```

### Retrieve DSA Response values

> [!NOTE]
> ANDSAResponseInfo can be retrieved using Video Ad instance, Interstitial Ad View instance and Native Ad Response also apart from Banner Ad View.

#### Code sample Java

```
// Request Banner Ad
bav = new BannerAdView(this);
bav.setPlacementID("1"); // Placement ID
bav.setAdSize(300, 250); // Size
bav.setAdListener(this) // AdListener
// On Ad Loaded
@Override
public void onAdLoaded(AdView bav) {
log("Banner Ad Loaded");

ANDSAResponseInfo dsaResponseInfo = bav.getAdResponseInfo().getDSAResponseInfo();

/**
* Retrieve on whose behalf the ad is displayed.
*/
String behalf = dsaResponseInfo.getBehalf();

/**
* Retrieve who paid for the ad.
*/
String paid = dsaResponseInfo.getPaid();

/**
* Retrieve the transparency user parameters info
*/
ArrayList<ANDSATransparencyInfo> transparencyList = dsaResponseInfo.getTransparencyList();

for(int i = 0; i <= transparencyList.size(); i++) {
ANDSATransparencyInfo tranparencyInfo = transparencyList.get(i);
String domain = tranparencyInfo.getDomain();
ArrayList<Integer> params = tranparencyInfo.getDSAParams();
}

/**
* Retrieve indicating if the buyer/advertiser will render DSA transparency info.
* 0 = buyer/advertiser will not render
* 1 = buyer/advertiser will render
*/
int adRender = dsaResponseInfo.getAdRender();
}
```

#### Code Sample Kotlin

```
// Request Banner Ad
banner = BannerAdView(this)
banner.placementID = "1" // PlacementID
banner.setAdSize(300, 250) // Size
banner.adListener = this // AdListener
banner.loadAd()
// On Ad Loaded
override fun onAdLoaded(ad: AdView?) {
log("Banner Ad Loaded")
  
val dsaResponseInfo: ANDSAResponseInfo = bav.adResponseInfo.dsaResponseInfo
  
/**
 * Retrieve on whose behalf the ad is displayed.
 */
val behalf: String? = dsaResponseInfo.behalf
  
/**
 * Retrieve who paid for the ad.
 */
val paid: String? = dsaResponseInfo.paid
  
/**
 * Retrieve the transparency user parameters info
 */
val transparencyList: ArrayList<ANDSATransparencyInfo> = dsaResponseInfo.transparencyList
  
for (i in 0 until transparencyList.size) {
    val transparencyInfo: ANDSATransparencyInfo = transparencyList[i]
    val domain: String = transparencyInfo.domain
    val params: ArrayList<Int> = transparencyInfo.getDSAParams()
}
}
/**
 * Retrieve indicating if the buyer/advertiser will render DSA transparency info.
 * 0 = buyer/advertiser will not render
 * 1 = buyer/advertiser will render
 */
val adRender: Int = dsaResponseInfo.adRender
```

## Code sample (Video ad)

### [Java](#tab/java1)

```
Java
//Video Ad
ANDSAResponseInfo dsaResponseInfo = videoAd.getAdResponseInfo().getDSAResponseInfo()
//Native Ad
ANDSAResponseInfo dsaResponseInfo = nativeAdResponse.getAdResponseInfo().getDSAResponseInfo()
//Insterstitial Ad View
ANDSAResponseInfo dsaResponseInfo = interstitial.getAdResponseInfo().getDSAResponseInfo()
```

### [Kotlin](#tab/kotlin1)

```
Kotlin
//Video Ad
val dsaResponseInfo = videoAd.adResponseInfo.dsaResponseInfo
//Native Ad
val dsaResponseInfo = nativeAdResponse.adResponseInfo.dsaResponseInfo
//Insterstitial Ad View
val dsaResponseInfo = interstitial.adResponseInfo.dsaResponseInfo
```
