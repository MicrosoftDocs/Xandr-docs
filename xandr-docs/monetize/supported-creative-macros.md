---
title: Microsoft Monetize - Supported Creative Macros
description: Explore creative macros that can be used for all, mobile, and video impressions. Additionally, privacy and function macros are supported as well.
ms.date: 10/28/2023
---

# Microsoft Monetize - Supported creative macros

We have creative macros that can be used for all, mobile, and video impressions. We also support privacy and function macros.

> [!NOTE]
> Creative macros are case-sensitive and aren't available for piggyback conversion pixels.

## Creative macros for all impressions

The following macros can be used for all impressions:

| Macro | Description |
|---|---|
| `${CLICK_URL}` | The click tracking URL. For example: `https://xandr.com` |
| `${CLICK_URL_ENC}` | The encoded click tracking URL (only necessary for some third-party ad servers). For example: `https%3A%2F%2Fxandr.com` |

The following macros can be used in creative third-party tags and landing page URLs:

| Macro | Description |
|---|---|
| `${ADV_CODE}` | The code of the advertiser to which the creative belongs. |
| `${ADV_FREQ}` | The total number of impressions seen by a user across all advertiser campaigns. |
| `${ADV_ID}` | The ID of the advertiser to which the creative belongs. |
| `${AGE}` | The age of the user if available. Supported values are an integer or 0. |
| `${APPNEXUS_AUCTION_ID}` | This macro is an alias for `${AUCTION_ID}`, and behaves in the same manner. |
| `${AUCTION_ID}` | The 64-bit character string representing the individual auction that led to the impression. |
| `${BID_PRICE}` | The first price bid for this impression, as opposed to the price paid after price reduction. |
| `${BIDPRICE}` | This macro is an alias for `${BID_PRICE}`, and behaves in the same manner. |
| `${CACHEBUSTER}` | A random number string used to limit caching of the URL.<br><br>**Note**: This macro ensures that a fresh call is made to the ad server every time the tag is called to accurately count all impressions. If you don't add this macro to the tag, you may see inaccurate impression totals. |
| `${CP_CODE}` | The campaign code of the served impression. |
| `${CP_ID}` | The campaign or split ID of the served impression. |
| `${CPG_CODE}` | The line item code of the served impression. |
| `${CPG_ID}` | The line item ID of the served impression. |
| `${CREATIVE_CODE}` | The code of the creative served if available. |
| `${CREATIVE_HEIGHT}` | The height of the creative served. |
| `${HEIGHT}` | This is an alias for `${CREATIVE_HEIGHT}`, and behaves in the same manner. |
| `${CREATIVE_ID}` | The creative ID that won the impression. |
| `${CREATIVE_SIZE}` | The width and height of the creative served. For example: 300x250. |
| `${CREATIVE_WIDTH}` | The width of the creative served. |
| `${WIDTH}` | This macro is an alias for `${CREATIVE_WIDTH}`, and behaves in the same manner. |
| `${CUSTOM_MODEL_ID}` | The `id` of the custom model used in the auction. When no custom model is used, this macro will return `0`.<br><br>**Note**: This custom macro will only work for APB Alpha Test clients. |
| `${CUSTOM_MODEL_LAST_MODIFIED}` | The date and time (in Unix Epoch time) since the custom model that was used in the auction was last modified. If no model was used, this macro will return `0`.<br><br>**Note**: This custom macro will only work for APB Alpha Test clients. |
| `${CUSTOM_MODEL_LEAF_NAME}` | The `leaf_name` specified in the leaf that determined the winning bid. If no name is specified or if a model was not used, this macro will return `---`. This aligns with the `leaf_name` field in the Standard Feed in Log Level Data. For more information, see [Standard Feed](../log-level-data/standard-feed.md).<br><br>**Note**: This custom macro will only work for APB Alpha Test clients. |
| `${DATACENTER}` | The data center ID (1 = NYM, 2 = LAX, 3 = AMS, 4 = FRA, 5 = SIN). |
| `${DEAL_ID}` | The Microsoft Advertising Deal ID associated with the winning bid if applicable. If there is no deal, this macro will return `0`. |
| `${ECP}` | The publisher-side estimated clear price (ECP) for the auction. |
| `${GENDER}` | The gender of the user if available. Possible values include:<br> - `f` (female)<br> - `m` (male)<br> - `u` (unknown) |
| `${INV_SOURCE_ID}` | **Deprecated** |
| `${IO_CODE}` | The insertion order code of the served impression. |
| `${IO_ID}` | The insertion order ID of the served impression. |
| `${OZONE_ID}` | **Deprecated** |
| `${PMT_RULE_ID}` | The ID of the payment rule used to price the impression. |
| `${POSTAL_CODE}` | The postal code of the user. |
| `${PRICE_PAID}` | The price paid for this impression after price reduction. This is the second price. |
| `${SECOND_PRICE}` | The price that represent the second highest bid in auction. |
| `${PT1}`, `${PT2}`, `${PT3}`, `${PT4}`, `${PT5}`, `${PT6}`, `${PT7}`, `${PT8}`, `${PT9}` | These macros can be populated with arbitrary custom data that you send when using the following placement tag query string parameters:<br> - `pt1`<br> - `pt2`<br> - `pt3`<br> - `pt4`<br> - `pt5`<br> - `pt6`<br> - `pt7`<br> - `pt8`<br> - `pt9`<br>For more information, see [Create a Placement Tag Macro](create-a-placement-tag-macro.md). |
| `${PUBLISHER_CODE}` | The code of the publisher selling the impression.<br><br>**Note**: This ID is available only if the publisher uses a code and has exposed it for reporting. |
| `${PUBLISHER_ID}` | The ID of the publisher selling the impression.<br>**Note**: This ID is available only if the publisher is exposed for reporting. |
| `${REFERER_URL}` | **Deprecated**<br><br>**Note**: Use `${REFERER_URL_ENC}` instead. |
| `${REFERER_URL_ENC}` | The encoded referring URL if available.<br>For mobile app impressions, this macro returns the app store URL if available. |
| `${REM_USER}` | A boolean value that indicates if the user is being remarketed. |
| `${RESERVE_PRICE}` | The reserve price set by the publisher. When there isn't a reserve price, this macro will return `0`. |
| `${SCHEME}` | Populates the appropriate application protocol (HTTP or HTTPS) depending on the inventory type. |
| `${SEG_CODES}` | The codes for the segments that the winning buyer owns or has access to within this user's cookie (in order of last seen time). If the user is in more than 15 of your accessible segments, this macro will only return the first 15 (ordered by most recently seen segment to oldest segment). |
| `${SEG_IDS}` | The IDs of the segments that the winning buyer owns or has access to within this user's cookie (in order of last seen time). If the user is in more than 15 of your accessible segments, this macro will only return the first 15 (ordered by most recently seen segment to oldest segment). |
| `${SELLER_MEMBER_ID}` | The member ID of the member that is selling the impression. |
| `${SITE_ID}` | The ID of the site that the impression is being served on. |
| `${SSP_DATA}` | Required for server-side conversion pixels. For more information, see [Server-Side Conversion Pixels](server-side-conversion-pixels.md). |
| `${TAG_CODE1}` | The integration code set on the placement. |
| `${TAG_CODE2}` | The additional integration code set on the placement. |
| `${TAG_ID}` | The Microsoft Advertising placement ID that initiated the bid request. |
| `${TIMESTAMP}` | The UNIX timestamp for the auction. |
| `${USE_COOKIES}` | This is used for third-party creatives to indicate whether cookies should be set for the user viewing the impression. Allowed values include:<br> - `0` for no<br> - `1` for yes<br>For more information about cookie-related settings, see [Cookie Privacy Settings](cookie-privacy-settings.md) and the [Publisher Service](../digital-platform-api/publisher-service.md). |
| `${USER_AGENT}` | The user agent string from the request's HTTP header. The user agent often identifies information such as the application, operating system, and software vendor acting on behalf of the user. For example: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4. |
| `${USER_AGENT_ENC}` | The encoded user agent string from the request's HTTP header. |
| `${USER_CITY} `| The character string of the user's city. |
| `${USER_COUNTRY}` | The character string of the user's country. |
| `${USER_ID}` | The Microsoft Advertising 64-bit character string representing the user for the impression. |
| `${USER_IP}` | The IP address of the user, which is truncated. |
| `${USER_LOCALE}` | The language and dialect (aa-DD) reported by the user's device. For example, en-ZA represents English (en) used in South Africa (ZA). |
| `${USER_STATE}` | The character string of the user's state or region.<br> - **In the USA**: 2 letter abbreviation<br> - **Outside of USA**: An encoded URL with the user's country followed by the user's region ID (FIPS 10-4 or Microsoft Advertising-generated).<br>For example, the region surrounding Riva, Latvia is LV%3A25 (encoding for LV:A25). |

