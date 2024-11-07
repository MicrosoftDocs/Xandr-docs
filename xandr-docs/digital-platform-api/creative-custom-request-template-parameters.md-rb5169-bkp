---
title: Creative Custom Request Template Parameters
description: In this article, learn about the query string parameters and creative macros of the Creative Custom Request Template.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Creative Custom Request Template parameters

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

This document describes the query string parameters and creative macros Xandr supports for use by the [Creative Custom Request Template Service](creative-custom-request-template-service.md). For each ad server listed below, the supported parameters and macros are listed, along with examples of their use in building a request tailored to that ad server.

> [!TIP]
> For those parameters which are listed as "Not supported" below, you can use the `PT1` through `PT9` custom macros to pass the information you require in the request.

## Millennial

> [!NOTE]
> For more information, see the Millennial Media Ad Request Documentation.

## Required

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `apid` | Ad placement ID assigned by Millennial. | Use custom macro. | `apid=#{APID}` |
| `auid` | Unique ID. | `${DEVICE_OPENUDID}` |  |
| `ua` | User agent. | `${USER_AGENT_ENC}`; User agent is also automatically passed in the header. | `ua=${USER_AGENT_ENC}` |
| `uip` | User's IP address. | `${USER_IP}` | `uip=${USER_IP}`<br><br>**Note:** Xandr is COPPA compliant so the last octet will be truncated as appropriate. |

## Optional

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `age` | User's age. | `${AGE}` | `age=${AGE}` |
| `gender` | User's gender. | `${GENDER}` | `gender=${GENDER}` |
| `zip` | User's zip code. | `${POSTAL_CODE}` | `zip=${POSTAL_CODE}` |
| `marital` | User's marital status. | Not supported. | NOT SUPPORTED |
| `income` | User's househould income. | Not supported. | NOT SUPPORTED |
| `lat` | User's latitude. | `${GEO_LAT}` | `lat=${GEO_LAT}` |
| `long` | User's longitude.| `${GEO_LON}` | `long=${GEO_LON}` |

## Jumptap

### Jumptap: Required

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `gateway-ip` | User's IP address. | User's IP address is automatically passed in the header. | DO NOT INCLUDE.<br><br>**Note:** Xandr is COPPA compliant so the last octet will be truncated as appropriate. |
| `hid` | Device ID.| Not supported. | NOT SUPPORTED |
| `hid_sha1` | SHA1 hash of device ID. | `${DEVICE_SHA1}` | `hid_sha1=${DEVICE_SHA1}` |
| `idfa` | IDFA (for iOS devices only). | `${DEVICE_APPLE_IDA}` | `idfa=${DEVICE_APPLE_IDA}` |
| `idflag` | Limit ad tracking. | Automatically populated. | DO NOT INCLUDE |
| `l` | User's preferred language. | User's Accept-Language is automatically passed in the header. | NOT SUPPORTED |
| `pub` | Publisher alias assigned by Jumptap. | Use custom macro. | `pub=#{PUB}` |
| `site` | Site alias asigned by Jumptap. | Use custom macro. | `site=#{SITE}` |
| `spot` | Ad spot alias assigned by Jumptap. | Use custom macro. | `spot=#{SPOT}` |
| `url` | URL of the page requesting the ad. | `${REFERER_URL_ENC}` | `url=${REFERER_URL_ENC}` |
| `ua` | User agent. | `${USER_AGENT_ENC};`<br> User agent is also automatically passed in the header. | `ua=${USER_AGENT_ENC}` |
| `v` | Version of the Jumptap tapLink API. | Automatically populated. | DO NOT INCLUDE |

