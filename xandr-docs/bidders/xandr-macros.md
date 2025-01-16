---
title: Xandr Macros
description: Explain how macros populate URLs, acting as variables for useful information in ad creatives, revealing their replaced values during ad calls.
ms.date: 10/28/2023
---

# Xandr macros

Macros are used to populate URLs (such as those found in creatives) with useful information. They are essentially variables that are expanded by our ad server with whatever their actual value is at the time of the ad call.

This page contains information about all of the macros we support. For each macro, we list the information that that macro is replaced with during the ad call.

> [!TIP]
> For more control over URL encoding and decoding, see the section on [Function Macros](xandr-macros.md#function-macros).
>
> For additional examples about how macros may be > used when uploading creatives, refer to the [Creative Service](creative-service.md) page.

## Creative macros

> [!WARNING]
>  
> OpenRTB macros (like `${AUCTION_PRICE`}) are not supported when adding creatives using the [Creative Service](creative-service.md). They are only supported on the [Bid Response](incoming-bid-response-from-bidders.md).

Xandr supports the following creative macros when adding creatives using the [Creative Service](creative-service.md).

| Macro | Description |
|--|--|
| `${CLICK_URL}` | The click tracking URL. |
| `${CLICK_URL_ENC}` | The encoded click tracking URL (only necessary for some third party adservers) |
| `${AUCTION_ID}` | The 64-bit character string representing the individual auction that led to the impression. |
| `${TAG_ID}` | The Xandr TinyTag ID that originated the Bid Request |
| `${EXT_APP_ID}` | The external identifier for the application requesting the impression. This is most useful for impressions from mobile apps. |
| `${CREATIVE_ID}` | The creative ID that won the impression. |
| `${DEAL_ID}` | The Xandr Deal ID associated with the winning bid, if applicable. If there is no deal, this will return 0. |
| `${ECP}` | The publisher side Estimated Clear Price for the auction. |
| `${RESERVE_PRICE}` | The reserve price set by the publisher. |
| `${SESSION_FREQ}` | The session frequency for the user. |
| `${AGE}` | The age of the user (if available). Integer (e.g., 26) or 0. |
| `${GENDER}` | The gender of the user (if available). Values are 'f','m','u'. |
| `${CACHEBUSTER}` | A random number string used to limit caching of the URL |
| `${PRICE_PAID}` | The price paid for this impression. (As opposed to the price bid, before price reduction.) |
| `${SECOND_PRICE}` | The price that represent the second highest bid in auction. Expressed in floating point number format (e.g. 1.23) |
| `${REFERER_URL}` | If available, the referring URL for this inventory. <br>**Note**: This field is deprecated (as of May 2016). Use ${REFERER_URL_ENC} instead. |
| `${REFERER_URL_ENC}` | The encoded referring URL. |
| `${BID_PRICE}` | The price bid for this impression as opposed to the price paid after price reduction. |
| `${TAG_CODE1}` | Integration code set on the placement. |
| `${TAG_CODE2}` | Additional integration code set on the placement. |
| `${INV_SOURCE_ID}` | **Deprecated**. |
| `${USER_ID}` | The Xandr 64-bit character string representing the user for the impression. |
| `${USER_IP}` | The IP address of the user. |
| `${IS_PREVIEW}` | If we are "previewing" the creative, we can pass a flag to the third-party server so they don't count it as a production impression. If true, we pass a "1"; if false, we pass a "0". |
| `${SELLER_MEMBER_ID}` | The member that owns the publisher where the impression originates. |
| `${SEG_IDS}` | IDs of the segments belonging to the winning buyer in this user's cookie (in order of last seen time). Note that this macro does not work for shared segments (such as those owned by a third party data provider). |
| `${SEG_CODES}` | Codes for the segments belonging to the winning buyer in this user's cookie (in order of last seen time). Note that this macro does not work for shared segments (such as those owned by a third party data provider). |
| `${DATACENTER}` | Data center ID (1 = NYM, 2 = LAX, 3 = AMS) |
| `${USER_CITY}` | Character string of the user's city |
| `${USER_STATE}` | Character string of the user's state (2 letter abbreviation. FIPS 10-4 outside US and Canada) |
| `${SITE_ID}` | ID of the site the impression is being served on |
| `${PUBLISHER_ID}` | ID of the publisher selling the impression |
| `${PUBLISHER_CODE}` | Code of the publisher selling the impression (if available) |
| `${CREATIVE_CODE}` | Code of the creative served (if available) |
| `${CREATIVE_SIZE}` | Width x Height of the creative served (e.g., `"300x250"`) |
| `${WIDTH}` | Width of the creative served |
| `${HEIGHT}` | Height of the creative served |
| `${SUPPLY_TYPE}` | This macro will be populated with a numeric value that denotes the supply type of the impression. Allowed values include:<br>0: web<br>1: mobile web<br>2: mobile app<br>4: toolbar |
| `${TIMESTAMP}` | The UNIX timestamp for the auction. |
| `${USER_AGENT}` | The user agent string from the request's HTTP header. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user (e.g., "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"). |
| `${USER_AGENT_ENC}` | The encoded user agent string from the request's HTTP header. |
| `${EXTENDED_IDS}` | The identifiers (industry IDs and publisher provided IDs) represents the user of the impression. These would be passed as received in the request, with multiple identifiers supported following the format: <br><br>`…&extended_ids=<source_1>,<id_1>\ <source_2>,<id_2>\ …`<br><br> The separators proposed are commas between the source and the value, and a pipe symbol between different ID types and value pairs. |

