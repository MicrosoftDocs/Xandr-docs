---
title: Curator Feed
description: In this article, find information about the Curator feed and details about the columns associated with this data feed.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Curator feed

The Log-Level Curator Feed provides data on the transacted impressions of your curated deals. The feed contains one row per transacted impression. This data can then be used by curators to develop powerful offline attribution models, dashboards, and custom reporting as well as other solutions.

The Xandr internal name for this feed is `curator_feed`.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Recommended precisions / Lengths of data types

In the [Columns](#columns) table below, some values in the **Type** column contain a recommended precision or length in parentheses. For example, `string(100)` means "this string is probably (but not guaranteed to be) less than or equal to 100 characters in length".

For integers, the sizes are described in the [Integer Key](#integer-key) section.

For `numeric` (floating point) data types, we recommend being able to accept a precision of (18,6), meaning that we expect there to be a maximum total of 18 digits: 12 to the left of the decimal point, and 6 to the right.

For `string` data types, the recommended length of the field varies depending on the field. See the table below.

> [!WARNING]
> These are Recommendations, not Guarantees.
>
> The data *types* are meant to be accurate as documented. However, the recommended *precision* or *length* for a given data type should not be read as a guarantee. For example, a string or numeric column's value may exceed the suggested length or precision listed on this page.
>
> The recommendations are intended to help you build your system to ingest this data. You may need to do additional processing on the output of the Curator Feed to make it work with your particular integration.

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 01 | auction_id_64 | bigint | The Xandr unique auction identifier. |
| 02 | date_time | UNIX Epoch time | The time and date of the event (e.g., `1526057561` which would need to be translated to `Friday, May 11, 2018 4:52:41 PM (UTC)`). See `event_type` for a list of events. |
| 03 | user_tz_offset | tinyint | The time zone of user vs. UTC. Useful for daypart targeting. |
| 04 | media_type | tinyint | The general display style of the creative, classified by media subtype. To map media subtype IDs to their names and parent media types, use the [Media Subtype Service](../digital-platform-api/media-subtype-service.md). For the video media type, the value of the `creative_width` and `creative_height` columns will be `1`. |
| 05 | event_type | enum | Possible values: <br> - `imp` = impression <br> - `click` <br> - `served` = VAST Creative was served <br> - `started` = VAST Creative was started <br> - `skipped` = VAST Creative was skipped <br> - `error` = There was an error playing the VAST creative <br> - `25_pct` = The VAST creative played continuously for at least 25% of the total duration at normal speed <br> - `50_pct` = The VAST creative played continuously for at least 50% of the total duration at normal speed <br> - `75_pct` = The VAST creative played continuously for at least 75% of the duration at normal speed <br> - `100_pct` = The VAST creative was played to the end at normal speed so that 100% of the creative was played. |
| 06 | user_id_64 | bigint | The Xandr 64-bit User ID stored in the Xandr cookie store <br> This field is `0` when: <br> - Xandr does not have a match for this user; or <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies <br> It will be `-1` for opt-out/non-consented users. <br><br> **Note**: If you received the `hashed_user_id_64` version of this field, you will not receive the unhashed version. |
| 07 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. |
| 08 | ip_address | string | The IP address of user. This field has a maximum of 40 characters. |
| 09 | ip_address_trunc | string | The IP address of user with the last octet removed. This field has a maximum of 40 characters. |
| 10 | country | string | The geographic country of the impression. Derived from IP address of user or provided by the site associated with the impression. Uses [ISO 3166](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) country codes. |
| 11 | region | string | The geographic region of the impression. Derived from IP address of user or provided by the site associated with the impression. Uses ISO-3166-2 codes for US and Canadian regions, and FIPS codes for regions in all other countries. |
| 12 | dma | int | Specifies the ID of the designated market area for this impression. Use the [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md) to look up the area associated with the ID. |
| 13 | city | int | The ID of the city for this impression. Derived from IP address of user or provided by the site associated with the impression. Use the [City Service](../bidders/city-service.md) to look up the city associated with the ID. |
| 14 | postal_code | string | The postal code of the user's location. Derived from IP address of user or provided by the site associated with the impression. For postal codes, see [Postal Code Service](../bidders/postal-code-service.md). |
| 15 | latitude | string | The latitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd", for example `+12.345` or `-45.123`, where south is represented as negative. There can be a maximum of 5 decimal places of precision. |
| 16 | latitude_trunc | string | The truncated value (limited to 3 decimal places) of the latitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd". For example: <br> - `+12.345` or <br> - `-45.123` (where south is represented as negative). |
| 17 | longitude | string | The longitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd", for example `+12.345` or `-45.123`, where west is represented as negative. There can be a maximum of 5 decimal places of precision. |
| 18 | longitude_trunc | string | The truncated value (limited to 3 decimal places) of the longitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd". For example: <br> - `+12.345` or <br> - `-45.123` (where west is represented as negative). |
| 19 | device_unique_id | string | The unique identifier representing the mobile device. The numeric prefix indicates the type of unique device identifier: <br> - `0` = IDFA (Apple ID for Advertising) <br> - `1` = SHA1 <br> - `2` = MD5 <br> - `3` = ODIN <br> - `4` = OPENUDID <br> - `5` = AAID (Android Advertising ID) <br> - `6` = WINDOWSADID (Microsoft Advertising ID) <br> - `7` = RIDA (Roky id for Advertising) <br> - `8.9` = AFAI (Amazon Fire OS) <br> - `8.10` = TIFA (Tizen Identifier for Advertising (Samsung Ad ID)) <br> - `8.11` = VIDA (Vizio Advertising ID) <br> - `8.12` = LGUDID (LG Unique Device ID) |
| 20 | device_type | int | The type of device. Possible values are: <br> - `0` = Other Devices <br> - `1` = Desktops and Laptops <br> - `2` = Mobile Phones <br> - `3` = Tablets <br> - `4` = TV <br> - `5` = Game Console <br> - `6` = Media Players <br> - `7` = Set Top Box |
| 21 | tc_string | string | The Transparency and Consent String represents the [IAB Transparency and Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) string. The string is base-64 url-safe encoded and can be decoded using the IAB GDPR Transparency and Consent Framework technical specification. The string contains data rights, usage, and privacy information. |
| 22 | curated_deal_id | int | The ID of the curator's deal through which the impression transacted. |
| 23 | gross_revenue_dollars | numeric | The amount of spend the buyer sent to the curator for the impression (including buyer fees, if applicable). This is the same as Buyer's media cost (except media cost does not include buyer fees). <br> This is the same value as `curator_revenue` in the [Curator Analytics Report](../digital-platform-api/curator-analytics-report.md). |
| 24 | curator_margin | numeric | The profit the curator made on the transaction. |
| 25 | total_tech_fees_dollars | numeric | The fees Xandr charged to a curator on the impression. |
| 26 | total_cost_dollars | numeric | The amount the curator spent on exchange fees (to Xandr) and seller media for the impression. This does not include curator margin or curator fees. <br> This is the same value as `curator_total_cost` in the [Curator Analytics Report](../digital-platform-api/curator-analytics-report.md). |
| 27 | net_media_cost_dollars | numeric | The amount the curator spent on seller media for the impression. This does not include curator fees or curator margin (if applicable). <br> This is the same as gross seller revenue (which includes seller fees). |
| 28 | seller_member_id | int | The member ID of the seller. |
| 29 | publisher_id | int | The ID for the publisher of the placement. Curator member may map the Publisher ID to a name using the [Inventory Resold Service](../digital-platform-api/inventory-resold-service.md) if the seller has chosen to expose the publisher. Exposure to curator depends on the seller's visibility profile. |
| 30 | site_id | int | The ID for site associated with placement. Cannot be associated with a name, except by the seller member who owns the site. Exposure to curator depends on the seller's visibility profile. |
| 31 | site_domain | string | The most granular identifier of the site that we can offer (but not the full domain). This may be the domain of a supply partner (e.g., [doubleclick.com](https://marketingplatform.google.com/about/enterprise/)), the network who owns the resold inventory, or just "resold inventory". Exposure to curator depends on the seller's visibility profile settings. This field has a maximum of 100 characters. |
| 32 | tag_id | int | The ID of placement tag of the impression. Cannot be associated with a name, except by the seller member who owns the tag. Exposure to curator depends on the seller's visibility profile. |
| 33 | application_id | string | The ID of the mobile application (if applicable). |
| 34 | mobile_app_instance_id | int | Specifies the ID of the mobile app instance for this impression. Use the [Mobile App Instance Service](../digital-platform-api/mobile-app-instance-service.md) to look up the mobile app instance associated with the ID. |
| 35 | buyer_member_id | int | The member ID of the buyer. |
| 36 | creative_id | int | The ID of the creative served. |
| 37 | brand_id | int | The ID for brand of the creative. Curator member can map the `brand_id` to a name using the [Brand Service](../digital-platform-api/brand-service.md). |
| 38 | deal_id | int | The `seller_deal_id` associated with the impression, or `0` if the curator sourced the impression from the open exchange. |
| 39 | view_result | enum | The Xandr viewability measurement result of the impression. Possible values: <br> - `0` = VIEW_UNKNOWN <br> - `1` = VIEW_DETECTED <br> - `2` = VIEW_NOT_DETECTED <br> - `3` = VIEW_NOT_MEASURABLE <br> - `-1` = UNKNOWN <br><br> **Note**: For more details about viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md). |
| 40 | view_non_measurable_reason | int | The reason an impression could not be measured for viewability. Possible values: <br> - `0` = N/A. The impression was measured for viewability <br> - `1` = SCRIPT_NOT_SERVED. The viewability script was not served with the creative. For example, on mobile-app inventory. <br> - `2` = NO_SCRIPT_CALLBACK. The viewability script was served with the creative, but no callback/event was received. For example, the user left the page before the creative was served. <br> - `3` = TECHNICAL_LIMITATION. The viewability script was served and loaded, but was unable to measure for a technical reason. For example, a cross-domain iframe with Flash disabled. <br> - `-1` = UNKNOWN. The reason is unknown. <br><br> **Note**: For more information regarding viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md). |
| 41 | supply_type | enum | The type of supply. Possible values: <br> - `0` = WEB <br> - `1` = MOBILE_WEB <br> - `2` = MOBILE_APP <br> - `5` = TOOLBAR |
| 42 | creative_width | smallint | The width of the creative. |
| 43 | creative_height | smallint | The height of the creative. |
| 44 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
| 45 | operating_system | smallint | The operating system on which the impression occurred. Use the [Operating System Service](../digital-platform-api/operating-system-service.md) to look up the operating system associated with the ID. |
| 46 | browser | smallint | The browser in which the impression occurred. Use the [Browser Service](../digital-platform-api/browser-service.md) to look up the browser associated with the ID. |
| 47 | language | smallint | The language setting of the browser in which the impression occurred. Use the [Language Service](../digital-platform-api/language-service.md) to look up the language associated with the ID. |
| 48 | device_id | smallint | The model of the device on which the impression occurred. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to look up the device model associated with the ID. |
| 49 | extended_ids | array of messages | A list of Extended IDs available in the auction, regardless of whether they specifically influenced the transaction. Check the extended_ids table below for more details. |
| 50 | curated_deal_code | String | `curated_deal_code` allows you to conveniently receive the code you may have populated on your curated deal object. |
| 51 | split_id | int32 | The ID of the split which added the curated deal to the auction where the buyer purchased the impression. |
| 52 | external_campaign_id | string | An optional value DSPs can pass in the cid field on their bid response where they can indicate the line item ID in their system which submitted the bid. Since the cid field is optional, the external_campaign_id field will only have data when the external DSPs populate it on their bid response. See the [Open RTB specification](../bidders/incoming-bid-response-from-bidders.md) for more info on the cid field. |
| 53 | external_bidrequest_id | bigint | A unique identifier generated by Microsoft for the bid request. DSPs can use this identifier to associate their bid response with a bid request and potentially log the bid request identifier in their own log level data. |
| 54 | external_bidrequest_imp_id | bigint | A unique identifier for the impression within the bid request. A single bid request can have multiple impression opportunities which each have their own ID, allowing DSPs to associate their bid response with a bid request impression and potentially log the bid request impression identifier in their own log level data. |
| 55 | postal_code_ext_id | int32 | United States only. The 9 digital U.S. postal code of the user’s location, in the format 12345-1234. Derived from the IP address of the user or provided by the site associated with the impression. For postal codes, see Postal Code Service. |

### extended_ids

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 1 | id_type | unsigned 32 bit int | The source of the extended identifier: <br> - `10` = Trade Desk ID (Unified ID 1.0) <br> - `11` = Criteo ID <br> - `12` = NetID <br> - `13` = RampID <br> - `15` = UID 2.0 |
| 2 | id_value | string | Value of the extended identifier (for example `"ID0001"`). <br><br> **Note**: You will only see the value of this field if you have been permissioned. |