### Jumptap: Optional

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `mt-mraid` | MRAID version. | Not supported.| NOT SUPPORTED |
| `mt-jtlib` | Jumptap SDK version. | Not supported. | NOT SUPPORTED |
| `a` | Indicate whether adult ads are allowed. | Use custom macro. | `a=#{ADULT_ADS}` |
| `client-ip` | User's IP address. | User's IP address is automatically passed in the header. | DO NOT INCLUDE |
| `country` | User's country. | `${USER_COUNTRY}` | `country=${USER_COUNTRY}` |
| `ll` | User's lat/long. | `{{${JUMPTAP_LAT_LONG_ENC}` | `{{ll=${JUMPTAP_LAT_LONG_ENC}}}` |
| `email_sha1` | SHA1 hash of email address. | Not supported. | NOT SUPPORTED |
| `mt-age` | User's age. | `${AGE}` | `mt-age=${AGE}` |
| `mt-gender` | User's gender. | `${GENDER}` | `mt-gender=${GENDER}` |
| `mt-hhi` | User's household income. | Not supported. | NOT SUPPORTED |
| `mt-model` | Manufacturer's model name. | Not supported.| NOT SUPPORTED |
| `operator` | On-deck mobile operator. | Not supported. | NOT SUPPORTED |
| `pc` | User's zip code. | `${POSTAL_CODE}` | `pc=${POSTAL_CODE}` |
| `q` | Search terms. | Not supported. | NOT SUPPORTED |
| `u` | Publisher's unique ID of end-user. | Not supported. | NOT SUPPORTED |

## InMobi

### InMobi: Required

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `mk-siteid` | Site ID assigned by InMobi. | Use custom macro. | `mk-siteid=#{MK_SITEID}` |
| `mk-carrier` | User's IP address. | `${USER_IP}` | `mk-carrier=${USER_IP}`<br><br>**Note:** Xandr is COPPA compliant so the last octet will be truncated as appropriate. |
| `h-user-agent` | User agent. | `${USER_AGENT_ENC}` | `h-user-agent=${USER_AGENT_ENC}` |
| `mk-version` | Version of the InMobi API. | Automatically populated. | DO NOT INCLUDE |

### InMobi: Optional

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `mk-ad-slot` | Ad slot ID corresponding to tag size. | Automatically populated. | DO NOT INCLUDE |
| `h-referer` | Referer. | `${REFERER_URL_ENC}` | `h-referer=${REFERER_URL_ENC}` |
| `u-id-map` | Map of unique user IDs. | `${INMOBI_UID_MAP}` | `u-id-map=${INMOBI_UID_MAP}` |
| `u-id-adt` | Limit ad tracking. | Automatically populated. | DO NOT INCLUDE |
| `u-key-ver` | Must be set to 0. | Automatically populated when u-id-map is present. | DO NOT INCLUDE |
| `mk-ads` | Number of ads requested. | Automatically populated. | DO NOT INCLUDE |
| `ref-tag` | Reporting/performance grouping metrics. | Not supported. | NOT SUPPORTED |
| `adtype` | Ad format. | Not supported. | NOT SUPPORTED |
| `u-latlong-accu` | User's lat/long/accuracy. | `${INMOBI_LAT_LONG_ACCU}` | `u-latlong-accu=${INMOBI_LAT_LONG_ACCU}` |
| `u-age` | User's age. | `${AGE}` | `u-age=${AGE}` |
| `u-gender` | User's gender. | `${GENDER}` | `u-gender=${GENDER}` |
| `p-keywords` | Comma-separated list that describes page content. | Not supported. | NOT SUPPORTED |
| `tp` | Third-party integration type. | Automatically populated. | DO NOT INCLUDE |
| `d-localization` | User locale. | `${USER_LOCALE}` | `d-localization=${USER_LOCALE}` |
| `d-nettype` | Type of network. | `${INMOBI_NETTYPE}` | `d-nettype=${INMOBI_NETTYPE}` |
| `d-orientation` | Orientation of the screen. | `${INMOBI_ORIENTATION}` | `d-orientation=${INMOBI_ORIENTATION}` |
| `format` | Output format. | Automatically populated. | DO NOT INCLUDE |

## Mojiva

### Mojiva: Required

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `zone` | Zone of the publisher site assigned by Mojiva. | Use custom macro. | `zone=#{ZONE}` |
| `ip` | User's IP address. | `${USER_IP}` | `ip=${USER_IP}` |
| `ua` | User agent. | `${USER_AGENT_ENC}` | `ua=${USER_AGENT_ENC}` |

### Mojiva: Optional