### European Ad inventory and providing notice, transparency and choice

> [!WARNING]
> In order for our clients to meet their transparency, notice and choice/consent requirements under US state privacy law, the GDPR and the existing ePrivacy Directive, Xandr supports [the IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/) (the "Framework").
>
> This is a reference for publishers using the macros to surface notice,transparency and choice to end users located in applicable US states and the EEA and signal approved vendors, and where necessary pass consent and/or Do Not Share/Sell signals to Xandr and demand sources and their vendors through Xandr's platform.
>
> This resource should not be construed as legal advice and Xandr makes no guarantees about compliance with any law or regulation.  Please note that because every company and its collection, use, and storage of personal data is different, you should also seek independent legal advice relating to obligations under US state law, European regulations, including the GDPR and the existing ePrivacy Directive. Only a lawyer can provide you with legal advice specifically tailored to your situation. Nothing in this guide is intended to provide you with, or should be used as a substitute for, legal advice tailored to your business.
>
> Note that our [Part of Service Policies](../policies-regulations/index.yml) (for Buying, Selling, and Data Providers) include privacy-specific obligations of which you should be aware. These Service Policies have been updated effective 1st of January 2023.

| Macro | Description |
|--|--|
| `${GDPR_APPLIES}` | Designates whether GDPR regulations are applied. Specifically, it indicates whether the user is located in a GDPR impacted country or region, or if we have a GDPR-required signal passed with the request. 1 if yes, 0 if no. |
| `${GDPR}` | Offers same functionally as `${GDPR_APPLIES}`. |
| `${GDPR_CONSENT_STRING}` | This is the IAB GDPR consent string. If the GDPR applies, then this will have a list of user approved vendors based on the [IAB GDPR Transparency and Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). |
| `${GDPR_CONSENT}` | This is the IAB GDPR consent string according to TCF 1.0 official specification. It is included to maintain backwards compatibility for client convenience. |
| `${GDPR_CONSENT_[0-9]+}` | For example, GDPR_CONSENT_1, GDPR_CONSENT_12345 etc. These all resolve to the same GDPR consent string as explained above in `'${GDPR_CONSENT_STRING}'`. |
| `${GPP_SID}` | Designates whether a section (i.e. regulatory framework) of the [Global Privacy Platform](https://iabtechlab.com/gpp/) should be applied. Specifically, it indicates whether the user is located in a country or region affected by legislation covered by the GPP. |
| `${GPP_STRING_XXXXX*}` | This is the IAB [Global Privacy Platform](https://iabtechlab.com/gpp/) (GPP) string. If a section of the GPP applies, then this will contain framework-dependent information reflecting the consent elections of the user.<br>**Note**: * XXXXX can represent any numerical id |

The following table contains reserved macro names that are not for use by Bidder clients. They will cause conflicts with other Xandr technologies and are not to be used for custom macros.

| Reserved Macro Name |
|--|
| `${ADV_CODE}` |
| `${ANCOST}` |
| `${BASE64_UID_ENC}` |
| `${BASE64_UID}` |
| `${BIDPRICE}` |
| `${CND}` |
| `${CONTENT}` |
| `${CREATIVE_HEIGHT}` |
| `${CREATIVE_WIDTH}` |
| `${FLASH_BACKUP_URL}` |
| `${FLASHVARS}` |
| `${IE7_FLASH_JS_URL}` |
| `${IF_CALLBACK_URL}` |
| `${IO_CODE}` |
| `${IO_ID}` |
| `${IS_PREVIEW_COL}` |
| `${IT_CALLBACK_URL}` |
| `${MATCHED_PROFILE_CODE}` |
| `${MATCHED_PROFILE_ID}` |
| `${MEDIA_SUBTYPE}` |
| `${MEDIA_TYPE}` |
| `${MEDIA_URL_ENC}` |
| `${MEDIA_URL}` |
| `${PMT_RULE_CODE}` |
| `${POP_CALLBACK_URL}` |
| `${POP_CREATIVE_MAXIMIZED}` |
| `${POP_IS_PREPOP}` |
| `${POP_IS_TAG_INITIATED}` |
| `${POP_WINDOW_LOCATION}` |
| `${POP_WINDOW_MENUBAR}` |
| `${POP_WINDOW_RESIZABLE}` |
| `${POP_WINDOW_SCROLLBARS}` |
| `${POP_WINDOW_STATUSBAR}` |
| `${POP_WINDOW_TITLE}` |
| `${POP_WINDOW_TOOLBARS}` |
| `${PRICE_PAID_ENCR}` |
| `${PT1}` |
| `${PT2}` |
| `${PT3}` |
| `${PT4}` |
| `${PT5}` |
| `${SECOND_LEVEL_CATEGORY_ID}` |
| `${SEG_CODES_COL}` |
| `${SITE_CODE}` |
| `${SSP_DATA}` |
| `${TAG_HEIGHT}` |
| `${TAG_WIDTH}` |
| `${TOP_LEVEL_CATEGORY_ID}` |
| `${TRACKER_ID}` |
| `${UID}` |
| `${USER_COUNTRY}` |
| `${VENUE_ID}` |

## Mobile macros

| Macro | Description |
|--|--|
| `${GEO_LAT}` | The latitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd" (e.g., `+12.345` or `-45.123`), where south is represented as negative. There can be a maximum of 5 decimal places of precision. |
| `${GEO_LON}` | The longitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd" (e.g., `+12.345` or `-45.123`), where west is represented as negative. There can be a maximum of 5 decimal places of precision. |
| `${EXT_APP_ID}` | The external identifier for the application requesting the impression. This is useful only for impressions from mobile apps. |
| `${DEVICE_MD5}` | The MD5-encrypted unique identifier representing the mobile device. |
| `${DEVICE_SHA1}` | The SHA1-encrypted unique identifier representing the mobile device. |
| `${DEVICE_OPENUDID}` | The OPENUDID-encrypted unique identifier representing the mobile device. |
| `${DEVICE_ODIN}` | The [ODIN](https://code.google.com/archive/p/odinmobile/)-encrypted unique identifier representing the mobile device. |
| `${DEVICE_AAID}` | The Android advertising identifier, when the impression is from an Android device. |
| `${DEVICE_APPLE_IDA}` | The Apple advertising identifier, when the impression is from an Apple device. |
| `${DEVICE_MAKE_ID}` | The Xandr integer representing the ID of the make of the mobile device (e.g., `26`).  For a complete list of mobile device make IDs, see the [Device Make Service](device-make-service.md). |
| `${DEVICE_MODEL_ID}` | The Xandr integer representing the ID of the mobile device model (e.g., 301). For a complete list of mobile device model IDs, see the [Device Model Service](device-make-service.md). |
| `${DEVICE_WIN_ID}` | The Windows Ad ID for the device on which this impression occurred (if applicable). |
| `${CARRIER_ID}` | The Xandr integer representing the mobile carrier ID. For a complete list of mobile carrier IDs, see the [Carrier Service](carrier-service.md). |
| `${SUPPLY_TYPE}` | This macro will be populated with a numeric value that denotes the supply type of the impression. Allowed values include:<br>0: web<br>1: mobile web<br>2: mobile app<br>4: toolbar |

## Function macros

A function macro a special kind of macro that performs a function on another macro. Function macros can be used in combination with any other creative macro, including custom macros, although if they are not recognized at render time, they will not be translated and the function will not be called.

Xandr currently supports the `{$URL_ENC}` function macro, which can be used for a variety of purposes related to encoding.  A key use case is when a URL needs to be passed from ad server to ad server via a creative macro, and due to the presence of unsupported characters in standard URL formatting, must be encoded at various steps of the process.

The macro takes the following form:

```
 ${URL_ENC(${MACRO_NAME},#)} 
```

where `${MACRO_NAME}` is the macro to be encoded and \# is the integer `1`, `2`, or `3`, representing the number of times to encode the contents. Note that more than three encodings are not supported.

> [!NOTE]
> Each encoding corresponds to a step in the redirect chain, as well as how a given third-party click
> tracker works with the macro. Double encoding will usually be needed for final destination URLs when a second ad server is involved, and triple encoding for a third ad server.
>
> To determine whether you will need to use single, double, or triple encoding, you should check with your third-party click tracker and then test your `URL_ENC` macro to ensure it works. If your macro is not working, one consequence of this may be link breakage, which will result in users not reaching the intended destination URL.

## Encoding examples

### To encode click URL once

```
${URL_ENC(${CLICK_URL},1)} 
```

If  `https://xandr.com` is passed as the click URL, using `${URL_ENC(${CLICK_URL},1)}` to single encode the URL would result in `https%3A%2F%2Fxandr.com`  populating the creative.

**To encode media URL once:**

```
 ${URL_ENC(${MEDIA_URL},1)} 
```

**To encode media URL twice:**

```
 ${URL_ENC(${MEDIA_URL},2)} 
```

**To encode a custom macro called ADFORMAT once:**

```
${URL_ENC(${ADFORMAT},1)}
```
