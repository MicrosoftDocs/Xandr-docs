---
title: SDK Privacy for Android
description: Android SDK includes client support for Global Privacy Platform, General Data Protection Regulations, the California Consumer Privacy Act, and the Children's Online Privacy Protection Act.
ms.custom: android-sdk
ms.date: 07/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# SDK privacy for Android

The Android SDK includes client support for Global Privacy Platform (GPP), the [General Data Protection Regulations](https://gdpr-info.eu/) (GDPR), and the [California Consumer Protection Act](https://oag.ca.gov/privacy/ccpa) (CCPA) and [Digital Services Act](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/europe-fit-digital-age/digital-services-act_en) (DSA).

The Global Privacy Platform (GPP) enables advertisers, publishers and technology vendors to adapt to regulatory demands across markets. GDPR provides regulations for the processing, movement, and protection of personal data within the European Union. CCPA creates new consumer rights relating to the access to, deletion of, and sharing of personal information that is collected by organizations. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

> [!WARNING]
> This resource should not be construed as legal advice and Microsoft makes no guarantees about compliance with any law or regulation. Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
> [!NOTE]
>
> - Publishers are responsible for providing notice, transparency, and choice and for collecting consent from their users in accordance with the [Framework policies](https://iabeurope.eu/transparency-consent-framework/), either using their own Consent Management Provider or working with a vendor.
    > - [Register your own CMP](https://register.consensu.org/CMP)
    > - [List of registered CMPs](https://iabeurope.eu/cmp-list/)
>
> - Our Service Policies (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.
> - All vendor SDKs (including mediation SDKs) are responsible for looking up approved vendor and consent information on their own; Microsoft Monetize does not pass this information to these SDKs.

## General Data Protection Regulations (GDPR)

In order for our clients to meet their transparency, notice and choice/consent requirements under the GDPR and the existing ePrivacy Directive, Microsoft Monetize supports the [IAB Europe Transparency & Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) (the "Framework").

This is a reference for mobile app publishers using the Android SDK to surface notice, transparency and choice to end users located in the EEA and signal approved vendors and, where necessary, pass consent, to Microsoft Monetize and demand sources and their vendors through the Monetize platform.

The Android SDK provides three APIs for mobile app publishers to use the Framework. These APIs allow you to:

- Define whether the user is located in the European Economic Area (the "EEA") and that European privacy regulations should apply
- Set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/commit/a32574941ce201708e30e78702278efe1ce6cd59) (IAB) consent string
- Set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md) (IAB) purpose consents

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by [Mobile In-App CMP API v2.0: Transparency & Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/README.md)) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

Use the following methods on `ANGDPRSettings`:

| Method | Description |
|:---|:---|
| `public static void setConsentRequired(Context context, boolean subjectToGDPR)` | Set whether the user is subject to GDPR regulations. |
| `public static void setConsentString(Context context, String consentString)` | Set the IAB Base64-encoded consent string. |
| `public static void setPurposeConsents(Context context, String purposeConsents)` | Set the IAB purpose consents binary string. `'0'` or `'1'` at position `n` (indexing from 0) indicates the consent status for purpose ID `n+1`. |

### [Kotlin](#tab/kotlin1)

```
// Set whether the user is subject to GDPR regulations
ANGDPRSettings.setConsentRequired(context, true)

// Set the IAB Base64-encoded consent string
ANGDPRSettings.setConsentString(context, "BOMyQRvOMyQRvABABBAAABAAAAAAEA")

// Set the IAB purpose consents (binary string; '1' at index n = consent for purpose ID n+1)
ANGDPRSettings.setPurposeConsents(context, "101010001")
```

### [Java](#tab/java1)

```
// Set whether the user is subject to GDPR regulations
ANGDPRSettings.setConsentRequired(context, true);

// Set the IAB Base64-encoded consent string
ANGDPRSettings.setConsentString(context, "BOMyQRvOMyQRvABABBAAABAAAAAAEA");

// Set the IAB purpose consents (binary string; '1' at index n = consent for purpose ID n+1)
ANGDPRSettings.setPurposeConsents(context, "101010001");
```

---

> [!NOTE]
> To ensure proper monetization and relevant targeting, the SDK should be enabled to send the device information. Setting the `consentRequired` and `purposeConsents` flag correctly will help ensure proper device information is sent. Refer to the table below to determine whether the device details will be passed or not.

### Consent and device information logic

The following table describes the SDK behavior based on different `purposeConsents` values in combination with `consentRequired` values:

| `deviceAccessConsent` | `true` | `false` | `undefined` |
|----------------------|--------|---------|------------|
| `consentRequired=false` | The SDK will pass device info. | **The SDK will pass device info.** | The SDK will pass device info. |
| `consentRequired=true` | The SDK will pass device info. | The SDK will not pass device info. | The SDK will not pass device info. |
| `consentRequired=undefined` | The SDK will pass device info. | The SDK will not pass device info. | The SDK will pass device info. |

## California Consumer Privacy Act (CCPA)

The Android SDK provides three APIs that enable SDK users to set, retrieve and clear U.S. Privacy User Signal Mechanism controls. The IAB Tech Lab has formalized and adopted the `"us_privacy"` string as the mechanism to encode data about the information disclosed to the user and user elections under various US privacy laws, starting with the CCPA.

This information will be persisted by the SDK and will be added to each ad call for applying platform controls.  

Publishers/Consent Management Platforms (CMPs) are free to store these values in a SharedPreferences interface (as defined by IAB's CCPA Compliance Mechanism) instead of passing them via the new APIs, and the SDK will read the values as a fallback.

Use the following methods on `ANUSPrivacySettings`:

| Method | Description |
|:---|:---|
| `public static void setUSPrivacyString(Context context, String privacyString)` | Set the IAB US Privacy String in the SDK. |
| `public static String getUSPrivacyString(Context context)` | Get the IAB US Privacy String currently in the SDK. |
| `public static void reset(Context context)` | Clear the previously set IAB US Privacy String. |

### [Kotlin](#tab/kotlin2)

```
// Set the IAB US Privacy String in the SDK
ANUSPrivacySettings.setUSPrivacyString(context, "1YNN")

// Get the IAB US Privacy String that will be sent in the request
val privacyString: String? = ANUSPrivacySettings.getUSPrivacyString(context)

// Clear the previously set IAB US Privacy String
ANUSPrivacySettings.reset(context)
```

### [Java](#tab/java2)

```
// Set the IAB US Privacy String in the SDK
ANUSPrivacySettings.setUSPrivacyString(context, "1YNN");

// Get the IAB US Privacy String that will be sent in the request
String privacyString = ANUSPrivacySettings.getUSPrivacyString(context);

// Clear the previously set IAB US Privacy String
ANUSPrivacySettings.reset(context);
```

---

## Children's Online Privacy Protection Act (COPPA)

The [U.S. Children's Online Privacy Protection Act](https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa) (COPPA) applies when your app's ad requests are directed to children under the age of 13. When COPPA is enabled, the SDK sends `user.coppa = true` in the ad request so downstream systems can restrict the collection of personal information for those users.

Use the `SDKSettings.setCOPPA(boolean)` API to signal that the current session is subject to COPPA. The value is applied to every subsequent ad request until it is changed. Default value is `false`.

Use the following methods on `SDKSettings`:

| Method | Description |
|:---|:---|
| `public static void setCOPPA(boolean coppa)` | Signal that the current session is subject to COPPA. Default value is `false`. |
| `public static boolean getCOPPA()` | Returns `true` if COPPA is currently enabled, `false` otherwise. |

### [Kotlin](#tab/kotlin3)

```
// Enable or disable COPPA for the current session
SDKSettings.setCOPPA(true)

// Check whether COPPA is currently enabled
val coppa: Boolean = SDKSettings.getCOPPA()
```

### [Java](#tab/java3)

```
// Enable or disable COPPA for the current session
SDKSettings.setCOPPA(true);

// Check whether COPPA is currently enabled
boolean coppa = SDKSettings.getCOPPA();
```

---

## Global Privacy Platform (GPP)

[Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Core/CMP%20API%20Specification.md#in-app-details) is a single protocol designed to streamline transmitting privacy, consent, and consumer choice signals from websites and apps to ad tech providers. These signals are packaged in a standardized, easily communicated payload called a GPP String. The pre-parsed GPP data as well as the GPP string shall be stored under [SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences.html) (Android). This will allow the following:

- Vendors to easily access GPP data.
- GPP data to persist across app sessions.
- GPP data to be portable between Consent Management Platforms (CMPs) to provide flexibility for a publisher to exchange one CMP SDK for another.
- Vendors within an app to avoid code duplication, by not requiring to include a GPP string decoder while still enabling all typical use cases.

> [!NOTE]
> If a Publisher chooses to remove a CMP SDK from their app they are responsible for clearing all IABGPP\_\* vestigial values for users so that vendors do not continue to use the GPP data therein.

The Android SDK will then read the values from [SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences.html) which is then passed to the ad call. Following are the strings SDK will query from:

| Key Name | Data type | Description  |
|:---|:---|:---|
| `IABGPP_HDR_GppString` | string | Full consent string in its encoded form. e.g `"DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN"` |
| `IABGPP_GppSID` | string | Section ID(s) considered to be in force. Multiple IDs are separated by underscore, e.g. `“2_3”` |

## Digital Services Act (DSA)

The Digital Services Act (DSA) oversees online intermediaries and platforms, where its primary objective is to curb illegal and harmful activities on the internet and to mitigate the dissemination of disinformation. The DSA is a key legislative measure by the European Union aimed at enhancing transparency in digital advertising, with a core objective of promoting transparency, accountability, and user protection in online services.

### Set and retrieve DSA values in the SDK

The SDK passes these values to the ad call.

Use the following methods on `ANDSASettings`:

| Method | Description |
|:---|:---|
| `public static void setDSARequired(int dsaRequired)` | Set the DSA information requirement. `0` = Not required, `1` = Supported, `2` = Required, `3` = Required + Publisher is an Online Platform. |
| `public static int getDSARequired()` | Returns the current DSA information requirement. |
| `public static void setPubRender(int pubRender)` | Set whether the publisher renders DSA transparency info. `0` = Publisher can't render, `1` = Publisher could render depending on adrender, `2` = Publisher will render. |
| `public static int getPubRender()` | Returns the current publisher-render setting. |
| `public static void setTransparencyList(ArrayList<ANDSATransparencyInfo> transparencyList)` | Set the transparency list using `ANDSATransparencyInfo` entries. |
| `public static ArrayList<ANDSATransparencyInfo> getTransparencyList()` | Returns the current transparency list. |

#### [Kotlin](#tab/kotlin4)

```
// Set DSA information requirement (0=Not required, 1=Supported, 2=Required, 3=Required + Online Platform)
ANDSASettings.setDSARequired(1)

// Set publisher render behavior (0=Can't render, 1=Depends on adrender, 2=Will render)
ANDSASettings.setPubRender(0)

// Set the transparency list
ANDSASettings.setTransparencyList(arrayListOf(
    ANDSATransparencyInfo("example.com", arrayListOf(1, 2, 3)),
    ANDSATransparencyInfo("example.net", arrayListOf(4, 5, 6))
))
```

#### [Java](#tab/java4)

```
// Set DSA information requirement (0=Not required, 1=Supported, 2=Required, 3=Required + Online Platform)
ANDSASettings.setDSARequired(1);

// Set publisher render behavior (0=Can't render, 1=Depends on adrender, 2=Will render)
ANDSASettings.setPubRender(0);

// Set the transparency list
ArrayList<ANDSATransparencyInfo> transparencyList = new ArrayList<>();
transparencyList.add(new ANDSATransparencyInfo("example.com", new ArrayList<>(Arrays.asList(1, 2, 3))));
transparencyList.add(new ANDSATransparencyInfo("example.net", new ArrayList<>(Arrays.asList(4, 5, 6))));
ANDSASettings.setTransparencyList(transparencyList);
```

---

### Retrieve DSA Response values

Use the following methods on `ANDSAResponseInfo`:

| Method | Description |
|:---|:---|
| `public String getBehalf()` | On whose behalf the ad is displayed. |
| `public String getPaid()` | Who paid for the ad. |
| `public ArrayList<ANDSATransparencyInfo> getTransparencyList()` | Transparency user parameters info. |
| `public int getAdRender()` | Whether the buyer/advertiser will render DSA transparency info. `0` = will not render, `1` = will render. |

#### [Kotlin](#tab/kotlin5)

```
val banner = BannerAdView(this)
banner.placementID = "1"
banner.setAdSize(300, 250)
banner.adListener = this
banner.loadAd()

override fun onAdLoaded(ad: AdView?) {
    //   The example uses `banner`. For other ad units, use:
    //   videoAd.adResponseInfo.dsaResponseInfo
    //   nativeAdResponse.adResponseInfo.dsaResponseInfo  (in NativeAdRequestListener.onAdLoaded)
    //   interstitial.adResponseInfo.dsaResponseInfo
    banner.adResponseInfo.dsaResponseInfo?.let { info ->
        val behalf: String? = info.behalf          // Advertised on behalf of
        val paid: String? = info.paid              // Paid by
        val adRender: Int = info.adRender          // 0 = won't render, 1 = will render
        for (t in info.transparencyList) {
            val domain: String = t.domain
            val params: ArrayList<Int> = t.getDSAParams()
        }
    }
}
```

#### [Java](#tab/java5)

```
BannerAdView banner = new BannerAdView(this);
banner.setPlacementID("1");
banner.setAdSize(300, 250);
banner.setAdListener(this);
banner.loadAd();

@Override
public void onAdLoaded(AdView bav) {
    //   The example uses `bav`. For other ad units, use:
    //   videoAd.getAdResponseInfo().getDSAResponseInfo()
    //   nativeAdResponse.getAdResponseInfo().getDSAResponseInfo()  (in NativeAdRequestListener.onAdLoaded)
    //   interstitial.getAdResponseInfo().getDSAResponseInfo()
    ANDSAResponseInfo info = bav.getAdResponseInfo().getDSAResponseInfo();
    if (info != null) {
        String behalf = info.getBehalf();          // Advertised on behalf of
        String paid = info.getPaid();              // Paid by
        int adRender = info.getAdRender();         // 0 = won't render, 1 = will render
        for (ANDSATransparencyInfo t : info.getTransparencyList()) {
            String domain = t.getDomain();
            ArrayList<Integer> params = t.getDSAParams();
        }
    }
}
```

---

## Related

- [Publisher-side user opt-out (Do Not Track) for Android](publisher-side-user-opt-out-for-android.md)