| Parameter | Description | Macro | Example |
|:---|:---|:---|:---|
| `url` | URL of the page requesting the ad. | `${REFERER_URL_ENC}` | `url=${REFERER_URL_ENC}` |
| `key` | Output format. | Automatically populated. | DO NOT INCLUDE |
| `type` | Type of ad. | Not supported. | NOT SUPPORTED |
| `count` | Number of ads requested. | Automatically populated. | DO NOT INCLUDE |
| `udid` | MD5 hash of device ID. | `${DEVICE_MD5}` | `udid=${DEVICE_MD5}` |
| `test` | Retrieve test ads. | Use custom macro. | `test=#{TEST}` |
| `timeout` | Timeout of ad call. | Use custom macro. | `timeout=#{TIMEOUT}`<br><br>**Note:** The lower of the value set here and the value defined on the template or creative will be used as the timeout. |
| `creatives` | Returns the ad with the specified creative ID. | Use custom macro. | `creatives=#{CREATIVES}` |
| `excreatives` | Returns the ad excluding the specified creative IDs. | Use custom macro. | `excreatives=#{EXCREATIVES}` |
| `lineitems` | Returns the creative that belongs to the line item of the specific ID. | Use custom macro. | `lineitems=#{LINEITEMS}` |
| `exlineitems` | Returns the creative that does not belong to the line item of the specific ID. | Use custom macro. | `exlineitems=#{EXLINEITEMS}` |
| `order` | Sorted list of line item IDs desired to be shown first. | Use custom macro. | `order=#{ORDER}` |
| `image` | Used for getting the direct image. | Use custom macro. | `image=#{IMAGE}` |
| `over_18` | Filter ads by over 18 content. | Use custom macro. | `over_18=#{OVER_18}` |
| `keywords` | Filter ads by keywords. | Use custom macro. | `keywords=#{KEYWORDS}` |
| `border` | Show borders around banner ads.| Use custom macro. | `border=#{BORDER}` |
| `textborder` | Show borders around text ads. | Use custom macro. | `textborder=#{TEXTBORDER}` |
| `paramBG` | Background color in HEX. | Use custom macro. | `paramBG=#{PARAMBG}` |
| `paramBORDER` | Border color for text ads in HEX.| Use custom macro. | `paramBORDER=#{PARAMBORDER}` |
| `paramLINK` | Determine the color of links in HEX. | Use custom macro. | `paramLINK=#{PARAMLINK}` |
| `min_size_x` | Minimal width of ad. | Automatically populated. | DO NOT INCLUDE. |
| `min_size_y` | Minimal height of ad. | Automatically populated. | DO NOT INCLUDE. |
| `size_x` | Maximum width of ad. | Automatically populated. | DO NOT INCLUDE |
| `size_y` | Maximum height of ad. | Automatically populated. | DO NOT INCLUDE |
| `size_required` | Indicate whether image size info is returned. | Automatically populated. | DO NOT INCLUDE |
| `lat` | User's latitude. | `${GEO_LAT}` | `lat=${GEO_LAT}` |
| `long` | User's longitude. | `${GEO_LON}` | `long=${GEO_LON}` |
| `country` | User's country. | `${USER_COUNTRY}` | `country=${USER_COUNTRY}` |
| `mcc` | Mobile country code. | Not supported. | NOT SUPPORTED |
| `mnc` | Mobile network code. | Not supported. | NOT SUPPORTED |
| `region` | User's region. | `${USER_STATE}` | `region=${USER_STATE}` |
| `city` | User's city. | `${USER_CITY}`| `city=${USER_CITY}` |
| `area` | User's area code. | Not supported. | NOT SUPPORTED. |
| `dma` | User's DMA. | `${USER_DMA}` | `dma=${USER_DMA}` |
| `zip` | User's zip code. | `${POSTAL_CODE}` | `zip=${POSTAL_CODE}` |
| `jsvar` | Variable used to identify ad on page. | Not applicable. | NOT APPLICABLE |
| `callback` | JSONP callback function. | Not applicable. | NOT APPLICABLE |
| `carrier` | Mobile carrier name. | Not supported. | NOT SUPPORTED |
| `track` | Configure when impressions are counted by Mojiva. | Use custom macro. | `track=#{TRACK}` |
| `no_external` | Indicate whether external ads are allowed. | Use custom macro. | `no_external=#{NO_EXTERNAL}` |
| `imgstyle` | Add style attribute to `<img>` tag. | Use custom macro. | `imgstyle=#{IMGSTYLE}` |
| `encoding` | Ad encoding.| Not applicable. | NOT APPLICABLE |
| `target` | Change the `<a>` target for HTML responses. | Not applicable. | NOT APPLICABLE |

## Related topics

- [Creative Custom Request Template Service](creative-custom-request-template-service.md)
- [Creative Custom Request Template Type Service](creative-custom-request-template-type-service.md)
