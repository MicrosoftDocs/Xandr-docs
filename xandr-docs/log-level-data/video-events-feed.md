---
title: Video Events Feed
description: In this article, find information about the Video events feed and details about the columns associated with this data feed.
ms.custom: log-level-data
ms.date: 10/28/2023
---

# Video events feed

The Video Events Feed provides you with a listing of all video-specific events that occur on your video impressions. The feed contains one row per video event.

The Xandr internal name for this feed is `video_events_feed`.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description | Visibility |
|---|---|---|---|---|
| 01 | date_time | UNIX Epoch time | The time and date truncated to the hour that the record was processed by Xandr. For cross-hour events, for example, starting at 12:59 and finishing at 13:01, the hour recorded would be the last event's hour, which is 13 in this example. | Both |
| 02 | auction_id_64 | bigint | The Xandr unique auction identifier. | Both |
| 03 | buyer_member_id | int | The member ID of the buyer. <br> - For `imp_type` = 1 (Blank), the `buyer_member_id` and `creative_id` is `0`. <br> - For `imp_type` = 2 (PSA), the Xandr PSA `member_id` displays. <br> - For `imp_type` = 3 or 4 (Default Error or Default), the `seller_member_id` displays. | Both |
| 04 | seller_member_id | int | The member ID of the seller. | Both |
| 05 | advertiser_id | int | The ID of the advertiser. | Buyer |
| 06 | publisher_id | int | The ID for the publisher of the placement. Buyer member may map the Publisher ID to a name using the [Inventory Resold Service](../digital-platform-api/inventory-resold-service.md) if the seller has chosen to expose the publisher. Exposure to buyer depends on the seller's visibility profile. | Both |
| 07 | site_id | int | The ID for site associated with placement. Cannot be associated with a name, except by the seller member who owns the site. Exposure to buyer depends on the seller's visibility profile. | Seller |
| 08 | tag_id | int | The ID of placement tag of the impression. Cannot be associated with a name, except by the seller member who owns the tag. Exposure to buyer depends on the seller's visibility profile. | Both |
| 09 | insertion_order_id | int | The ID for insertion order if used. | Buyer |
| 10 | line_item_id | int | The identifier of line item. | Buyer |
| 11 | campaign_id | int | The ID of the campaign. | Buyer |
| 12 | creative_id | int | The ID of the creative served. | Both |
| 13 | creative_freq | int | The creative-level frequency (times the user has seen this creative by this advertiser). | Buyer |
| 14 | creative_rec | int | The creative-level recency in minutes (how long it has been since the user has seen this creative ad). | Buyer |
| 15 | brand_id | int | The ID for brand of the creative. | Both |
| 16 | country | string(2) | The geographic country of the impression passed in on the ad call. Uses [ISO 3166](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) country codes. | Both |
| 17 | creative_width | smallint | The width of the creative. | Both |
| 18 | creative_height | smallint | The height of the creative. | Both |
| 19 | deal_id | int | The Deal ID associated with this impression. | Both |
| 20 | video_was_served | boolean | Whether or not the video was served this hour | Both |
| 21 | video_started | boolean | Whether or not the video was started this hour | Both |
| 22 | video_was_skipped | boolean | Whether or not the video was skipped this hour | Both |
| 23 | video_had_error | boolean | Whether or not the video had an error this hour | Both |
| 24 | video_hit_25_pct | boolean | Whether or not the video hit 25 pct this hour | Both |
| 25 | video_hit_50_pct | boolean | Whether or not the video hit 50 pct this hour | Both |
| 26 | video_hit_75_pct | boolean | Whether or not the video hit 75 pct this hour | Both |
| 27 | video_completed | boolean | Whether or not the video completed this hour | Both |
| 28 | imp_type | tinyint | The type of impression. Possible values: <br> - `0` = Video event error <br> - `1` = Blank: "200 OK" response (blank) served. <br> - `2` = PSA: A public service announcement served because no other creative was eligible. <br> - `3` = Default Error: A default creative served due to timeout issue. <br> - `4` = Default: A default creative served because no campaigns bid or no other creative was eligible. <br> - `5` = Kept: One of your managed advertisers served a creative. <br> - `6` = Resold: The impression was sold to a third-party buyer. <br> - `7` = RTB: Your creative served on third-party inventory. <br> - `8` = PSA Error: A public service announcement served due to timeout issue. <br> - `9` = External Impression: An impression from an impression tracker. <br> - `10` = External Click: A click from a click tracker. | Both |
| 29 | advertiser_currency | string(3) | The currency used by advertiser. | Buyer |
| 30 | publisher_currency | string(3) | The currency in which publisher is paid. | Seller |
| 31 | site_domain | string(100) | The most granular identifier of the site that we can offer (but not the full domain). This may be the domain of a supply partner (e.g., [doubleclick.com](https://marketingplatform.google.com/about/enterprise/)), the network who owns the resold inventory, or just "resold inventory". Exposure to buyer depends on the seller's visibility profile settings. | Both |
| 32 | application_id | string | The ID of the mobile application (if applicable). Exposure to buyer depends on the seller's visibility profile. | Both |
| 33 | media_cost_cpm | numeric | For buyers, the dollar amount * 1000 that a network is paying for the video impression associated to this video event. For sellers, the dollar amount * 1000 paid to publisher for the impression associated to this video event. | Both |
| 34 | booked_revenue | numeric | The dollar amount earned by network on the impression associated with this video event | Buyer |
| 35 | seller_revenue_cpm | numeric | The amount the seller is paid for the impression associated with this video event. <br><br> **Note**: The `impression_seller_revenue_cpm` is also calculated for `imp_type = 5` (managed impressions). If you wish to calculate total revenue from resold impressions, sum `seller_revenue_cpm` only for `imp_type = 6`. | Seller |
| 36 | playback_method | enum | The type of initiation method. Possible values: <br> - `0` = Unknown <br> - `1` = Auto-play, sound on <br> - `2` = Auto-play, sound off <br> - `3` = Click-to-play <br> - `4` = Mouse-over <br> - `5` = Auto-play, sound unknown |  |
| 37 | video_context | enum | The type of context. Possible values: <br> - `0` = Unknown <br> - `1` = Pre-Roll <br> - `2` = Mid-Roll <br> - `3` = Post-Roll <br> - `4` = Outstream <br> - `5` = Bannerstream |  |
| 38 | player_size_id | tinyint | The size of the video player. Possible values: <br> - `0` = Unknown <br> - `1` = Small <br> - `2` = Medium <br> - `3` = Large |  |
| 39 | supply_type | enum | The type of supply. Possible values: <br> - `0` = Web <br> - `1` = Mobile_Web <br> - `2` = Mobile_App |  |
| 40 | view_result | enum | The Xandr viewability measurement result of the impression. Possible values: <br> - `0` = VIEW_UNKNOWN <br> - `1` = VIEW_DETECTED <br> - `2` = VIEW_NOT_DETECTED <br> - `3` = VIEW_NON_MEASURABLE <br> - `-1` = UNKNOWN <br> For non-impression events, this will be `NULL`. <br><br> **Note**: For more details about viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md). | Both |
| 41 | view_non_measurable_reason | enum | The reason an impression could not be measured for viewability. Possible values: <br> - `0` = N/A. The impression was measured for viewability <br> - `1` = SCRIPT_NOT_SERVED. The viewability script was not served with the creative. For example, on mobile-app inventory. <br> - `2` = NO_SCRIPT_CALLBACK. The viewability script was served with the creative, but no callback/event was received. For example, the user left the page before the creative was served. <br> - `3` = TECHNICAL_LIMITATION. The viewability script was served and loaded, but was unable to measure for a technical reason. For example, a cross-domain iFrame with Flash disabled. <br> - `-1` = UNKNOWN <br><br> **Note**: For more information regarding viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md). | Both |
| 42 | error_code | int | For a detailed description of error codes and their meanings, see the [IAB's VAST 3.0 documentation](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf) or view the list of Error Codes below. |  |
| 43 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |  |
| 44 | split_id | int32 | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. | Buyer |
| 45 | video_served_timestamp | UNIX Epoch time | The time and date when the video ad response was recorded. | Both |
| 46 | video_started_timestamp | UNIX Epoch time | The time and date when the video started event was received by Xandr. | Both |
| 47 | video_skipped_timestamp | UNIX Epoch time | The time and date when the video skipped event was received by Xandr. | Both |
| 48 | video_errored_timestamp | UNIX Epoch time | The time and date when the video error event was received by Xandr. | Both |
| 49 | video_hit_25_pct_timestamp | UNIX Epoch time | The time and date when the video first quartile event was received by Xandr. | Both |
| 50 | video_hit_50_pct_timestamp | UNIX Epoch time | The time and date when the video second quartile event was received by Xandr. | Both |
| 51 | video_hit_75_pct_timestamp | UNIX Epoch time | The time and date when the video third quartile event was received by Xandr. | Both |
| 52 | video_completed_timestamp | UNIX Epoch time | The time and date when the video completed event was received by Xandr. | Both |
| 53 | vg_id | Int | Field is part of an ongoing alpha release. | Buyer |

## Error codes

The table below shows a complete listing of error codes and their meanings.

> [!NOTE]
> You may receive error codes in the feed that are not present in the list below. If you do, those error codes are generally non-VAST-compliant custom codes sent from the video player.

| Error Codes | Definition |
|---|---|
| `100` | XML parsing error. |
| `101` | VAST schema validation error. |
| `102` | VAST version of response not supported. |
| `200` | Trafficking error. Video player received an ad type that it was not expecting and/or cannot display. |
| `201` | Video player expecting different linearity. |
| `202` | Video player expecting different duration. |
| `203` | Video player expecting different size. |
| `300` | General Wrapper error. |
| `301` | Timeout of VAST URI provided in Wrapper element, or of VAST URI provided in a subsequent Wrapper element. Includes request errors such as invalid URI, unreachable or request timeout for URI, and security or other exceptions related to requesting a VAST URI. |
| `302` | Wrapper limit reached, as defined by the video player. Too many Wrapper responses have been received with no InLine response. |
| `303` | No ads VAST response after one or more Wrappers. Also includes number of empty VAST responses from fallback. |
| `400` | General linear error. Video player is unable to display the linear ad. |
| `401` | File not found. Unable to find Linear/MediaFile from URI. |
| `402` | Timeout of MediaFile URI. |
| `403` | Could not find MediaFile that is supported by this video player, based on the attributes of the MediaFile element. |
| `405` | Problem displaying MediaFile. |
| `500` | General NonLinearAds error. |
| `501` | Unable to display NonLinear Ad because creative dimensions do not align with creative display area (i.e., creative dimension too large). |
| `502` | Unable to fetch NonLinearAds/NonLinear resource. |
| `503` | Could not find NonLinearresource with supported type. |
| `600` | General CompanionAds error. |
| `601` | Unable to display companion because creative dimensions do not fit within Companion display area (i.e., no available space). |
| `602` | Unable to display Required Companion. |
| `603` | Unable to fetch CompanionAds/Companion resource. |
| `604` | Could not find Companion resource with supported type. |
| `900` | Undefined error. |
| `901` | General VPAID error. |
