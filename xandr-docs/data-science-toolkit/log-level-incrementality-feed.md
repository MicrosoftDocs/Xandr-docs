---
title: Data Science Toolkit - Log-Level Incrementality Feed
description: The log-level incrementality feed provides data on ad impressions for a random audience split between test and control groups.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---

# Data Science Toolkit - Log-level incrementality feed

The Log-Level Incrementality Feed provides data on impressions shown to an audience randomly split between a test group (the group exposed to ads) and control group (the group not exposed to ads). The test uses the same targeting and bidding approach for each group so that advertisers can analyze the revenue driven by users from each group to determine incremental lift from users exposed to ads. The feed contains one row per impression.

## Incrementality in Console UI (required)

1. In Xandr's UI, go to **Line Item** > **Basic Setup** > **Incrementality** and select **“Use control group”**.
1. Assign a key and a percentage of traffic to assign to the control group.

## Sequence

The [Columns](#columns) below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Data visibility and `"NULL"` values

All columns are always included, but you can only see data for which you have permission. Columns that are not visible will be shown as `"NULL"`.

`"NULL"` may be returned in cases when:

- The seller on the impression has visibility settings that hide the value of that field from buyers (assuming you are a buyer in this transaction).
- The data is not available.

## Recommended precisions/lengths of data types

In the [Columns](#columns) table below, some values in the Type column contain a recommended precision or length in parentheses. For example `string(100)` means "this string is probably (but not guaranteed to be) less than or equal to 100 characters in length".

For integers, the sizes are described in the [Integer Key](#integer-key) section.

For `numeric` (floating point) data types, we recommend being able to accept a precision of (18,6), meaning that we expect there to be a maximum total of 18 digits: 12 to the left of the decimal point, and 6 to the right.

For `string` data types, the recommended length of the field varies depending on the field. See the table below.

> [!NOTE]
> These are Recommendations, not Guarantees.
>
> The data types are meant to be accurate as documented. However, the recommended precision or length for a given data type should not be read as a guarantee. For example, a string or numeric column's value may exceed the suggested length or precision listed on this page.
>
> The recommendations are intended to help you build your system to ingest this data. You may need to do additional processing on the output of the Standard Feed to make it work with your particular integration.

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

| Column Index | Column Name | Type | Description |
|:---|:---|:---|:---|
| 01 | `date_time` | UNIX Epoch time | The time and date of the impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 02 | `auction_id_64` | bigint | The Xandr unique auction identifier. |
| 03 | `price` | numeric (18,6) | The dollar amount * 1000 that a network is paying for an impression. |
| 04 | `buyer_member_id` | int | The member ID of the buyer. |
| 05 | `advertiser_id` | int | The ID of the advertiser. |
| 06 | `campaign_group_id` | int | The ID of line item. |
| 07 | `campaign_id` | int | The ID of the campaign. |
| 08 | `creative_id` | int | The ID of the creative served. |
| 09 | `creative_freq` | int | The creative-level frequency (times the user has seen this creative). |
| 10 | `creative_rec` | int | The creative-level recency in minutes (how long it has been since the user has seen this creative ad). |
| 11 | `advertiser_freq` | int | The advertiser-level frequency (times the user has seen a creative by this advertiser). |
| 12 | `advertiser_rec` | int | The creative-level recency in minutes (how long it has been since the user has seen a creative ad by this advertiser). |
| 13 | `is_remarketing` | tinyint | Indicates that a new segment pixel is for remarketing. |
| 14 | `user_group_id` | int | The group ID, if the advertiser separates users into groups for purposes of A/B testing. |
| 15 | `media_buy_cost` | numeric (18,6) | The dollar amount * 1000 that a network is paying for an impression. |
| 16 | `is_default` | int | Indicates that a default creative served. |
| 17 | `pub_rule_id` | int | The ID for the publisher rule, which is set up in and defines how the publisher is paid. |
| 18 | `media_buy_rev_share_pct` | numeric(18,6) | The publisher revenue share or the percent of booked revenue the seller shares with its publisher. This is a fraction between 0 and 1. If you multiply by 100, you get the percentage value. |
| 19 | `pricing_type` | string(3) | The line item pricing type, or how the buyer network gets paid by the advertiser (e.g. cpm, cpc). |
| 20 | `can_convert` | tinyint | Indicates that conversion pixels associated are associated with the impression. |
| 22 | `control_pct` | numeric(18,6) | The percentage of traffic sent to the control group. |
| 23 | `control_creative_id` | int | The ID of the creative served to the control group. |
| 24 | `cadence_modifier` | numeric(18,6) | The cadence modifier for the impression, which is the number by which the bid was multiplied. |
| 25 | `advertiser_currency` | string | The currency used by advertiser. |
| 26 | `advertiser_exchange_rate` | numeric(18,6) | The exchange rate on day of event. Rate is updated daily at 4 PM GMT. |
| 27 | `insertion_order_id` | int | The ID for insertion order, if used. |
| 28 | `predict_type` | tinyint | The optimization phase of the bid. Possible values:<br> `-2` = No predict phase<br> `-1` = Base predict phase<br> `0` = Learn giveup<br> `1` = Learn<br> `2` = Throttled<br> `3` = Optimized<br> `4` = Biased<br> `5` = Optimized 1<br> `8` = Optimized giveup<br> `9` = Base bid below giveup |
| 29 | `predict_type_goal` | int | The goal amount of the specified predict type. |
| 30 | `revenue_value_dollars` | numeric(18,6) | The dollar amount earned by network on impression. |
| 31 | `revenue_value_adv_curr` | string | The dollar amount earned on impression, displayed in your advertiser currency. |
| 32 | `commission_cpm` | numeric(18,6) | Specifies the commission in cpm, if used. |
| 33 | `commission_revshare` | numeric(18,6) | Specifies the commission in revenue share, if used. |
| 34 | `serving_fees_cpm` | numeric(18,6) | The serving fees in addition to media costs to when serving an ad. |
| 35 | `serving_fees_revshare` | numeric(18,6) | The serving fees in addition to revenue sharing when serving an ad. |
| 36 | `publisher_currency` | string(3) | The currency in which publisher is paid. |
| 37 | `publisher_exchange_rate` | numeric(18,6) | The exchange rate (publisher currency: USD) on the day of the transaction. |
| 38 | `payment_type` | tinyint | The method by which the buyer is paying for the impression. Possible values:<br> `-1` = No payment<br> `0` = CPM<br> `1` = CPC<br> `2` = CPA<br> `3` = Owner CPM<br> `4` = Owner revshare |
| 39 | `payment_value` | numeric(18,6) | The amount paid for the impression using the specified payment type. |
| 40 | `creative_group_freq` | int | The creative-group-level frequency (times the user has seen this creative group). |
| 41 | `creative_group_rec` | int | The creative-group-level recency (how long it has been since the user has seen this creative group). |
| 42 | `revenue_type` | tinyint | The method by which the buyer network gets paid by the advertiser, or how the method by which the seller network was paid by the buyer network. Possible values:<br><br> `-1` = No payment<br> `0` = Flat CPM<br> `1` = Cost Plus CPM<br> `2` = Cost Plus Margin<br> `3` = CPC<br> `4` = CPA<br> `5` = Revshare<br> `6` = Flat Fee<br> `7` = Variable CPM (vcpm)<br> `8` = Estimated CPM (est_cpm) |
| 43 | `apply_cost_on_default` | int | Indicates whether to apply cost on default creatives. |
| 44 | `instance_id` | int | Specifies the ID of the mobile app instance for this impression. Use the  [Mobile App Instance Service](../digital-platform-api/mobile-app-instance-service.md) to look up the mobile app instance associated with the ID. |
| 45 | `vp_expose_gender` | bool | Indicates whether gender is exposed.  |
| 46 | `targeted_segments` | array | The IDs of the targeted segment pixels. |
| 47 | `ttl` | int | The time to live (TTL) of the segment pixels. |
| 48 | `auction_timestamp` | UNIX Epoch time | The time and date of the impression (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 49 | `data_costs` | numeric(18,6) | Total data costs the buyer paid for the given impression. |
| 50 | `targeted_segment_list` | array | The IDs of the targeted segment pixels. |
| 51 | `campaign_group_freq` | int | The line-item-level frequency (how often the user has seen an ad from this line item). |
| 52 | `campaign_group_rec` | int | The line-item-level recency in minutes (how long it has been since the user has seen an ad from this line item). |
| 53 | `insertion_order_freq` | int | The insertion-order-level frequency (how often the user has seen an ad from this insertion order). |
| 54 | `insertion_order_rec` | int | The insertion-order-level recency in minutes (how long it has been since the user has seen an ad from this insertion order). |
| 55 | `buyer_gender` | string(1) | The gender of the user, if known. Possible values are `"u"`, `"m"`, and `"f"`. |
| 56 | `buyer_age` | int | Age of the user, if known. |
| 57 | `custom_model_id` | int | The ID of the custom model used in the auction. When no custom model is used, this defaults to `0`. |
| 58 | `custom_model_last_modified` | int | The date and time (in Unix Epoch time) since the custom model that was used in the auction was last modified. If no model was used, this defaults to `0`. |
| 59 | `custom_model_output_code` | string(7) | An optional string value that will be passed through to logs and reporting to aid with debugging and performance analysis. `custom_model_output_code` may be up to seven ASCII (7-bit) characters and is not required to be unique. |
| 60 | `bid_priority` | int | Specifies the campaign or line item's priority for the managed impressions only. For all other impressions, defaults to `0`. |
| 61 | `is_control` | tinyint | Indicates whether the creative served is a control creative.<br> `0` = test impression<br> `1` = control impression<br> `2` = no cookie user. (Xandr does not include no cookie users to avoid skewing the size of test and control groups). |
| 62 | `site_domain` | string(100) | The most granular identifier of the site available to buyers (This may be the domain of a supply partner, ex: [doubleclick.com](https://marketingplatform.google.com/about/enterprise/); network who owns resold inventory; or it may just say 'resold inventory'). Exposure to buyer depends on the seller's visibility profile. |
| 63 | `eap` | numeric(18,6) | The estimated average price for placement tag, in dollars unless another advertiser currency is specified. |
| 64 | `ecp` | numeric(18,6) | The estimated clear price for placement tag, in dollars unless another advertiser currency is specified. |
| 65 | `user_id_64` | bigint | The Xandr 64-bit User ID stored in the Xandr cookie store. This field is `0` when Xandr does not have a match for this user or the user's browser doesn't accept cookies. It will be `-1` for opt-out users. |
| 66 | `predicted_engagement_rate` | int | Percentage calculated to predict how likely the impression is to be viewable. |
| 67 | `seller_member_id` | int | The member ID of the seller. |
| 68 | `bidder_auction_rank` | int | The hypothetical ordered rank of the current bid, calculated by the bidder in comparison with other bids sent back to Impression Bus. The top bid is auction rank 0 (0-indexed). |
| 69 | `hashed_user_id_64` | bytes | The user ID represented as a 64-bit hashed value. |
| 70 | `partition_time_millis` | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |
| 71 | `device_unique_id` | string | **Note**: This field will only be populated for clients who have signed a contract addendum.  For more information, please contact your Xandr Account Manager.<br><br>The unique identifier representing the mobile device. The numeric prefix indicates the type of unique device identifier:<br>`0` = IDFA (Apple ID for Advertising)<br>`1` = SHA1<br>`2` = MD5<br>`3` = ODIN<br>`4` = OPENUDID<br>`5` = AAID (Android Advertising ID)<br>`6` = WINDOWSADID (Microsoft Advertising ID)<br>`7` = RIDA (Roky id for Advertising)<br>`8.9` = AFAI (Amazon Fire OS)<br>`8.10` = TIFA (Tizen Identifier for Advertising (Samsung Ad ID))<br>`8.11` = VIDA (Vizio Advertising ID)<br>`8.12` = LGUDID (LG Unique Device ID) |
| 72 | `ip_address` | string | **Note**: This field will only be populated for clients who have signed a contract addendum.  For more information, please contact your Xandr Account Manager.<br><br> The IP address of user. |

## Related topic
[Incrementality](./incrementality.md)
