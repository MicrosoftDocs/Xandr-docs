---
title: Set Page Options
description: Use the set page options function to set page-level options placements. You can use various parameters as arguments in this function.
ms.custom: seller-tag
ms.date: 10/28/2023
---

# Set page options

This function sets page-level options placements.

```
setPageOpts ({parameters})
```

The parameters listed below can be sent as arguments in the function.

## Parameters

| Parameter | Type | Description |
|:---|:---|:---|
| `dsa` | object | Object that specifies settings in conjunction with the Digital Services Act (DSA). See [DSA Object for details below](#dsa-object).
| `msft` | object | Object that contains request values unique to Microsoft. See [MSFT Object details below](#msft-object). |
| `member` | number | The member ID. |
| `publisherId` | number | The `publisherId` can be used when using an inventory code. This ensures the right publisher is used to help pick the correct default placement. |
| `user` | object | Object that specifies information about an external user. See [User Object](#user-object) details below. |
| `keywords` | object | A set of key/value pairs applicable to all ad slots on this page. Querystring segments are defined by key/value pairs in this object. Keywords that contain hyphens must be enclosed in single quote marks. Best practice is to always surround keywords with single quotes. A maximum of 100 key/value pairs can be defined at the page level. Each tag can have up to 100 additional key/value pairs defined. |
| `disablePsa` | Boolean | Indicates whether all placements should disable PSAs from showing. A value of `true` will disable all PSAs globally. |
| `device` | object | Complex object that declares and overrides the type of device, as populated in the Xandr bid request. See [Device Object](#device-object) details below. |
| `enableSafeFrame` | Boolean | Specifies whether all ads will be served in a SafeFrame container. For more information, see the [SafeFrame API Reference](./safeframe-api-reference.md). |
| `app` | object | Complex object that populates app information. It is an object that holds information related to the application. See [App Object](#app-object) details below. |
| `consentManagement` | object | Specifies whether consent management is enabled for compliance with the transparency, notice and choice/consent requirements under the US state privacy law via the [Global Privacy Platform](https://iabtechlab.com/gpp), GDPR and the ePrivacy Directive. Consent management is enabled by default. See [Consent Management Object](#consent-management-object) details below. |
| `auctionTimeout` | number | The amount of time, in milliseconds, to wait for a bidder to respond to a bid request. |
| `geoOverride` | object | Provides the ability to override IP-based geo location. See [Geo Override Object](#geo-override-object) details below. |
| `schain` | object |  Allows publishers to specify their Supply Chain Object for the request they made to the ad server. Further information about the Supply Chain Object spec and its structure can be found with these links:<br> - [https://iabtechlab.com/sellers-json/](https://iabtechlab.com/sellers-json/)<br> - [https://github.com/InteractiveAdvertisingBureau/openrtb/blob/master/supplychainobject.md](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/master/supplychainobject.md) |
| `us_privacy` | string | A string that conforms to the [IAB CCPA Compliance Framework](https://iabtechlab.com/standards/ccpa/) requirements. See the code sample for this field below. <br><br>**Warning**:<br>This parameter is planned be deprecated at a future date. |
| `pageUrl` | string | This field is set to support progressive web apps that uses AST to show ads in their apps. The development framework generates an invalid referrer, that is blocked by our IQ rules.<br>Publishers using AST in their iOS apps, need to set this field to override the default page URL referrer information (normally derived by AST), to  HTTP(s) value they feel best represents the page. This feature is primarily designed for mobile environments where the referrer information may not reflect typical HTTP page URLs. The feature will only activate when the AST tag is loaded within an iOS app webview. |
| `trackingManagement` | object | Object that specifies values for tracking related features related to the auction and creatives (viewability, usersync, etc). See [TrackingManagement Object](#trackingmanagement-object) details below. |
| `renderingManagement` | object | Object that specifies values for rendering related features, which influence how ads are rendered onto a webpage. See [RenderingManagement Object](#renderingmanagement-object) details below. |
| `content` | object | Object that specifies information about the content where the ads will show. See [Content Object](#content-object) for details below. |

## Objects

### App object

Specifies information about the application.

| Parameter | Type | Description |
|:---|:---|:---|
| `appid` | object | Object that defines the application identification information. |

Here's an example:

```
apntag.setPageOpts({
        app: {
                appid: 'com.mypackage.myapp'
        }
});
```

### DSA object

Specifies information related to the Digital Services Act. For the ideal values to use for each of the fields, refer to the [IAB Spec](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/main/extensions/community_extensions/dsa_transparency.md)

| Parameter | Type | Description |
|---|---|---|
| `dsarequired` | number | Flag to indicate if DSA information should be made available.
| `pubrender` | number | Flag to indicate if the publisher will render the DSA Transparency info.
| `transparency` | Array of objects | Array of objects of the entities that applied user parameters and the parameters they applied.

### MSFT object

Specifies information and settings unique to Microsoft.

| Parameter | Type | Description |
|---|---|---|
| `toptout` | number | A number that represents the status of the end user's MSFT optout choices (eg `0`, `1`, etc) |

### Schain object

The feature in AST allows for publishers to perform an optional syntax check on the schain they specify in the config parameter. The syntax criteria is based on the IAB specification for the schain object.

- If the publisher enables the strict option, the config schain object will be checked exactly and if there is an error in the structure, an error message from AST will be thrown in the console and the schain object will not be included in the request to the adserver.
- If the publisher enables the relaxed option, the config schain object will be checked. If is something wrong, a warning message will be displayed in the browser console, but the schain object will still be included in the request to the adserver.
- If the publisher enables the off option, the config schain object will not be checked at all. It will simply be included in the request to the adserver, whether it was correctly formatted or not.

> [!NOTE]
> You need to have the AST debug flag enabled to see the messages in the console.

Here's an example:

```
schain: {
  validation: 'strict',  // strict, relaxed, or off - strict is default
  config: {
    ver: '1.0',
    complete: 0,
    nodes: [{
      asi: 'testasi.com',
      sid: 'test123sid',
      hp: 1
    }]
  }
}
```

### User object

Specifies information about an external user to whom the ads will be shown.

| Parameter | Type | Description |
|:---|:---|:---|
| `age` | number | The age of the user. |
| `dnt` | Boolean | Do not track flag. Indicates if tracking cookies should be disabled for this auction:<br> - `true` (disable cookies)<br> - `false` (Default)<br><br>**Note**: When `dnt:true` , user data will not be available throughout the auction, regardless of sending external UID or Xandr UUID. The ID would appear as `-1` in LLD, representing opted-out. |
| `externalUid` | string | Specifies a string that corresponds to an external user ID for this user.<br><br>**Warning**: <br>`externalUid` should only be used in cookieless environments. Application outside of that may result in decreased user match rate (impacting retargeting) and / or increased user blocklisting over time. |
| `gender` | string | Specifies the gender of the user:<br> - `0`: unknown<br> - `1`: male<br> - `2`: female |
| `language` | string | The two-letter ANSI code for this user's language; for example, `EN`. |
| `segments` | array of numbers | Specifies the segments to which the user is a member. |
| `userIds` | array of objects | An array containing objects that hold userId parameters. See [User ID Object](#user-id-object) details below for definitions. |
| `coppa` | boolean | When enabled, this includes the coppa flag to the auction request. |

### User ID object

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | string | The cookie or platform native identifier |
| `type` | string | The source value of the provider that provides the included ID. Supported identity solutions:<br> - `criteo`: criteo's identity solution.<br> - `liveramp`: Liveramp's identity solution.<br> - `netid`: european cross-device enabled advertising identifier.<br> - `ttd`: the trade desk 1.0 identity solution.<br> - `uid2`: uid2 identity solution. |
| `extendedIDs` | type | The publisher defined first party IDs. |
| `eids` | array of objects | The eids value is only compliant with the extendedID type (all other defined types should use the existing id string defined above). The objects inside this eids array have 2 parameters, id and source:<br> - `id`: identical to the existing ID value in its purpose and description. <br> - `source`: the source or technology provider utilized by the publisher to handle the first party ID; generally expressed as a domain. See the example below. |

### Pass universal IDs in Monetize

You can pass a universal ID to Monetize through AST.js using one of two methods: the **mapped identifier method** (older) or the **`extendedIDs` method** (newer).

#### Mapped identifier method

This method allows you to pass a limited number of Universal IDs. The list of supported IDs is hardcoded in the `AST.js` code. Use this method when the Universal ID is among the supported types.

**Example JSON**

```

{
  "type": "liveramp",
  "id": "0d7e95c7-4783-4278-acf9-99809d0c5a61"
}
```

#### `ExtendedIDs` method

The `extendedIDs` method is more flexible and supports all [Universal IDs](../monetize/universal-id-support-matrix-for-sellers.md) and Publisher Provided Identifiers (PPIDs). Use this method to pass identifiers dynamically.

**Example JSON**

```
{
  "type": "extendedIDs",
  "eids": [
    {
      "source": "liveramp.com",
      "id": "2d7e95c7-4783-4278-acf9-99809d0c5a62"
    }
  ]
}
```

In this example:

- `source`is the domain or provider that manages the Universal ID.
- `id`is the identifier provided by the source.

The `extendedID` method is recommended for all current and future Universal ID formats. It offers flexibility for publishers who want to handle various first-party ID solutions.

#### Choose the right method

- Use the mapped identifier method only if your Universal ID is supported by the legacy AST.js mapping.
- Use the `extendedID` method for broader compatibility and future-proofing.

> [!NOTE]
> You can plan your migration to the `extendedIDs` method to ensure compatibility with all current and future identity solutions.

### Device object

Specifies a mobile device on which the ads will be shown.

| Parameter | Type | Description |
|:---|:---|:---|
| `deviceId` | object | Object that defines the device identification information; includes the following parameters:<br> - `idfa`: The Apple advertising identifier for iOS devices running iOS 6+.<br> - `aaid`: The Google advertising identifier for Android devices as retrieved from Google Play services.<br> - `sha1udid`: The SHA1 hash of the `ANDROID_ID`.<br> - `md5udid`: The The MD5 hash of the `ANDROID_ID`.<br> - `windowsadid` - The Microsoft advertising identifier for Windows devices. |
| `deviceType` | string | Specifies the type of device on which the ad will be shown (such as `phone` or `tablet`). |
| `useragent` | string | The user agent string from the device browser. |
| `geo` | object | Object that defines the location of the device; includes the following parameters:<br> - `lat`: Device latitude (a number, such as `45.5`).<br> - `lng`: Device longitude (a number, such as `-122.7`).<br> - `country`: Country for the device. Uses the three-character [ISO 3166-1 alpha-3](https://www.iso.org/obp/ui/#iso:pub:PUB500001:en) codes.<br> - `region`: Device region.<br> - `city`: Device city.<br> - `zip`: Device ZIP code. |
| `ip` | string | The device's IP address. |
| `make` | string | The device model; for example, `Apple`. |
| `model` | string | The device make; for example, `iPhone`. |
| `os` | string | The device operating system. |
| `osVersion` | string | The version of the device operating system. |
| `carrier` | string | The carrier for the device. |
| `connectionType` | number | The connection type:<br> - `0`: Unknown<br> - `1`: WiFi<br> - `2`: WAN |
| `mcc` | string | The mobile country code, as specified by the ITU. |
| `mnc` | string | The mobile network code, as specified by the ITU. |
| `devTime` | number | The time on the device (in UNIX Time). |

### Content Object

| Parameter | Type | Description |
|:---|:---|:---|
| `language` | string | The two-letter ANSI code for this user's language. For example, `'EN'`. |

### TrackingManagement object

| Parameter | Type | Description |
|:---|:---|:---|
| `native` | object | Object that contains settings related to native types specifically. |
| `native.loadViewabilityScriptAt` | string | Permitted values:<br> - `impression`<br> - `adresponse` <br><br>**Default**: `adresponse`<br>The adresponse time is recorded when the ad is received by AST. It is the historical setting.<br><br>The new impression time is recorded closer to the impression event. This may be more desirable to certain publishers who rely on native viewability metrics. |
| `userSync` | object | Object that contains settings related to the AST `userSync` feature. |

### RenderingManagement object

| Parameter | Type | Description |
|:---|:---|:---|
| `insertWrapperDiv` | boolean | When enabled, AST adds an additional div element between the main AST `utif` div and the AST iframe (or safeframe) container for all ad slots. This option is useful for publishers who wish to customize or control the contents of the ad container further without modifying the main div container.<br>**Default**: `false` |
| `sandboxAdIframe` | boolean | When enabled, AST adds and populates the HTML sandbox attribute for the AST iframe (or safeframe) container for all ad slots using the values from the appropriate `sandboxAttributes` parameter.<br>**Default**: `false` |
| `sandboxAttributes` | array of strings | The values of these attributes are applied to the HTML sandbox attribute for the AST iframe (or safeframe) ad containers when the appropriate `andboxAdIframe` setting is set to true. For suitable values to include in this array, see the HTML sandbox documentation. If enabled, it is advised to include at least `allow-same-origin` and `allow-scripts` to ensure that the contents of the iframe may function properly (omitting these values may result in some warnings in the browser console). |

### userSync object

> [!NOTE]
> For more details about `userSync` object, go to [User Sync](./user-sync.md) page.

| Parameter | Type | Description |
|:---|:---|:---|
| `syncEnabled` | boolean | Enables or disables the logic in AST that loads the `userSync` script after the auction ends.<br>**Default**: `true` |
| `syncDelay` | number | Specifies the amount of time (in milliseconds) that AST waits after the auction ends before loading the `userSync` script.<br>**Default**: `3000` |
| `publisherId` | number | Numeric identifier for the publisher entity used for the auction on this page. It includes the value that is passed to the `userSync` script, which provides more information downstream. |
| `sellerId` | number | Numeric identifier of the seller entity used for the auction on this page. It includes the value that is passed to the `userSync` script, which provides more information downstream. |

Here's an example

```
apntag.setPageOpts({
    member: 958,
    user: {
        age: 25,
        externalUid: '10',   
                userIds: [{ "type": "criteo", "id": "_fl7bV96WjZsbiUyQnJlQ3g4ckh5a1N", }, // Criteo Identifier
                  { "type": "ttd", "id": "00000111-91b1-49b2-ae37-17a8173dc36f" }, // Trade Desk Identifier
                  { "type": "netid", "id": "999888777" }, // NetID Identifier
                  { "type": "liveramp", "id": "AjfowMv4ZHZQJFM8TpiUnYEyA81Vdgg" }, //Liveramps's Identifier
                  { "type": "uid2", "id": "234123424" }, //UID2's Identifier
                  { "type": "extendedIDs", "eids": [{ "id": "abc123def345", "source": "mySampleDomain.com" }] }, // publisher first party IDs
                ], 
        segments: [1, 2],
        gender: 0,
        dnt: true,
        language: 'EN'
    }
    keywords: {
        genre: ['rock', 'pop']
    },
    disablePsa : true,
    enableSafeFrame : true,
    device : {
        deviceId : {
            idfa : 'String',
            aaid : 'String',
            md5udid : 'String',
            sha1udid : 'String'
        },
        deviceType : 'String',
        useragent : 'String',
        geo : {
            lat : 0.4,
            lng : 0.5,
            country : 'USA',
            region : 'String',
            city : 'String',
            zip : 'String'
        },
        ip : 'String',
        make : 'String',
        model : 'String',
        os : 'String',
        osVersion : 'String',
        carrier : 'String',
        connectionType : 0,
        mcc : 'String',
        mnc : 'String',
        devTime : 12345
    },
    auctionTimeout: 3000,
    pageUrl: 'http://www.samplesite.com/testpage.html',
    trackingManagement: {
     native: {
       loadViewabilityScriptAt: 'impression'
     },
    renderingManagement: {
      insertWrapperDiv: true,
      sandboxAdIframe: true,
      sandboxAttributes: ['allow-same-origin', 'allow-scripts', 'allow-presentation']
      },
     userSync: {
       syncEnabled: true,
       syncDelay: 4000,
       publisherId: 12345,
       sellerId: 123
      }
     }
 });
```

### Geo override object

Use this object to override the auction's geographic information. The supplied country code and zip code will be used to look up all geographic attributes to determine location.

| Field | Type | Description |
|:---|:---|:---|
| `countryCode` | string | Required. A two-character country code. |
| `zip` | string | Required. Zip code must be at least one character. |

Here's an example

```
apntag.setPageOpts({      
  ... // other settings
  geoOverride: {
    countryCode: 'US',
    zip: '10000'
  }
})
```

### Consent management object

Use this object to specify whether consent management is enabled for compliance with the transparency, notice and choice/consent requirements under US state privacy laws, GDPR, the ePrivacy Directive and [IAB's U.S. Privacy User Signal Mechanism (USP)](https://iabtechlab.com/wp-content/uploads/2019/10/CCPA_Compliance_Framework_US_Privacy_USER_SIGNAL_API_SPEC_IABTechLab_DRAFT_for_Public_Comment.pdf), which currently covers the [California Consumers Privacy Act (CCPA)](https://oag.ca.gov/privacy/ccpa). Consent management is enabled by default.

> [!WARNING]
>
> In order for our clients to meet their transparency, notice and choice/consent requirements under US state privacy laws, the GDPR, the existing ePrivacy Directive, Xandr supports the [Global Privacy Platform](https://iabtechlab.com/gpp)(GPP) and the [IAB Europe Transparency Consent Framewor](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/) (the [IAB's U.S. Privacy User Signal Mechanism (USP)](https://iabtechlab.com/wp-content/uploads/2019/10/CCPA_Compliance_Framework_US_Privacy_USER_SIGNAL_API_SPEC_IABTechLab_DRAFT_for_Public_Comment.pdf) will be deprecated in 2023).
>
> This is a reference for publishers using AST to surface notice, transparency and choice to end users located within regions covered by the above mentioned policies and signal approved vendors and, where necessary, pass consent, to Xandr and demand sources and their vendors through Xandr's platform.
>
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation. Note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
>
> Note our [Part of Service Policies](../policies-regulations/index.yml) (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware.

| Parameter | Type | Description | Default |
|:---|:---|:---|:---|
| `disabled` | Boolean | Set to true to disable consent management functionality. | `False` |
| `timeout` | Integer | The amount of time (in milliseconds) to wait for the CMP to respond. | `10000` |

### Disabling consent management

Xandr provides the option to disable all consent management or individual ones per the user's needs.

| Options | Examples |
|:---|:---|
| Disable all consent management | ```//disables all consent management apntag.setPageOpts({ ... // other settings consentManagement: { disabled: true, timeout: 10000 } })```                |
| Disable GDPR only | ```apntag.setPageOpts({ consentManagement: { timeout: 5000, tcf : { disabled: true } } });``` |
| Disable GPP only | ```apntag.setPageOpts({ consentManagement: { timeout: 5000, gpp : { disabled: true } } });```       |

The following describes the functionality of AST in supporting GPP and GDPR compliance when `consentManagement` is enabled:

- During the Load Tags function call, the AST tag will attempt to fetch the consent data from the IAB-compliant Consent Management Platforms (CMP).
- When it’s time for the AST tag to call ImpBus, the consent information is included in the `/ut` `POST` request. Specifically, the consent information is stored under the `POST`’s data object as:

> [!NOTE]
> The request-building process is paused during the above execution in order to allow new users a chance to complete their consent information. The process will stop waiting after a specified timeout period (default 10 seconds) and finish building the request.

```
gdpr_consent : {
    consent_string: 'abc123',
    consent_required: true|false
},
us_privacy: "1YNY"
```

When the CMP fetch fails or the timeout period expires, the `consentManagement` code will log a warning message to the browser console, package a consent object in the following manner and include it into the AST request as described.

```
gdpr_consent : {
    consent_string: undefined,
    consent_required: undefined
},
gpp_sid: [5]
```

When AST detects TCF 2.0 it will rely on events generated by the CMP. The consent string will be retrieved when any of the following conditions are met:

- The event generated is `useractioncomplete` or `tcloaded`.

- The event generated is `cmpuishown` and `purposeOneTreatment` flag is set to `true` in the available TCF string.

- The only event generated is `cmpuishown` and a time out occurs.

  In TCF v2.0 if the `gdprApplies` flag is set to `true` and Purpose One consent is not granted then AST will not include cookies in the `/ut` `POST` request.

## Global privacy platform

In order to comply with multiple US state privacy laws, Xandr supports the Global Privacy Platform. When AST detects GPP it will rely on events generated by the CMP. The GPP string will be retrieved when any of the following conditions are met:

- The event `sectionChange` has occurred - This event is called whenever the status or content of a section changes (e.g. consent is obtained).
- The `cmpStatus` is loaded and the `cmpDisplayStatus` does not equal visible - This means the CMP code has finished loading (out of the stub phase) and the CMP is not visible to the end-user (which typically means the CMP has prior consent information available).
