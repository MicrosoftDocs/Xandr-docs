---
title: Global Privacy Platform
description: Explore a global privacy platform efficiently managing user consent signals across diverse global privacy settings.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Global privacy platform

The [Global Privacy Platform](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform) (GPP) is a protocol that helps to consolidate the management of different user consent signals from a variety global privacy jurisdictions. It is a communication layer that interacts with frameworks such as the Transparency and Consent Framework ([TCF](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/tree/master/TCFv2)) and the US Privacy API ([USPAPI](https://github.com/InteractiveAdvertisingBureau/USPrivacy/blob/master/CCPA/USP%20API.md)) to convert multiple signals into a single API, thereby making communication between ad tech vendors
more efficient.

In order to be compliant with state legislation in the United States, Microsoft Advertising will support the '[US-States](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/tree/main/Sections/US-States)' section of the GPP as of 01.01.23. That means that publishers and advertisers operating in theUnited States will have an industry-accepted method of maintaining legal compliance and respecting the privacy of their users.

## How does the GPP work

The GPP works by translating consent signal frameworks into a signal API. It first ingests multiple signals and then creates a single ingestible signal for downstream vendors to interpret. For example, if a page is using both the TCF and the USPAPI, the GPP will convert the signals into a single GPP string, as shown below.

  :::image type="content" source="media/gpp-works.png" alt-text="Screenshot that illustrates GPP's consolidation of signals from both TCF and USPAPI into a unified GPP string.":::

The GPP string always consists of a 'header' and then the main string, which is divided into 'sections'. Each section relates to a local privacy framework. In the example above, the GPP string consists of TCF and USPAPI (CCPA) sections, as well as a header which provides information on which sections are included in the main string.

## Consent management platforms

In general, website owners can work with Consent Management Platforms (CMPs) to create and transmit the consent preferences of their users. The CMP is responsible for surfacing a banner (the so called 'cookie banner') on the website which presents users with the options they have with regards to the usage of their personal information. The CMP then
converts the consent choices of the user into a string, depending on the framework being used. CMPs which use the GPP are able to surface banners which include multiple legislative frameworks from different jurisdictions to end users and then to translate those choices into a single GPP string. They are also able to signal the jurisdiction of the end user to downstream vendors, so those vendors can decide how to apply global privacy laws.

## How we apply GPP controls

In general, ad tech vendors need to know two things in order to process privacy controls:

1. The local legislative framework of the user (for example, if the user is in the EU, then it's GDPR.)
1. For which data processing purposes the user has granted consent (consent elections) or the legal bases for processing data which do/do not apply.

In the GPP framework, this information is conveyed by 'applicable sections' (which sections of the string should be enforced) and the GPP string itself. Taken together, these parameters allow Microsoft Advertising to understand the consent choices of the end user and to know which privacy law to apply.

## AD call examples

**Prebid**

In order to use the GPP, website owners need to:

1. Work with a GPP-enabled CMP
1. Update to the latest version of prebid.js
1. Install the consent management module
1. Update the prebid config, as shown below:

    ```
    var pbjs = pbjs || {};
    pbjs.que = pbjs.que || [];
    pbjs.que.push(function() {
    pbjs.setConfig({
      consentManagement: {
        gpp: {
          timeout: 10000,    // time in ms
          cmpApi: 'iab'      // activates logic for module, leaving gpp object out keeps module off
        }
      }
    });
    ```

The ad call made to Microsoft Advertising will then be updated to include the GPP params as outlined below:

```
{
    "privacy": {
        ...
        "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN",
        "gpp_sid": [2],
        ...
    }
}
```

In the above example, the GPP string contains sections for the TCF and the US Privacy (V1; CPPA) frameworks, but the 'applicable section' is section 2, which corresponds to the TCF. See [here](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Sections/Section%20Information.md#section-ids) for the list of section ids.

**ast.js**

In order to use the GPP, website owners need to:

1. Work with a GPP-enabled CMP
1. Update to the latest version of ast.js
1. Modify the setPageOpts, as shown below:

    ```
    apntag.setPageOpts({
      consentManagement: {
        disabled: false       // global on/off switch; default is false (module is on)
        timeout: 10000,       // time in ms
        gpp: {
          disabled: false    // local on/off switch gpp module, default is false (module is on)
        }
      },
    });
    ```

The ad call made to Microsoft Advertising will then be updated to include the GPP params as outlined below:

```
{
    "privacy": {
        ...
        "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN",
        "gpp_sid": [2],
        ...
    }
}
```

In the above example, the GPP string contains sections for the TCF and the US Privacy (V1; CPPA) frameworks, but the 'applicable section' is section 2, which corresponds to the TCF. See [here](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Sections/Section%20Information.md#section-ids) for the list of section ids.
Further documentation can be found [here](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/tree/main/Sections).

**URL-based calls (/ttj, /ptv, etc.)**

Clients using URL-based calls can include GPP parameters as demonstrated below:

```
https://ib.adxns.com/ttj?id=[PLACEMENT_ID]&size=[SIZE]&gpp=[GPP_STRING]&gpp_sid=[GPP_SID]
```

For example, an ad call may look like this:

```
https://ib.adxns.com/ttj?id=12345678&size=300x250&gpp=DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN&gpp_sid=2
```

**Inserting GPP parameters into creative third-party tags**

You can insert GPP parameters into your creative third-party tags, impression trackers, landing page URLs, and third-party pixels for reporting and optimization purposes using the GPP-specific creative macros as demonstrated below:

```
https://lensmaster.com/newsunglasses?gpp=${GPP_STRING_XXXXX*}&gpp_sid=${GPP_SID}
```

\* XXXXX can represent any numerical id

> [!NOTE]
> Third-party partners must support GPP in order for this to work. You should contact the third-parties you work with before updating your creative macros.
