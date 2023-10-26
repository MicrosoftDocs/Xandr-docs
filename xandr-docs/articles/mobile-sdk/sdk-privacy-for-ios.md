---
title: SDK Privacy for iOS
description: Xandr's mobile SDKs include client support for Global Privacy Platform (GPP), and the California Consumer Protection Act (CCPA).
ms.custom: ios-sdk 
ms.custom: android-sdk
---

# SDK Privacy for iOS

Xandr's mobile SDKs include client support for
Global Privacy Platform (GPP), the [General Data Protection Regulations](https://gdpr-info.eu/) (GDPR), and the [California Consumer Protection Act](https://oag.ca.gov/privacy/ccpa) (CCPA).

GDPR provides regulations for the processing, movement, and protection
of personal data within the European Union. CCPA creates new consumer
rights relating to the access to, deletion of, and sharing of personal
information that is collected by organizations. The Global Privacy
Platform (GPP) enables advertisers, publishers and technology vendors
to adapt to regulatory demands across markets.

> [!WARNING]
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation.  Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business. Note our Service Policies (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.

> [!NOTE]
> Publishers are responsible for providing notice, transparency, and choice and for collecting consent from their users in accordance with [the Framework policies](https://iabeurope.eu/transparency-consent-framework/), either using their own Consent Management Provider or working with a vendor.
> - [Register your own CMP](https://register.consensu.org/CMP)
> - [List of registered CMPs](https://advertisingconsent.eu/cmp-list/)
>
> All vendor SDKs (including mediation SDKs) are responsible for looking up approved vendor and consent information on their own; Xandr does not pass this information to these SDKs

## General data protection regulations (GDPR)

In order for our clients to meet their transparency, notice and
choice/consent requirements under the GDPR and the existing ePrivacy
Directive, Xandr
supports [the IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/)(the "Framework").

This is a reference for mobile app publishers using
Xandr's Mobile SDK to surface notice,
transparency and choice to end users located in the EEA and signal
approved vendors and, where necessary, pass consent, to
Xandr and demand sources and their vendors
through the Xandr platform.

Xandr provides three APIs in the Mobile SDK for
mobile app publishers to use the Framework. (These  APIs are available
in Mobile SDK version 4.8+ for Android and 4.7.1+ for iOS.) These APIs
allow you to:

- define whether the user is located in the European Economic Area (the
  "EEA") and that European privacy regulations should apply
- set the [IAB Europe](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/commit/a32574941ce201708e30e78702278efe1ce6cd59)(IAB) consent string

This information will be persisted by the SDK and will be added to each
ad call for applying platform controls. 

Publishers/Consent Management Platforms (CMPs) are free to store these
values in a SharedPreferences interface (as defined by [Mobile In-App CMP API v2.0: Transparency
&amp; Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/README.md)) instead of passing them via the new APIs,
and the SDK will read the values as a fallback.

``` pre
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
>To ensure proper monetization and relevant targeting, the SDK should be enabled to send the device information. Setting the `consentRequired` and `purposeConsents` flag correctly will help ensure proper device information is sent. Refer to the table below to determine whether the device details will be passed or not.

The table below describes the actions taken for the
different `purposeConsents` values in combination with `consentRequired`
values.

|  |  deviceAccessConsent= true |deviceAccessConsent= false | deviceAccessConsent= undefined  |
|---|---|---|---|
| `consentRequired=undefined<br>(gdprApplies = undefined)` | The SDK will read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. |
| `consentRequired=true<br>(gdprApplies = true)` | The SDK will read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. |
| `consentRequired=false<br>(gdprApplies = false)` | The SDK will read and pass IDFA/AAID info to server. | The SDK will **not** read and pass IDFA/AAID info to server. | The SDK will read and pass IDFA/AAID info to server. |

Xandr provides three APIs that enable SDK users to set, retrieve and clear U.S. Privacy User Signal Mechanism controls. The IAB Tech Lab has formalized and adopted the "us_privacy" string as the mechanism to encode data about the information disclosed to the user and user elections under various US privacy laws, starting with the CCPA.

## California Consumer Privacy Act (CCPA)

This information will be persisted by the SDK and will be added to each
ad call for applying platform controls.  

Publishers/Consent Management Platforms (CMPs) are free to store these
values in a SharedPreferences interface (as defined by [IAB's CCPA Compliance Mechanism](https://iabtechlab.com/wp-content/uploads/2019/11/US-Privacy-USER-SIGNAL-API-SPEC-v1.0.pdf)) instead
of passing them via the new APIs, and the SDK will read the values as a
fallback.

``` pre
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

[Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Core/CMP%20API%20Specification.md#in-app-details) is a single
protocol designed to streamline transmitting privacy, consent, and
consumer choice signals from websites and apps to ad tech providers.
These signals are packaged in a standardized, easily communicated
payload called a GPP String. The pre-parsed GPP data as well as the GPP
string shall be stored under [NSUserDefaults](https://developer.apple.com/documentation/foundation/nsuserdefaults#1664798?language=objc) (iOS). This will allow
the following:

- Vendors to easily access GPP data.
- GPP data to persist across app sessions.
- GPP data to be portable between CMPs to provide flexibility for a
  publisher to exchange one CMP SDK for another.
- Vendors within an app to avoid code duplication, by not requiring to
  include a GPP string decoder while still enabling all typical use
  cases.  

> [!NOTE]
> If a Publisher chooses to remove a CMP SDK from their app they are responsible for clearing all IABGPP\_\* vestigial values for users so that vendors do not continue to use the GPP data therein.
 
Xandr SDK will then read the values from
NSUserDefault which is then passed to the ad call. Following are the
strings SDK will query from : 

| Key Name | Data type | Description  |
|---|---|---|
| `IABGPP_HDR_GppString` | string | Full consent string in its encoded form. e.g "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN" |
| `IABGPP_GppSID` | string | Section ID(s) considered to be in force. Multiple IDs are separated by underscore, e.g. “2_3” | 
