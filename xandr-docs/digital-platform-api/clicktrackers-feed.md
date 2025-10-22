---
title: Clicktrackers Feed
description: In this article, learn about the Clicktrackers feed, their Dimensions, and Metrics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Clicktrackers feed

You can use [click trackers](click-tracker-service.md) to track user clicks on creatives served by third-party ad servers (rather than by Xandr). This reporting feed provides data on those external clicks.

> [!NOTE]
> Each row returned is for a single click event.
>
> **How to fetch this feed?**
>
> For instructions on how to fetch the clicktrackers feed, see the example on the [Bulk Reporting Feeds](bulk-reporting-feeds.md) page, but set the `"report_type"` to `"clicktrackers"` and build your request using the fields shown below.

## Dimensions

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `hour` | timestamp | `2012-02-24 12:00` | The year, month, day, and hour of the external click. |
| `day` | timestamp | `2012-02-24` | The year, month, and day of the external click. |
| `month` | timestamp | `2012-02` | The year and month of the external click. |
| `datetime` | timestamp | `2012-02-24 12:52:55` | The year, month, day, hour, minute, and second of the external click. |
| `advertiser_id` | int | `36224` | The ID of the advertiser that owns the click tracker. |
| `auction_id` | int | `7562841545137044238` | The ID used by Xandr for the external click event. |
| `line_item_id` | int | `70411` | The ID of the line item to which the click tracker is associated. |
| `insertion_order_id` | int | `2983` | The ID of the insertion order to which the line item is associated. If `0`, the line item is not associated to an insertion order. |
| `member_id` | int | `536` | The ID of the member to which the advertiser belongs. |
| `pricing_type` | enum | `"cpm"` | The way the member is paid by the advertiser. Possible values: `"none"`, `"cpm"`, `"cpc"`, `"cpa"`, `"cost_plus_cpm"`, or `"cost_plus_margin"`. |
| `publisher_id` | int | `114370` | The ID of the publisher to which the click tracker is associated. |
| `site_domain` | string | `"test-domain.com"` | The domain where the external click occurred. |
| `tag_id` | int | `690240` | The ID of the placement to which the click tracker is associated. If `0`, the click tracker is not associated to a placement. |
| `tracker_id` | int | `22` | The ID of the click tracker. |
| `user_id` | int | `5809746384815353833` | The ID used by Xandr for the user who clicked. If not known, this is `0`. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `commission_cpm` | money | `0.25` | commission_cpm | The cpm that the member pays a broker. This is set at the line item. |
| `commission_revshare` | money | `0` | commission_revshare | The revshare that the member pays a broker. This is set at the line item. |
| `media_buy_cost` | money | `0.25` | media_buy_cost | The amount paid for the external click. The third-party ad server passes this in the `"ancost"` parameter of the click tracker's query string. |
| `media_buy_rev_share_pct` | double | `0.1` | media_buy_rev_share_pct | The percentage of revenue that the member pays the publisher. |
| `revenue_value` | money | `5.00` | revenue_value | The amount that the advertiser pays the member. This is set at the line item. |

## Related topics

- [Network Analytics Feed](network-analytics-feed.md)
- [Bulk Reporting Feeds](bulk-reporting-feeds.md)
