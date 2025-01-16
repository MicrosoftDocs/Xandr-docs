---
title: Xandr Macros for Data Providers
description: In this article, learn about macros for impressions, ad inventory, mobile impressions, and content object targeting.
ms.custom: data-providers
ms.date: 10/28/2023
---

# Xandr macros for Data Providers

Xandr can populate the following information.

## Macros for all impressions

| Macro | Description |
|:---|:---|
| `${REFERER_URL}` | The refering URL for this inventory if available. |
| `${REFERER_URL_ENC}` | The encoded refering URL. |
| `${USER_ID}` | The Xandr 64-bit character string representing the user for the impression. |
| `${USER_IP}` | The IP address of the user. |
| `${AUCTION_ID}` | The 64-bit character string representing the individual auction that led to the impression. |
| `${USER_AGENT}` | The user agent string from the request's HTTP header. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user (e.g., "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"). |
| `${USER_AGENT_ENC}` | The encoded user agent string from the request's HTTP header. |
| `${SELLER_MEMBER_ID}` | The Xandr member ID for the inventory seller associated with the auction. |
| `${USER_COUNTRY}` | The country or region for the impression's user. |
| `${USER_STATE}` | The state for the impression's user. |
| `${USER_CITY}` | The city for the impression's user. |
| `${USER_DMA}` | The DMA (Designated Market Area) for the impression's user. |
| `${POSTAL_CODE}` | The postal code for the impression's user. |
| `${TIME_ZONE}` | The time zone for the impression's user. |
| `${TAG_ID}` | Provides the placement ID of the tag in this impression. The permission to view tags is part of the seller's visibility profile. Tag IDs will not be visible unless explicitly allowed by the seller. |
| `${EXTERNAL_UID}` | The character string the inventory seller has assigned to the user for the impression. |
| `${EXTENDED_IDS}` | The identifiers (industry IDs and publisher provided IDs) represents the user of the impression. These would be passed as received in the request, with multiple identifiers supported following the format :<br><br>`…&extended_ids=<source_1>,<id_1>\|<source_2>,<id_2>\|…`<br><br>The separators proposed being `,` between the source and the value, and \| between the different IDs type and value pairs. |

## European ad inventory and providing notice, transparency and choice

> [!WARNING]
> In order for our clients to meet their transparency, notice and choice/consent requirements under US state privacy law, GDPR and the existing ePrivacy Directive, Xandr supports the [IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/) (the "Framework").
>
> This is a reference for publishers using the macros to surface notice, transparency and choice to end users located in applicable US states and the EEA and signal approved vendors, and where necessary pass consent and/or Do Not Share/Sell signals to Xandr and demand sources and their vendors through the Xandr Platform.
>
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation. Note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under US state law, European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for legal advice tailored to your business.
> [!NOTE]
> Our [Service Policies](../policies-regulations/index.yml) (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware. These Service Policies have been updated effective 1st of January 2023.

| Macro | Description |
|:---|:---|
| `${GDPR_APPLIES}` | Designates whether GDPR regulations are applied. Specifically, it indicates whether the user is located in a GDPR impacted country or region, or if we have a GDPR-required signal passed with the request. 1 if yes, 0 if no.<br><br>**Warning:** A "0" may be received from an EEA country or region. It is the publisher's choice to signal in this manner. |
| `${GDPR_CONSENT_STRING}` | This is the IAB GDPR consent string. If the GDPR applies, then this will have a list of user approved vendors based on the [IAB GDPR Transparency and Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). |
| `${GPP_SID}` | Designates whether a section (i.e. regulatory framework) of the [Global Privacy Platform](https://iabtechlab.com/gpp) should be applied. Specifically, it indicates whether the user is located in a country or region affected by legislation covered by the GPP. |
| `${GPP_STRING_XXXXX*}` | This is the IAB [Global Privacy Platform](https://iabtechlab.com/gpp) (GPP) string. If a section of the GPP applies, then this will contain framework-dependent information reflecting the consent elections of the user.<br><br>**Note:** * XXXXX can represent any numerical ID. |

## Macros for mobile impressions

| Macro | Description |
|:---|:---|
| `${GEO_LAT }` | The latitude of the user when GPS data is available from a mobile device. |
| `${DERIVED_GEO_LAT}` | An approximation of the latitude of the user truncated down to 3 decimal places of precision. |
| `${GEO_LON}` | The longitude of the user when GPS data is available from a mobile device. |
| `${DERIVED_GEO_LON}` | An approximation of the longitude of the user truncated down to 3 decimal places of precision. |
| `${EXT_APP_ID}` | The external identifier for the application requesting the impression. This is most useful for impressions from mobile apps. |
| `${DEVICE_IFA}` | The unique identifier for advertising (IFA) representing the mobile device. It is defined on the principles of the Interactive Advertising Bureau's (IAB's) guidelines for IFA on Over The Top (OTT) media services. |
| `${DEVICE_IFA_TYPE}` | The source of the unique identifier for advertising (IFA) representing the mobile device. It is defined on the principles of the Interactive Advertising Bureau's (IAB's) guidelines for IFA on Over The Top (OTT) media services. |
| `${DEVICE_MD5}` | The MD5-encrypted unique identifier representing the mobile device. |
| `${DEVICE_SHA1}` | The SHA1-encrypted unique identifier representing the mobile device. |
| `${DEVICE_AAID}` | The Android advertising identifier when the impression is from an Android device. |
| `${DEVICE_OPENUDID}` | The OPENUDID-encrypted unique identifier representing the mobile device. |
| `${DEVICE_APPLE_IDA}` | The Apple advertising identifier when the impression is from an Apple device. |
| `${DEVICE_MAKE_ID}` | The Xandr 64-bit character string representing the make of the mobile device (e.g., "Apple"). |
| `${DEVICE_MODEL_ID}` | The Xandr 64-bit character string representing the model of the mobile device (e.g., "iPhone"). |
| `${CARRIER_ID}` | The Xandr 64-bit character string representing the mobile carrier. |

## Macros for content object targeting

| Macro | Description |
|:---|:---|
| `${CONTENT_ID}` | A unique identifier that the inventory seller has assigned to the content. |
| `${CONTENT_LIVESTREAM}` | Denotes whether the content is live (e.g., stream, live blog). |
| `${CONTENT_GENRE}` | The main genre of the program on which the ad will be played. |
| `${CONTENT_CONTENTRATING}` | The type of rating for the content. |
| `${CONTENT_LEN}` | The length (duration) of the content. |
| `${CONTENT_PROGRAM_TYPE}` | The higher level categorization of the program on which the ad will be played. |
| `${CONTENT_NETWORK}` | The parent company or sub-brand which owns multiple content channels, content brands, or digital properties. |
| `${CONTENT_LANGUAGE}` | The language in which the content is being streamed. |
