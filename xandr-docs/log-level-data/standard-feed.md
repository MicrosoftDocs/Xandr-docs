---
title: Standard Feed
description: In this article, find information about the Standard feed and details about the columns associated with this data feed.
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Standard feed

The Log-Level Standard Feed provides data on your managed publishers' and/or your managed advertisers' transacted impressions and the resulting clicks and conversions. The feed contains one row per transacted impression, click, or conversion. If you use impression and click trackers, the feed will also contain one row per impression tracker or click tracker event. For video and audio media types, the feed will also contain one row per video/audio VAST event (see `event_type` in the [Columns](#columns) section below for more information).

The Xandr internal name for this feed is `standard_feed`.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Data visibility and "NULL" values

All columns are always included, but you can only see data about your own transacted impressions. The "Visibility" column tells you who sees a particular column in any given transaction (e.g., both buyers and sellers, just buyers, or just sellers). Columns that are not visible will be shown as "NULL."

"NULL" may be returned in cases when:

- You are a buyer in the transaction but the field is a seller-related field (or vice versa).
- The seller on the impression has visibility settings that hide the value of that field from buyers (assuming you are a buyer in this transaction).
- The data is not available.

## Recommended precisions / Lengths of data types

In the [Columns](#columns) table below, some values in the **Type** column contain a recommended precision or length in parentheses. For example, `string(100)` means "this string is probably (but not guaranteed to be) less than or equal to 100 characters in length".

For integers, the sizes are described in the [Integer Key](#integer-key) section.

For `numeric` (floating point) data types, we recommend being able to accept a precision of (18,6), meaning that we expect there to be a maximum total of 18 digits: 12 to the left of the decimal point, and 6 to the right.

For `string` data types, the recommended length of the field varies depending on the field. See the [Columns](#columns) table below.

> [!WARNING]
> These are Recommendations, not Guarantees:
>
> The data *types* are meant to be accurate as documented. However, the recommended *precision* or *length* for a given data type should not be read as a guarantee. For example, a string or numeric column's value may exceed the suggested length or precision listed on this page.
>
> The recommendations are intended to help you build your system to ingest this data. You may need to do additional processing on the output of the Standard Feed to make it work with your particular integration.

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
| 01 | auction_id_64 | bigint | The Xandr unique auction identifier. | Both |
| 02 | date_time | UNIX Epoch time | The time and date of the event (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). See `event_type` for a list of events. | Both |
| 03 | user_tz_offset | tinyint | The time zone of user vs. UTC. Useful for daypart targeting. | Both |
| 04 | creative_width | smallint | The width of the creative. | Both |
| 05 | creative_height | smallint | The height of the creative. | Both |
| 06 | media_type | tinyint | The general display style of the creative, classified by media subtype. To map media subtype IDs to their names and parent media types, use the [Media Subtype Service](../digital-platform-api/media-subtype-service.md). For the video media type, the value of the `creative_width` and `creative_height` columns will be `1`. | Both |
| 07 | fold_position | tinyint | The placement position relative to fold. Possible values: <br> - `0` = Unknown (Default) <br> - `1` = Above the fold <br> - `2` = Locked (Fixed position) | Both |
| 08 | event_type | enum | Possible values: <br> - `imp` = impression <br> - `click` <br> - `pc_conv` = Post-click conversion associated with Xandr's cookie ID. <br> - `pv_conv` = Post-view conversion associated with Xandr's cookie ID. <br> - `pc_ip_conv` = Post-click conversion associated with IP address. <br> - `pv_ip_conv` = Post-view conversion associated with IP address. <br> - `pc_crossdevice_conv` = Post-click conversion associated with Xandr's cross-device graph. <br> - `pv_crossdevice_conv` = Post-view conversion associated with Xandr's cross-device graph. <br> In addition, for VAST creatives, there are these VAST-specific possible event types: <br> - `served` = VAST Creative was served. <br> - `started` = VAST Creative was started. <br> - `skipped` = VAST Creative was skipped. <br> - `error` = There was an error playing the VAST creative. <br> - `25_pct` = The VAST creative played continuously for at least 25% of the total duration at normal speed. <br> - `50_pct` = The VAST creative played continuously for at least 50% of the total duration at normal speed. <br> - `75_pct` = The VAST creative played continuously for at least 75% of the duration at normal speed. <br> - `100_pct` = The VAST creative was played to the end at normal speed so that 100% of the creative was played. | Both |
| 09 | imp_type | tinyint | The type of impression. Possible values: <br> - `1` = Blank: "200 OK" response (blank) served. <br> - `2` = PSA: A public service announcement served because no other creative was eligible. <br> - `3` = Default Error: A default creative served due to timeout issue. <br> - `4` = Default: A default creative is served because no campaign bid or no other creative was eligible. <br> - `5` = Kept: Serve the creative to one of your managed advertisers. <br> - `6` = Resold: The impression was sold to a third-party buyer. <br> - `7` = RTB: Serve your creative on third-party inventory. <br> - `8` = PSA Error: A public service announcement is served due to timeout issue. <br> - `9` = External Impression: An impression from an impression tracker. <br> - `10` = External Click: A click from a click tracker. <br> - `11` = Insertion: Serve your creative on third-party inventory where it persists across page-loads and sessions. | Both |
| 10 | payment_type | tinyint | The method by which the buyer is paying for the impression. Possible values: <br> - `-1` = No payment <br> - `0` = CPM <br> - `1` = CPC <br> - `2` = CPA <br> - `3` = Owner CPM <br> - `4` = Owner revshare <br> - `5` = CPVM <br> - `6` = CPCV <br> - `999` = Unknown | Both |
| 11 | media_cost_cpm | numeric | For buyers, the amount (in USD) * 1000 that a network is paying for an impression . For sellers, the amount (in USD) * 1000 paid to publisher. | Both |
| 12 | revenue_type | tinyint | The method by which the buyer network gets paid by the advertiser, or how the method by which the seller network was paid by the buyer network. Possible values: <br> - `-1` = No payment <br> - `0` = Flat CPM <br> - `1` = Cost Plus CPM <br> - `2` = Cost Plus Margin <br> - `3` = CPC <br> - `4` = CPA <br> - `5` = Revshare <br> - `6` = Flat Fee <br> - `7` = Variable CPM (vcpm) <br> - `8` = Estimated CPM (est_cpm) <br> - `9` = Viewable CPM <br> - `10` = Cost Per Completed Video | Both |
| 13 | media_cost | numeric | The gross CPM amount (in USD) paid by the buyer (includes all deductions and price reductions). | Buyer |
| 14 | buyer_bid | numeric | This column returns different values for buyers and for sellers measured in CPM (in USD). <br> - For buyers, this is the raw value submitted to the auction prior to subtraction of fees, commissions, etc. It will be greater than or equal to the total amount paid by the buyer (`buyer_spend`). <br> - For sellers, this value is the bid that was evaluated during the auction, after subtraction of fees, commissions, etc. <br> - For managed transactions (`imp_type = 5`), `buyer_bid` will equal `buyer_spend` because bid and price reductions are not applied. <br><br> **Note**: The value of this column reflects any bid reductions made for Bid Price Pacing (BPP) but does not include reductions made for Bid Price Optimization (BPO). | Both |
| 15 | ecp | numeric | The estimated clear price for placement tag, in dollars unless another advertiser currency is specified. | Both |
| 16 | eap | numeric | The estimated average price for placement tag, in dollars unless another advertiser currency is specified. | Both |
| 17 | is_imp | int | Possible values: <br> - `0` = False <br> - `1` = True | Both |
| 18 | is_learn | tinyint | Possible values: <br> - `0` = Base Bid <br> - `1` = Learn <br> - `2` = Optimized | Both |
| 19 | predict_type_rev | tinyint | The optimization phase of the bid. Possible values: <br> - `-2` = No predict phase <br> - `-1` = Base predict phase <br> - `0` = Learn give up <br> - `1` = Learn <br> - `2` = Throttled <br> - `3` = Optimized <br> - `4` = Biased <br> - `5` = Optimized 1 <br> - `8` = Optimized give up <br> - `9` = Base bid below give up | Both |
| 20 | user_id_64 | bigint | The Xandr 64-bit User ID stored in the Xandr cookie store. <br> This field is `0` when: <br> - Xandr does not have a match for this user; or <br> - the user's browser doesn't accept cookies; or <br> - you do not have a legal basis to access and process personal data for an impression where GDPR applies. <br> It will be `-1` for opt-out/non-consented users. <br><br> **Note**: If you received the `hashed_user_id_64` version of this field, you will not receive the unhashed version. | Both |
| 21 | ip_address | string(40) | The IP address of user. | Both |
| 22 | ip_address_trunc | string(40) | The IP address of user with the last octet removed. | Both |
| 23 | country | string(2) | The geographic country of the impression. Derived from IP address of user or provided by the site associated with the impression. Uses [ISO 3166](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) country codes. | Both |
| 24 | region | string(2) | The geographic region of the impression. Derived from IP address of user or provided by the site associated with the impression. Uses ISO-3166-2 codes for US and Canadian regions, and FIPS codes for regions in all other countries. | Both |
| 25 | operating_system | tinyint | The ID of operating system version. To map operating system version IDs to names, use the [Operating System Extended Service](../digital-platform-api/operating-system-extended-service.md). | Both |
| 26 | browser | tinyint | The ID of the browser. To map browser IDs to names, use the [Browser Service](../digital-platform-api/browser-service.md). | Both |
| 27 | language | tinyint | The ID of the language. To map language IDs to names, use the [Language Service](../digital-platform-api/language-service.md). | Both |
| 28 | venue_id | int | The venue is a combination of domain, site, tag, and user country which Xandr's optimization system uses to determine bid valuations. | Both |
| 29 | seller_member_id | int | The member ID of the seller. | Both |
| 30 | publisher_id | int | The ID for the publisher of the placement. Buyer member may map the Publisher ID to a name using the [Inventory Resold Service](../digital-platform-api/inventory-resold-service.md) if the seller has chosen to expose the publisher. Exposure to buyer depends on the seller's visibility profile. | Both |
| 31 | site_id | int | The ID for site associated with placement. Cannot be associated with a name, except by the seller member who owns the site. Exposure to buyer depends on the seller's visibility profile. | Seller |
| 32 | site_domain | string(100) | The most granular identifier of the site that we can offer (but not the full domain). This may be the domain of a supply partner (e.g., [doubleclick.com](https://marketingplatform.google.com/about/enterprise/)), the network who owns the resold inventory, or just "resold inventory". Exposure to buyer depends on the seller's visibility profile settings. | Both |
| 33 | tag_id | int | The ID of placement tag of the impression. Cannot be associated with a name, except by the seller member who owns the tag. Exposure to buyer depends on the seller's visibility profile. | Both |
| 34 | external_inv_id | int | The ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). | Seller |
| 35 | reserve_price | numeric | The reserve price for the placement (in USD), if any. | Seller |
| 36 | seller_revenue_cpm | numeric | The amount (in USD) the seller is paid for the impression. When `revenue_type` is `3` (CPC) or `4` (CPA), revenue will appear in this field on the corresponding click or conversion row (as determined by `event_type`). The revenue value will still be in CPM, so to calculate the revenue for the specific click/conversion event, divide by 1000. <br><br> **Note**: <br> - This field is also calculated for `imp_type = 5` (managed impressions). If you wish to calculate total revenue from resold impressions, sum `seller_revenue_cpm` only for `imp_type = 6`. <br> - For fixed fee line items, revenue would not be reflected accurately in this field. Fixed fee line items allocate revenue on a one time or daily basis and therefore, revenue is not logged at an auction level. | Seller |
| 37 | media_buy_rev_share_pct | numeric | The publisher revenue share or the percent of booked revenue the seller shares with its publisher. This is a fraction between 0 and 1. If you multiply by 100 you get the percentage value. | Seller |
| 38 | pub_rule_id | int | The ID for the publisher rule, which is set up in and defines how the publisher is paid. | Seller |
| 39 | seller_currency | string(3) | The currency used by the seller. | Seller |
| 40 | publisher_currency | string(3) | The currency in which publisher is paid. | Seller |
| 41 | publisher_exchange_rate | numeric | The exchange rate (publisher currency: USD) on the day of the transaction. | Seller |
| 42 | serving_fees_cpm | numeric | The serving fees in addition to media costs to when serving an ad (in USD). For more details, see [Partner Fee Service](../digital-platform-api/partner-fee-service.md). | Buyer |
| 43 | serving_fees_revshare | numeric | The revenue share in addition to media costs when serving an ad (in USD). For more details, see [Partner Fee Service](../digital-platform-api/partner-fee-service.md). | Buyer |
| 44 | buyer_member_id | int | The value of this field depends on the value of the `imp_type` field. Possible values of the `imp_type` field and the affect on the value of the `buyer_member_id` field are listed below: <br> - if the `imp_type` field is `1` (Blank), then the `buyer_member_id` and `creative_id` is `0`. <br> - if the `imp_type` field is `2` (PSA), then the `buyer_member_id` field is set to the Xandr PSA `member_id`. <br> - if the `imp_type` field is `3` (Default Error) or `4` (Default), then the `buyer_member_id` field is set to the value of the `seller_member_id`. <br> - if the `imp_type` field is `5`, `6`, or `7`, then the `buyer_member_id` field is set to the ID of the member who bought the impression. | Both |
| 45 | advertiser_id | int | The ID of the advertiser. | Buyer |
| 46 | brand_id | int | The ID for brand of the creative. | Both |
| 47 | advertiser_frequency | int | The advertiser-level frequency (times they have seen an ad by this advertiser). The value of the advertiser frequency is the lifetime imps for the user. | Buyer |
| 48 | advertiser_recency | int | The advertiser-level recency in minutes (how long it has been since the user saw an ad from this advertiser?). | Buyer |
| 49 | insertion_order_id | int | The ID for insertion order if used. | Buyer |
| 50 | line_item_id | int | The identifier of line item. | Buyer |
| 51 | campaign_id | int | The ID of the campaign. | Buyer |
| 52 | creative_id | int | The ID of the creative served. | Both |
| 53 | creative_freq | int | The creative-level frequency (times the user has seen this creative by this advertiser). | Buyer |
| 54 | creative_rec | int | The creative-level recency in minutes (how long it has been since the user has seen this creative ad?). | Buyer |
| 55 | cadence_modifier | numeric | The cadence modifier for the impression, which is the number by which the bid was multiplied. | Buyer |
| 56 | can_convert | tinyint | If impression has conversion pixels associated or not. | Buyer |
| 57 | user_group_id | int | Used if advertiser separates users into groups for purposes of A/B testing. | Buyer |
| 58 | is_control | tinyint | Whether the creative served is a control creative. <br> - `0` = test impression <br> - `1` = control impression <br> - `2` = no cookie user. (Xandr does not include no cookie users to avoid skewing the size of test and control groups). | Buyer |
| 59 | control_pct | numeric | The percentage of events (specified by `event_type`) that are control. This is set by the network. | Buyer |
| 60 | control_creative_id | int | The ID of the control creative, if a control creative is served. | Buyer |
| 61 | is_click | int | Indicates if the creative was clicked. Possible values: <br> - `0` = False <br> - `1` = True <br> - `NULL` = No information available | Buyer |
| 62 | pixel_id | int | The ID of conversion pixel. | Buyer |
| 63 | is_remarketing | tinyint | Used to indicate that a new segment pixel is remarketing or not. | Buyer |
| 64 | post_click_conv | int | Used to identify a row that is a post click conversion. This has a maximum value of `1`. | Buyer |
| 65 | post_view_conv | int | Used to identify a row that is a post view conversion. This has a maximum value of `1`. | Buyer |
| 66 | post_click_revenue | numeric | The advertiser post click revenue (in USD). | Buyer |
| 67 | post_view_revenue | numeric | The advertiser post view revenue (in USD). | Buyer |
| 68 | order_id | string(36) | An optional value passed in by buyer on conversion pixel using the `order_id` parameter. | Buyer |
| 69 | external_data | string(30) | An optional extra data passed in by buyer on conversion pixel using the `other` parameter. | Buyer |
| 70 | pricing_type | string(3) | The line item pricing type, or how the buyer network gets paid by the advertiser. Possible values: <br> - cpm <br> - plc (cost plus CPM) <br> - plm (cost plus margin) | Buyer |
| 71 | booked_revenue | numeric | The amount (in USD) earned by network on impression. | Buyer |
| 72 | booked_revenue_adv_curr | numeric | The same amount as booked revenue dollars, but displayed in that advertiser currency. For example, if your advertiser pays in Euros you can see this here. Use the `advertiser_currency` field to look up the advertiser's currency. | Buyer |
| 73 | commission_cpm | numeric | Commission (in USD) if used in or API. For more details, see [Partner Fee Service](../digital-platform-api/partner-fee-service.md). | Buyer |
| 74 | commission_revshare | numeric | Commission (in USD) if used in or API. For more details, see [Partner Fee Service](../digital-platform-api/partner-fee-service.md). | Buyer |
| 75 | auction_service_deduction | numeric | The amount (in USD) deducted from the bid to pay for auction hosting. | Buyer |
| 76 | auction_service_fees | numeric | The amount (in USD) charged for purchasing inventory from a publisher that Xandr does not have a revshare agreement with. | Buyer |
| 77 | creative_overage_fees | numeric | The amount (in USD) charged if the creative served is over our size (bandwith) limit, dollar amount. | Buyer |
| 78 | clear_fees | numeric | The amount (in USD) charged for facilitating the auction for the buyer. | Buyer |
| 79 | buyer_currency | string(3) | The currency used by the buyer. | Buyer |
| 80 | advertiser_currency | string | The currency used by the advertiser. | Buyer |
| 81 | advertiser_exchange_rate | numeric | The exchange rate on day of event. Rate is updated daily at 4 PM GMT. For any currency fields provided in the advertiser currency (i.e., fields with an "`adv_curr`" suffix), use this rate to convert the value into USD. | Buyer |
| 82 | latitude | string | The latitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd", for example `+12.345` or `-45.123`, where south is represented as negative. There can be a maximum of 5 decimal places of precision. | Both |
| 83 | longitude | string | The longitude of the user's location, when GPS data is available from a mobile device. Expressed in the format "snn.ddd,snn.ddd", for example `+12.345` or `-45.123`, where west is represented as negative. There can be a maximum of 5 decimal places of precision. | Both |
| 84 | device_unique_id | string | The unique identifier representing the mobile device. The numeric prefix indicates the type of unique device identifier: <br> - `0` = IDFA (Apple ID for Advertising) <br> - `1` = SHA1 <br> - `2` = MD5 <br> - `3` = ODIN <br> - `4` = OPENUDID <br> - `5` = AAID (Android Advertising ID) <br> - `6` = WINDOWSADID (Microsoft Advertising ID) <br> - `7` = RIDA (Roky id for Advertising) <br> - `8.9` = AFAI (Amazon Fire OS) <br> - `8.10` = TIFA (Tizen Identifier for Advertising (Samsung Ad ID)) <br> - `8.11` = VIDA (Vizio Advertising ID) <br> - `8.12` = LGUDID (LG Unique Device ID) | Both |
| 85 | device_id | int | The model ID of the mobile device. To map model IDs to names, use the [Device Model Service](../digital-platform-api/device-model-service.md). | Both |
| 86 | carrier_id | int | The ID of the carrier associated with the mobile device. Top map carrier IDs to names, use the [Carrier Service](../digital-platform-api/carrier-service.md). | Both |
| 87 | deal_id | int | The Deal ID associated with this impression. | Both |
| 88 | view_result | enum | The Xandr viewability measurement result of the impression. Possible values: <br> - `0` = VIEW_UNKNOWN <br> - `1` = VIEW_DETECTED <br> - `2` = VIEW_NOT_DETECTED <br> - `3` = VIEW_NOT_MEASURABLE <br> - `-1` = UNKNOWN <br><br> **Note**: For more details about viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md).<br><br>**Important**:<br>Starting September 8, 2025, Microsoft will update the Standard Log Level Data (LLD) feed for **conversion events** in Microsoft Monetize and Microsoft Invest. Only the default value `-1` = UNKNOWN will be passed for these events. <br>This change **does not affect non-conversion events**, which will continue to include the full set of possible values. | Both |
| 89 | application_id | string | The ID of the mobile application (if applicable). | Seller: Always <br> - Buyer: If allowed by seller's visibility profile |
| 90 | supply_type | enum | The type of supply. Possible values: <br> - `0` = WEB <br> - `1` = MOBILE_WEB <br> - `2` = MOBILE_APP <br> - `5` = TOOLBAR | Both |
| 91 | sdk_version | string | The version of the SDK (e.g., "3.3.0", "sdkandroid_4-0-9", "soma_ios_602"). | Both |
| 92 | ozone_id | int | **Deprecated**. The ID of the optimization zone. | Seller |
| 93 | billing_period_id | int | The ID of the billing period under which the impression was served. | Buyer |
| 94 | view_non_measurable_reason | int | The reason an impression could not be measured for viewability. Possible values: <br> - `0` = N/A. The impression was measured for viewability <br> - `1` = SCRIPT_NOT_SERVED. The viewability script was not served with the creative. For example, on mobile-app inventory. <br> - `2` = NO_SCRIPT_CALLBACK. The viewability script was served with the creative, but no callback/event was received. For example, the user left the page before the creative was served. <br> - `3` = TECHNICAL_LIMITATION. The viewability script was served and loaded, but was unable to measure for a technical reason. For example, a cross-domain iframe with Flash disabled. <br> - `-1` = UNKNOWN. The reason is unknown. <br><br> **Note**: For more information regarding viewability, see [Introduction to Viewability](../industry-reference/introduction-to-viewability.md).<br><br>**Important**:<br>Starting September 8, 2025, Microsoft will update the Standard Log Level Data (LLD) feed for **conversion events** in Microsoft Monetize and Microsoft Invest. Only the default value `-1` = UNKNOWN will be passed for these events. <br>This change **does not affect non-conversion events**, which will continue to include the full set of possible values. | Both |
| 95 | external_uid | string(100) | Specifies a string that corresponds to an external user ID for this user, passed in on the ad call by the seller. | Seller |
| 96 | request_uuid | string(36) | Specifies a unique identifier for the request. For single tag requests (such as `/ttj`), this is the same as `auction_id_64`. For multiple tag requests (such as with AST or some OpenRTB integrations), represents all of the `auction_id_64` values. | Both |
| 97 | dma | int | Specifies the ID of the designated market area for this impression. Use the [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md) to look up the area associated with the ID. | Both |
| 98 | city | int | The ID of the city for this impression. Derived from IP address of user or provided by the site associated with the impression. Use the [City Service](../digital-platform-api/city-service.md) to look up the city associated with the ID. | Both |
| 99 | mobile_app_instance_id | int | Specifies the ID of the mobile app instance for this impression. Use the [Mobile App Instance Service](../digital-platform-api/mobile-app-instance-service.md) to look up the mobile app instance associated with the ID. | Both |
| 100 | traffic_source_code | string(100) | Specifies the external source of the third party traffic for this impression. | Seller |
| 101 | external_request_id | string(100) | Specifies the seller's own version of `request_uuid` or `auction_id_64` that ties the impression back to their own data feeds. | Seller |
| 102 | deal_type | int | Specifies the type of deal: <br> - `1` = open auction deal <br> - `2` = private auction deal <br> - `3` = first look deal <br> - `4` = programmatic guaranteed deal <br> - `5` = curated deal | Both |
| 103 | ym_floor_id | int | The ID of the yield management floor that was applied to the buyer. Use the [Yield Management Floor Service](../digital-platform-api/yield-management-floor-service.md) to look up the floor associated with the ID. | Seller |
| 104 | ym_bias_id | int | The ID of the yield management bias that was applied to the buyer. Use the [Yield Management Bias Service](../digital-platform-api/yield-management-bias-service.md) to look up the bias associated with the ID. | Seller |
| 105 | is_filtered_request | int | Specifies whether or not the event was filtered for Inventory Quality reasons. <br> - `0` = event was not filtered <br> - `1` = event was filtered | Seller |
| 106 | age | int | The age of the user, if known. | Both |
| 107 | gender | string(1) | The gender of the user, if known. Possible values are `u`, `m`, and `f`. | Both |
| 108 | is_exclusive | int | Specifies which types of bids were eligible to win the auction. <br> - `0` = Both managed and non-managed bids were eligible to win. <br> - `1` = Only managed bids were eligible to win. | Seller |
| 109 | bid_priority | int | Specifies the campaign or line item's priority from the bidder only when `imp_type = 5` (managed impressions). For all other `imp_type`, values defaults to `0`. | Seller |
| 110 | custom_model_id | int | The `id` of the custom model used in the auction. When no custom model is used, this defaults to `0`. | Buyer |
| 111 | custom_model_last_modified | int | The date and time (in Unix Epoch time) since the custom model that was used in the auction was last modified. If no model was used, this defaults to `0`. | Buyer |
| 112 | custom_model_leaf_name | string | The `leaf_name` specified in the leaf that determined the winning bid. If no name is specified, or if a model was not used, this defaults to `---`. | Buyer |
| 114 | device_type | int | The type of device. Possible values are: <br> - `0` = Other Devices <br> - `1` = Desktops and Laptops <br> - `2` = Mobile Phones <br> - `3` = Tablets <br> - `4` = TV <br> - `5` = Game Console <br> - `6` = Media Players <br> - `7` = Set Top Box | Buyer |
| 115 | postal_code | string | The postal code of the user's location. Derived from IP address of user or provided by the site associated with the impression. For postal codes, see [Postal Code Service](../digital-platform-api/postal-code-service.md). | Both |
| 116 | imps_for_budget_caps_pacing | int | The total number of impressions from the master creative in page-level roadblocking. | Buyer |
| 117 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will be provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not receive the hashed version. | Both |
| 119 | latitude_trunc | string | The truncated latitude value (limited to 3 decimal places) of the user's location, when GPS data is available from a mobile device is expressed in the format "snn.ddd,snn.ddd". For example: <br> - `+12.345` or <br> - `-45.123` (where south is represented as negative). | Both |
| 120 | longitude_trunc | string | The truncated longitude value (limited to 3 decimal places) of the user's location, when GPS data is available from a mobile device is expressed in the format "snn.ddd,snn.ddd". For example: <br> - `+12.345` or <br> - `-45.123` (where west is represented as negative). | Both |
| 121 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given in the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. | |
| 122 | split_id | int32 | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. | Buyer |
| 123 | tc_string | string | The Transparency and Consent String represents the IAB Transparency and Consent Framework string. The string is base-64 url-safe encoded and can be decoded using the [IAB GDPR Transparency and Consent Framework Technical Specifications](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework). The string contains data rights, usage, and privacy information. | Both |
| 124 | partner_fees | double | The sum of all partner fees applied to this line item. | Buyer |
| 125 | external_campaign_id | string | An optional value passed in via the `cid` field on a DSP's bid (should only appear to sellers on resold impression rows). Since the `cid` field is optional, the `external_campaign_id` field will only have data when the external DSPs populate it on their bid(s). See the [Open RTB specification](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf) for more info on the `cid` field. | Seller |
| 126 | playback_method | enum | The type of initiation method. Possible values: <br> - `0` = Unknown <br> - `1` = Auto-play, sound on <br> - `2` = Auto-play, sound off <br> - `3` = Click-to-play <br> - `4` = Mouse-over <br> - `5` = Auto-play, sound unknown | Both |
| 127 | video_context | enum | The type of context. Possible values: <br> - `0` = Unknown <br> - `1` = Pre-Roll <br> - `2` = Mid-Roll <br> - `3` = Post-Roll <br> - `4` = Outstream <br> - `5` = Bannerstream <br> - `6` = In-feed <br> - `7` = Interstitial<br> - `8` = Accompanying Content Pre-roll <br> - `9` = Accompanying Content Mid-roll <br> - `10` = Accompanying Content Post-roll | Both |
| 128 | player_size_id | tinyint | The size of the video player. Possible values: <br> - `0` = Unknown <br> - `1` = Small <br> - `2` = Medium <br> - `3` = Large | Both |
| 129 | error_code | int | The VAST error code. For a detailed description of VAST error codes and their meanings, see the [IAB's VAST 4.0 documentation](https://iabtechlab.com/wp-content/uploads/2018/11/VAST4.1-final-Nov-8-2018.pdf) or refer to the list of [VAST error codes](#vast-error-codes-for-video-or-audio-creatives-only) below. | Both |
| 130 | personal_identifiers | array of messages | **Deprecated**. Please **DO NOT** use this parameter and use `extended_ids` listed below. | Both |
| 131 | device_make_id | int32 | The ID of the device make, which is generally the manufacturer of the device (e.g., Samsung). To map device make IDs to names, use the [Device Make Service](../digital-platform-api/device-make-service.md). | Both |
| 132 | postal_code_ext | string | United States only. The 9 digital U.S. postal code of the user’s location, in the format `12345-1234`. Derived from the IP address of the user or provided by the site associated with the impression. For postal codes, see [Postal Code Service](../digital-platform-api/postal-code-service.md). | Both |
| 133 | extended_ids | array of messages | A list of Extended IDs (`eids`) available in the auction, regardless of whether they specifically influenced the transaction. For more details, see [extended_ids](#extended_ids) below. | Both |
| 134 | segment_data_costs | optional double | **Unit**: `microcents` <br> `1 microcent is equivalent to 1E-8 dollars.` <br> `For Example : 200 microcent = 200/100000000 = 0.000002 dollar` <br> This includes all costs related to usage of segments in the data marketplace. Applicable when specific segments are applied in line items and associated pricing is displayed in the platform. | Buyer |
| 135 | feature_costs | optional double | **Unit**: microcents <br> `1 microcent is equivalent to 1E-8 dollars.` <br> `For Example : 200 microcent = 200/100000000 = 0.000002 dollar` <br> These are costs incurred when using a platform feature such as cross-device. | Buyer |
| 136 | fallback_ad_index | optional int | Fallback occurs when multiple SSPs get the opportunity to return a video creative and their responses are evaluated in a waterfall hierarchy. Default value is `-1`. | Seller |
| 137 | region_id | int32 | The ID of the region. To map region IDs to names, use the [Region Service](../digital-platform-api/region-service.md). | Both |
| 138 | is_private_auction | int32 | Indicates whether the auction was conducted within a Protected Audience API auction.<br>The possible values are: <br> - `0` = False <br> - `1` = True | Both |
| 139 | private_auction_eligible | int32 | Indicates whether the inventory associated with this auction was eligible for a Protected Audience API auction.<br>The possible values are: <br> - `0` = False <br> - `1` = True| Both |
| 140 | chrome_traffic_label | Enum | The Chrome label assigned for Privacy Sandbox testing, as explained [here](https://developers.google.com/privacy-sandbox/relevance/setup/web/chrome-facilitated-testing?mkt_tok=MjA0LUtaRy02ODUAAAGSpRSDWhlrfehHwCpqN8M4QmgkQgWXDQjbHOkEzJN5au1qzg2LxHPVs2EI9upbZLpE3d6O7J97Q2F1Y7-1HchIEfSb3pKGyyKyWEt3FbNGACfTFg). The type of context. The possible values are: <br> - `0` = NONE <br> - `1` = CONTROL_1_1 <br> - `2` = CONTROL_1_2 <br> - `3` = CONTROL_1_3 <br> - `4` = CONTROL_1_4 <br> - `5` = ONLY_1 <br> - `6` = ONLY_2 <br> - `7` = ONLY_3 <br> - `8` = ONLY_4 <br> - `9` = ONLY_5 <br> - `10` = TREATMENT_1_1 <br> - `11` = TREATMENT_1_2 <br> - `12` = TREATMENT_1_3 <br> - `13` = CONTROL_2 <br> - `14` = INVALID <br>**Note**: A null value may indicate that either none were sent or that the user is not associated with any labels.| Both |

### extended_ids

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 1 | id_type | unsigned 32 bit int | The source of the identifier: <br> - `10` = Trade Desk ID (Unified ID 1.0) <br> - `11` = Criteo ID <br> - `12` = NetID <br> - `13` = RampID <br> - `15` = UID 2.0 <br> - `16` = Oztam <br> - `99x` = Member-defined |
| 2 | id_value | string | Value of the identifier. For example, `"ID0001"`. <br><br> **Note**: You will only see the value of this field if you have been permissioned. |

## VAST error codes (for video or audio creatives only)

The table below shows a complete list of VAST error codes and their meanings.

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
| `301` | Timeout of VAST URI provided in Wrapper element, or of VAST URI provided in a subsequent Wrapper element. Includes request errors suchas invalid URI, unreachable or request timeout for URI, and security or other exceptions related to requesting a VAST URI. |
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
| `503` | Could not find NonLinear resource with supported type. |
| `600` | General CompanionAds error. |
| `601` | Unable to display companion because creative dimensions do not fit within Companion display area (i.e., no available space). |
| `602` | Unable to display Required Companion. |
| `603` | Unable to fetch CompanionAds/Companion resource. |
| `604` | Could not find Companion resource with supported type. |
| `900` | Undefined error. |
| `901` | General VPAID error. |