## Creative macros for video impressions

The following macros can be used specifically for video impressions:

| Macro | Description |
|---|---|
| `${VIDEO_CONTEXT}` | The context of the video ad. Allowed values include:<br> - `0`: In-stream unknown<br> - `1`: In-stream pre-roll<br> - `2`: In-stream mid-roll<br> - `3`: In-stream post-roll<br> - `4`: Out-stream |
| `${VIDEO_PLAYBACK_METHOD}` | Specifies how the video was played. Allowed values include:<br> - `0`: Unknown<br> - `1`: Auto-play, sound-on<br> - `2`: Auto-play, sound-off<br> - `3`: Click-to-play<br> - `4`: Mouse-over<br> - `5`: Auto-play, sound unknown |
| `${VIDEO_PLAYER_HEIGHT}` | The height of the video player, expressed in pixels. |
| `${VIDEO_PLAYER_WIDTH}` | The width of the video player, expressed in pixels. |

## Creative macros for mobile impressions

The following macros can be used specifically for mobile impressions:

| Macro | Description |
|---|---|
| `${CARRIER_ID}` | The Microsoft Advertising integer representing the mobile carrier ID. For a complete list of carrier IDs, see the [Carrier Service](../digital-platform-api/carrier-service.md). |
| `${DEVICE_AAID}` | The Android advertising identifier when the impression is delivered from an Android device. |
| `${DEVICE_APPLE_IDA} `| The Apple advertising identifier when the impression is delivered from an Apple device. |
| `${DEVICE_IFA_TYPE}` | The type of identifier represented by the `${DEVICE_IFA}`. Possible values include:<br> - AAID (Android Advertising ID/Google)<br> - IDFA (Identifier for Advertising/Apple)<br> - AFAI (Amazon Fire ID)<br> - RIDA (Roku ID)<br> - OPENUDID<br> - TIFA (Tizen Identifier for Advertising (Samsung Ad ID))<br> - VIDA (Vizio Advertising ID)<br> - LGUDID (LG Unique Device ID)<br><br> `${DEVICE_IFA_TYPE}` should be used in conjunction with `${DEVICE_IFA}`, and this setup is recommended over individual device macros specific to each IFA type. These macros are applicable to both mobile and CTV device types. |
| `${DEVICE_IFA} `| The unique identifier representing the device. |
| `${DEVICE_MAKE_ID}` | The Microsoft Advertising integer representing the ID of the make of the mobile device such as `26`. For a complete list of mobile device make IDs, see the [Device Make Service](../digital-platform-api/device-make-service.md). |
| `${DEVICE_MD5}` | The MD5-encrypted unique identifier representing the mobile device. |
| `${DEVICE_MODEL_ID}` | The Microsoft Advertising integer representing the ID of the mobile device model such as `301`. For a complete list of mobile device model IDs, see the [Device Model Service](../digital-platform-api/device-model-service.md). |
| `${DEVICE_ODIN}` | The ODIN-encrypted unique identifier representing the mobile device. For more information, see [ODIN](https://code.google.com/p/odinmobile/). |
| `${DEVICE_OPENUDID}` | The OPENUDID-encrypted unique identifier representing the mobile device. |
| `${DEVICE_SHA1}` | The SHA1-encrypted unique identifier representing the mobile device. |
| `${DEVICE_WIN_ID}` | The Windows Ad ID for the device on which this impression occurred if applicable. |
| `${EXT_APP_ID}` | The external identifier for the application requesting the impression. This macro is only useful for mobile app impressions. |
| `${GEO_LAT}` | The latitude of the user's location when GPS data is available from a mobile device, expressed using the `snn.ddd,snn.ddd` format such as `+12.345` or `-45.123`. South is represented as a negative in this example. To comply with privacy standards, the maximum is five decimal places of precision. |
| `${GEO_LON}` | The longitude of the user's location when GPS data is available from a mobile device. expressed using the format `snn.ddd,snn.ddd`. For example: `+12.345` or `-45.123`. West is represented as a negative in this example. To comply with privacy standards, the maximum is five decimal places of precision. |
| `${IS_PREVIEW}` | A flag can be passed to the third-party server so that production impressions don't get counted in the total number of impressions when previewing creatives. Possible values include:<br> - `0` for no<br> - `1` for yes |
| `${SUPPLY_TYPE}` | This macro will be populated with a numeric value that denotes the supply type of the impression. Allowed values include:<br> - `0`: web<br> - `1`: mobile web<br> - `2`: mobile app<br> - `4`: toolbar |

## Privacy macros

In order for our clients to meet their transparency, notice, and choice/consent requirements under US state privacy law, the GDPR and the ePrivacy Directive, Microsoft Advertising supports the [Global Privacy Platform](https://iabtechlab.com/gpp) and the IAB Europe Transparency & Consent Framework (the "Framework"). For more information, see [the IAB Europe Transparency &amp; Consent Framework](https://iabeurope.eu/transparency-consent-framework/). Publishers should reference [Part of Privacy Regulations](../policies-regulations/index.yml) when using macros, such as the ones noted in the table below, to surface notice, transparency, and choice to end users located in the EEA, signal approved vendors, and pass consent to Microsoft Advertising and demand sources as well as their vendors through the Microsoft Advertising Platform. For more information, see [Part of Service Policies](../policies-regulations/index.yml).

| Macro | Description |
|---|---|
| `${GDPR_APPLIES}` | Designates whether GDPR regulations are applied. It specifically indicates whether the user is located in a GDPR impacted country, or if we have a GDPR-required signal passed with the request. Possible values include:<br> - `0` for no<br> - `1` for yes<br>**Note**: `0` may be received from an EEA country. It is the publisher's choice to signal in this manner. |
| `${GDPR}` | This is an alias for `${GDPR_APPLIES}`, and behaves in the same manner. |
| `${GDPR_CONSENT_STRING}` | This macro specifies the IAB GDPR consent string. If the GDPR applies, it will contain a list of user-approved vendors based on the IAB GDPR Transparency and Consent Framework. For more information, see [IAB GDPR Transparency and Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). |
| `${GDPR_CONSENT}` | This macro is an alias for `${GDPR_CONSENT_STRING}`, and behaves in the same manner. |
| `${XANDR_DOMAIN}` | Dynamically retrieves the appropriate Microsoft Advertising domain based on the cookie consent settings included in the TCF string. If the user has cookies enabled from their browser settings but has:<br> - not given consent for their cookies to be included in the TCF string, the `adnxs-simple.com` domain will be used to prevent the browser from attaching cookies to subsequent ad calls.<br> - given consent for their cookies to be included in the TCF string, the `adnxs.com` domain will be used to pass cookies in the header of each ad call.<br>**Note**: This macro should only be used if you plan on serving impressions in countries that require consent for cookies. |
| `${GPP_SID}` | Designates whether a section (i.e. regulatory framework) of the [Global Privacy Platform](https://iabtechlab.com/gpp) should be applied. Specifically, it indicates whether the user is located in a country affected by legislation covered by the GPP. |
| `${GPP_STRING_XXXXX*}` | This is the IAB [Global Privacy Platform](https://iabtechlab.com/gpp) (GPP) string. If a section of the GPP applies, then this will contain framework-dependent information reflecting the consent elections of the user.<br>**Note**: * `XXXXX` can represent any numerical ID. |

## Function macros

A function macro performs a function on another macro. Function macros can be used in combination with any other creative macro, including custom macros. If they are not recognized at render time, they will not be translated and the function will not be called.

Microsoft Advertising currently supports the `{$URL_ENC}` function macro, which can be used for a variety of purposes related to encoding. A key use case is when a URL needs to be passed from ad server to ad server using a creative macro. Due to the presence of unsupported characters in standard URL formatting, the `{$URL_ENC}` function macro must be encoded at various stages of the process.

This function macro takes the following form:

```
${URL_ENC(${MACRO_NAME},#)}
```

`${MACRO_NAME}` is the macro to be encoded and `#` is the integer representing the number of times to encode the contents. Possible values include:

- `1`
- `2`
- `3`

Each encoding corresponds to a step in the redirect chain, as well as how a given third-party click tracker works with the macro. Double encoding will usually be needed for final destination URLs when a second ad server is involved, and triple encoding for a third ad server.

To determine whether you will need to use single, double, or triple encoding, you should check with your third-party click tracker and then test your `URL_ENC` macro to ensure it works. If your macro is not working, one consequence of this may be link breakage, which will result in users not reaching the intended destination URL.

| Encoding Example | Format |
|---|---|
| Encoding click URLs once | Use the following format:<br>`${URL_ENC(${CLICK_URL},1)}`<br><br>**Note**: If [https://xandr.com](https://xandr.com) is passed as the click URL, using `${URL_ENC(${CLICK_URL},1)}` to single encode the URL would result in `https%3A%2F%2Fxandr.com` populating the creative. |
| Encoding media URL once | Use the following format:<br> `${URL_ENC(${MEDIA_URL},1)}` |
| Encoding media URL twice | Use the following format:<br> `${URL_ENC(${MEDIA_URL},2)}` |
| Encoding a custom macro called ADFORMAT once | Use the following format:<br>`${URL_ENC(#{ADFORMAT},1)}` |

## Digital Services Act (DSA) macros

According to Article 26 of the DSA, online platforms, including Microsoft Advertising's publisher clients must provide clear, concise, and unambiguous information about advertisements by February 17th, 2024. These requirements include:

1. Clearly identifying that the information is an advertisement.
1. Disclosing the identity of an individual or legal person on whose behalf the advertisement is presented.
1. Indicating the identity of an individual or legal person who made payment for the advertisement, if different from the advertiser.
1. Providing information about the primary parameters used to determine the ad recipient and, where applicable, instructions on how to modify those parameters.

| Macro | Description |
|:---|:---|
| `${DSA_REQUIRED}` | Indicates if DSA information should be made available.<br>Possible values include:<br> - `0`: Not required.<br> - `1`: Required. Bid responses with or without DSA object will be accepted.<br>- `2`: Required. Bid responses without DSA object will not be accepted.<br>- `3`: Required. Bid responses without DSA object will not be accepted. Here, the publisher is an Online Platform. |
| `${DSA_BEHALF}` | The free UNICODE text string with a name on whose behalf the ad is being displayed. This macro is populated from the DSA bid response.<br>For example, `Advertiser`. |
| `${DSA_PAID}` | The free UNICODE text string of who paid for the ad. This macro is populated from the DSA bid response.<br>For example, `Advertiser`. |
| `${DSA_PARAMS}` | The combination of integer values representing user parameters, separated by an underscore “_”.<br>For example, `1_2_3`.<br>Possible values include:<br>- `1`: Information on your online activity indicating your similarity to groups targeted by the advertiser. For example, age group, gender, education level, or interests.<br>- `2`: Information on the setting in which you view a specific advertisement. For example, website content, device type, IP address, location (country or city).<br>- `3`: Information on your precise geographic location, with an accuracy of approximately 500 meters. |

## Related topic

[Creative Macros](creative-macros.md)
