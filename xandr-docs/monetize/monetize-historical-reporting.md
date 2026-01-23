---
title: Microsoft Monetize - Historical Reporting
description: Learn how Monetize Historical Reporting consolidates legacy reports, offering enhanced analytics, streamlined navigation, and improved performance insights.
ms.date: 1/22/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Microsoft Monetize -  Historical reporting

## Overview

Historical report is the primary analytics report in Microsoft Monetize, offering comprehensive data across a wide range of dimensions and metrics. It consolidates more than ten legacy report types, including [Network Analytics](network-analytics-report.md), [Seller Brand Review](seller-brand-review-report.md), and [Seller Fill and Delivery](seller-fill-and-delivery-network-report.md). It reduces the number of report types a user needs to interact with, providing features to improve usability such as categorization of `Dimensions` and `Metrics` and comprehensive search capabilities. <br><br> Historical report is built from two datasets accessible through a single interface, with `Dimension` and `Metric` incompatibilities surfaced during selection. The expanded range of options provides a more detailed view of data across multiple aspects of delivery and inventory, with additional reportable dimension combinations, such as placement and device. The Historical report includes most of the data available in the legacy reporting system. 

> [!NOTE]
> During the Alpha phase, additional dimensions and metrics are added to address key feature gaps compared to the legacy reports. Data in the Historical report is available from 10 October 2024 for general access, with earlier availability in 2024 for clients participating in the Alpha phase. The reporting interface in Microsoft Monetize provides access to the Historical report for Network users. Access to all existing report types is available during the Alpha phase, along with support for Publisher and Advertiser users.


### Report mappings

Delivery Analytics and Inventory Analytics reports are consolidated into a single Historical report builder experience. This integration streamlines reporting workflows and provides expanded insights into performance and inventory that provides:
- Consolidated reporting for comprehensive performance analysis
- Broader coverage of metrics and dimensions

| Legacy Report Name      | Mapped Report Name | API Name                       |
|---------------------|-------------------|-----------------------------------  |
| Delivery Analytics  | Historical Report | `monetize_creative_brand_analytics` |
| Inventory Analytics | Historical Report | `monetize_supply_analytics`         |

> [!NOTE]
> Coverage of dimensions and metrics is in progress. Additional fields are being added to support the deprecation of legacy report types.

## Legacy reports

Legacy reports will no longer receive Microsoft Monetize data starting `early 2026`. Historical data will remain accessible based on each report’s standard retention period or `2 years 6 months`, whichever is shorter, with some specific dimensions in the report having shorter retentions of `99 days` or `14 months`, mirroring retention of equivalent fields in relevant Legacy reports. These new report types automatically include data for all impression types except for `7=RTB` (a buying transaction on supply from another seat to your own) for Microsoft Monetize sellers. 
> [!NOTE]
> - Communication will be provided in advance to support the transition process.
> - Reporting for Microsoft Invest and External SSPs is not included in these datasets.


## Legacy report types

#### Network report types

The reports consolidate Delivery and Inventory analytics, streamlining data access. The table below maps the consolidated reports to their legacy counterparts and API names:

| **UI Report Name**                  | **API Report Name**                          |
|-------------------------------------|---------------------------------------|
| Network Analytics                   | network_analytics                     |
| Seller Brand Review                 | seller_brand_review                   |
| Seller Brand Review Hourly (alpha)  | seller_brand_review_hourly (alpha)    |
| Seller Fill and Delivery Network    | seller_fill_and_delivery_network      |
| Seller Site Domain                  | seller_site_domain                    |
| Site Domain Performance             | network_site_domain_performance       |
| Device Analytics                    | network_device_analytics              |
| Carrier Analytics                   | network_carrier_analytics             |
| Prebid Server Analytics             | prebid_server_analytics               |
| Audio Analytics                     | audio_analytics_network               |

### Advertiser or Publisher report types

| **UI Report Name**                | **API Report Name**                        |
|-----------------------------------|-------------------------------------|
| Advertiser Analytics              | advertiser_analytics                |
| Site Domain Performance           | site_domain_performance             |
| Advertiser Video Analytics        | video_analytics_network_advertiser  |
| Publisher Analytics               | network_publisher_analytics         |
| Not Available                     | publisher_brand_review              |
| Seller Fill and Delivery Publisher| seller_fill_and_delivery_publisher  |

## Historical report creation

The Historical report enables streamlined report creation. Users can select from various **Dimensions**, **Metrics**, and **Filters** to customize their reports.

:::image type="content" source="media/create-new-report.png" alt-text="The screenshot shows how to create new reports.":::

## Timing of Report Events

The Historical report enables metrics to be attributed to the **hour of the originating ad request**, rather than the time when each subsequent event occurs. This ensures consistency when calculating rates for events that may occur hours after the initial ad call, such as video impressions, native impressions, and conversions.

### Example

In the example below, a video ad request has a 6-hour TTL, and its related events occur over several hours:

| Event                 | Event Time |
|----------------------|------------|
| Ad Request           | 08:00      |
| Impression           | 10:00      |
| Post-View Conversion | 11:00      |

In the **Historical report**, all these events are attributed back to the **08:00** hour when the ad request was made.

#### Historical Report View

| Hour | Ad Requests | Imps | Post-View Conversions | Fill Rate | Conversion Rate |
|------|-------------|------|------------------------|-----------|------------------|
| 08:00 | 1 | 1 | 1 | 100% | 100% |

### Differences Compared to Legacy Reports

Legacy reports attribute events to the **actual event time**. Using the same example, the legacy reporting view would look like this:

| Hour | Ad Requests | Imps | Post-View Conversions | Fill Rate | Conversion Rate |
|------|-------------|------|------------------------|-----------|------------------|
| 08:00 | 1 | 0 | 0 | 0% | 0% |
| 10:00 | 0 | 1 | 0 | 0% | 0% |
| 11:00 | 0 | 0 | 1 | 0% | 0% |

Because timestamps are handled differently, **metric counts will not match exactly** between Historical reports and legacy reports when viewed at the day or hour level. This difference is expected and reflects the underlying attribution logic.

## Understanding the ad request to impression funnel

The **Historical Report**, starting **12 November 2025**, includes metrics that help analyze the **impression request funnel** and troubleshoot integrations.

These metrics were previously available in the [Seller Fill and Delivery](seller-fill-and-delivery-network-report.md) report. They are now exposed with **more granular dimensions and filters** to support deeper analysis.

> [!Note]  
> Non-transactional metrics such as **Ad Requests**, **Ad Responses**, and **Filtered Requests** are provided for **directional troubleshooting only** and **must not be used for billing or financial reconciliation**.

---

## Ad request flow

The following diagram illustrates how an ad request progresses through Microsoft Monetize, from receipt to final outcome.

:::image type="content" source="media/ad-flw.png" alt-text="The screenshot shows ad request flow.":::

---

## Ad request lifecycle

### Ad requests received

**Ad Requests Received** counts the total number of **unique impressions** sent to Microsoft Monetize.

- Each impression is counted individually.
- This count is independent of message structure. For example, if multiple impressions are included in a single OpenRTB request, each impression is counted separately.
- This metric supports a **limited set of dimensions** and is not reportable with certain dimensions, such as **Operating System**.

---

### Ad requests auctioned

**Ad Requests Auctioned** counts impressions that were **submitted to the auction process**.

- Impressions are counted using the same methodology as *Ad Requests Received*.
- Only impressions that enter the auction are included.

---

### Filtering

The first step of the auction process evaluates **inventory quality**.

- If an impression is filtered before bidding, it is counted as a **Filtered Request**.
- Filtered requests are logged with a **filtered request reason**.
- Filtered requests do not proceed to bidding.

---

### Ad responses

If the auction results in at least one **eligible bid** from managed or third-party demand, an **Ad Response** is counted.

---

### Impressions sold

Impressions are considered sold when an **impression tracker** is received within the **TTL (time to live)** for the creative media type.

Impressions can be:
- **Kept impressions** (managed demand)
- **Resold impressions** (third-party demand)

---

### Video player errors

**Video Player Errors** are counted when a video error is reported after the auction completes.

> [!Note]  
> This metric may not align with the Seller Fill and Delivery report due to updates in processing logic.

---

### Default impressions and no responses

If the impression returned is a **default creative**, it is counted separately, including:
- Default impressions
- Default no responses (non-video)
- Video default no responses

If an **impression tracker is not received within the TTL**, the outcome is counted as **Bid Sent No Responses**.  
This behavior applies to both standard and default creatives.

---

### No eligible demand

When no managed, programmatic, or default demand is eligible, the request is counted as **Ad Requests No Eligible Demand**.

- **Blank impressions** are recorded for specific integrations (for example, `/UT`).
- Blank impressions are not recorded for integrations where a downstream auction is expected (for example, Prebid).
- **PSAs** are recorded when no eligible demand exists and PSAs are enabled for the placement.

---

## Metrics

| UI name | API field | Description |
|-------|----------|-------------|
| Ad Requests Received | `ad_requests` | Total count of unique impressions sent to Microsoft Monetize |
| Ad Requests Auctioned | `ad_requests_auctioned` | Total count of unique impressions evaluated for auction |
| Filtered Requests | `filtered_requests` | Total count of auctioned requests filtered pre-bid for inventory quality |
| Ad Requests No Eligible Demand | `ad_requests_no_creative` | Total count of requests with no eligible managed, programmatic, or default demand |
| Ad Responses | `ad_responses_total` | Total count of auctions with at least one eligible bid |
| Video Ad Responses | `ad_responses` | Total count of auctions with at least one eligible video bid |
| Bid Sent No Responses | `bid_sent_no_responses` | Bid responses returned but where the creative ultimately did not render |
| Default No Responses | `defaults_no_responses` | Requests where a default creative was sent but no response was received |
| Video Default Errors | `video_default_errors` | Errors reported when a default video creative should have served |
| Video Player Errors | `video_player_errors` | Errors reported after VAST XML delivery (maximum 1 per auction) |
| Response Rate | `response_rate` | Total ad responses ÷ (Ad Requests − Filtered Requests) |
| Win Rate | `win_rate` | (Kept + Resold impressions) ÷ Total Ad Responses |
| Fill Rate | `fill_rate` | (Kept + Resold impressions) ÷ Ad Requests Auctioned |
| Ad Request RPM | `ad_request_rpm` | Seller revenue per 1,000 auctioned ad requests |

---

## Bid sent no responses: common scenarios

This metric typically occurs when Microsoft Advertising returns a bid, but the creative does not render. Common scenarios include:

- An external system (for example, Prebid or a waterfall-based ad server) selects a different bid.
- The user leaves the page before the impression tracker fires.
- Lazy loading prevents the ad from rendering.
- A video ad is requested but never plays.

---

## Dimensions available only for transacted impressions

For the following metrics:
- **Ad Requests Received**
- **Ad Requests Auctioned**
- **Filtered Requests**
- **Bid Sent No Responses**

The dimensions listed below are **not reportable** and only populate when an impression is transacted:

- Viewability metrics  
- Browser  
- Creative  
- Brand  
- Carrier  
- Deal Type  
- Curator  
- Audit Status  

## Time frame and data retention

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports.

However, all time ranges are not available for every report.

- **Custom**
- **Current Hour** 
- **Last Hour** 
- **Today** 
- **Yesterday** 
- **Last 48 Hours** 
- **Last 2 Days** 
- **Last 7 Days** 
- **Last 14 Days** 
- **Last 30 Days** 
- **Month to Date** 
- **Month to Yesterday**

:::image type="content" source="media/time-ranges.png" alt-text="The screenshot shows time ranges that define the period from which data is extracted for reports.":::

### Data retention period

- **Hourly data:** Data is retained for the last 100 days.
- **Cumulative data:** Data is retained for up to 2 years and 2 months.
- **Current maximum data availability:** Data is retained for 90 days (planned extensions forthcoming).

## Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- **Hourly:** Data is grouped by the hour.
- **Daily:** Data is grouped by the day.
- **Monthly:** Data is grouped by the month.
- **Cumulative:** Data is covered by an entire selected period.

:::image type="content" source="media/intervals-cumulative.png" alt-text="The screenshot illustrates Intervals, which define how data is grouped in the report, such as hourly, daily, monthly, or cumulative.":::

<!--
## Data availability

- **Maximum retention:** 2 years and 2 months.
- **Current maximum data availability:** 90 days (planned extensions forthcoming). -->

## Adjustments

Adjustments allocate revenue from fixed-fee line items for reporting. The allocation timing depends on the line item settings, which determine whether the fixed fee is distributed daily or at the end of the flight. Revenue is allocated proportionally to the number of impressions served during the day or flight, calculated on an hourly basis. At least one impression must be served on a given day for revenue to be allocated.

In Historical reports, these adjustments appear with the **Revenue Type** set to **Flat Fee**.

### Example

For example, line item 1234 has a fixed fee of $1,000 per day. Following is the adjustments for the line item:

| Hour         | Impressions | Revenue Allocated |
|--------------|-------------|-------------------|
| 2025-11-03 12 | 250         | $250              |
| 2025-11-03 13 | 500         | $500              |
| 2025-11-03 15 | 200         | $200              |
| 2025-11-03 18 | 50          | $50               |
| 2025-11-04 08 | 80          | $800              |
| 2025-11-04 09 | 20          | $200              |

### Supported date 
Adjustments revenue is available in reports for any adjustments created on or after January 28, 2025.

### Dimensions/filters reportable with adjustment revenue

The following dimensions are available when reporting on adjustment revenue.

| Name in UI            | Name in API          |
|-----------------------|----------------------|
| Advertiser            | advertiser           |
| Advertiser ID         | advertiser_id        |
| Advertiser Name       | advertiser_name      |
| Buyer Member          | buyer_member         |
| Buyer Member ID       | buyer_member_id      |
| Buyer Member Name     | buyer_member_name    |
| Buyer Seat            | buyer_seat           |
| Buyer Seat ID         | buyer_seat_id        |
| Buyer Seat Name       | buyer_seat_name      |
| Country Code          | geo_country          |
| Country/region Name          | geo_country_name     |
| Impression Type       | imp_type             |
| Impression Type ID    | imp_type_id          |
| Impression Type Name  | imp_type_name        |
| Insertion Order       | insertion_order      |
| Insertion Order ID    | insertion_order_id   |
| Insertion Order Name  | insertion_order_name |
| Is Curated            | is_curated           |
| Line Item             | line_item            |
| Line Item ID          | line_item_id         |
| Line Item Name        | line_item_name       |
| Payment Type          | payment_type         |
| Payment Type ID       | payment_type_id      |
| Placement             | placement            |
| Placement ID          | placement_id         |
| Placement Name        | placement_name       |
| Publisher             | publisher            |
| Publisher ID          | publisher_id         |
| Publisher Name        | publisher_name       |
| Revenue Type          | revenue_type    |
| Revenue Type ID       | revenue_type_id |
| Placement Group       | site            |
| Placement Group ID    | plmt_grp_id     |
| Placement Group Name  | plmt_grp.name   |

If you apply a filter that isn’t included in this list, the adjusted revenue won’t be returned in the report. Similarly, if you add a dimension that isn’t in this list, the adjusted revenue for rows containing that dimension value will be zero.

### Adjustment Processing Timelines 

Adjustments are processed at the end of the line item’s day or flight and may take up to nine hours to complete and appear in reporting.

**Example**

If a line item is set to the CET time zone and allocates a fixed fee of $1,000 per day, the adjustment processing will begin at 01:00 UTC. The revenue is expected to appear in reporting by 10:00 UTC.

## Filters

Filters allow you to limit displayed data by specific dimensions. Available filters include:

- Advertiser name
- Publisher name
- Impression type

:::image type="content" source="media/data-availability-filters.png" alt-text="The screenshot shows filter options to include or exclude data for specific dimensions.":::

## Dimensions

<!-- Users can filter and group data using various **dimensions** and **metrics**.-->

> [!WARNING]
> Some Dimensions, such as **Device Make** and **Creative**, cannot be used together. An info message will indicate unavailable combinations.

| Column| Filter?| Description|
|---|---|---|
|`Advertiser`| No | The advertiser associated with delivering the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Advertiser ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Advertiser Name` (Selectable via "Show IDs as separate column" option)| No| The name of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Bidder`| No | The Bidder object (in most cases this is a DSP).|
| `Bidder ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the Xandr Bidder object (in most cases this is a DSP).|
| `Bidder Name` (Selectable via "Show IDs as separate column" option)| No | The name of the Xandr Bidder object (in most cases this is a DSP).|
| `Billing Period`| Yes | The ID of the Billing Period. |
| `Booked Imps Budget Daily`| No | The daily impression budget of the Insertion order's billing period.|
| `Booked Imps Budget Lifetime`| No | The lifetime impression budget of the Insertion order's billing period.|
| `Start Date`| No | The earliest date of the insertion order's billing period. <br> **NOTE:** This field or feature is part of functionality currently in either Alpha or Beta phase and subject to change.|
| `End Date`| No | The last date of the insertion order's billing period. <br> **NOTE:** This field or feature is part of functionality currently in either Alpha or Beta phase and subject to change. |
| `External Code`| No | The custom code for the billing period.|
| `Buyer Member`| No | The name of the Xandr buyer member that purchased the impression. 	|
| `Buyer Member ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the Xandr buyer member that purchased the impression.|
| `Buyer Member Name` (Selectable via "Show IDs as separate column" option)| No | The Name of the Xandr buyer member that purchased the impression.|
| `Buyer Seat`| No | The seat for the Bidder. This enables reporting on sub-seats for bidders that do not have `buyer_member_id` breakouts.|
| `Buyer Seat ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have `buyer_member_id` breakouts. |
| `Buyer Seat Name` (Selectable via "Show IDs as separate column" option)| No | The name of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have `buyer_member_id` breakouts.|
| `Buyer Seat Code` | No | The custom buyer seat ID (submitted by DSP) which was used to bid on the impression.|
| `Flight Id`| No | The ID of the Line item flight under which the impression was purchased.|
| `Booked Impressions Budget Daily`| No| The daily impression budget for the Line item's flight.|
| `Booked Impressions Budget Lifetime`| No | The lifetime impression budget for the Line item's flight.|
| `Start Date` | No | The start date of the Line item's flight.|
| `End Date`| No | The end date of the Line item's flight.|
| `Insertion Order`| Yes | The Insertion order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Insertion Order ID` (Selectable via "Show IDs as separate column" option)| No | The Insertion order ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Insertion Order Name` (Selectable via "Show IDs as separate column" option)| No | The Insertion order name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Billing Code`| No | The billing code associated with the Insertion order (if there is one).|
| `End Date`| No | The end date of the Insertion order (for legacy insertion orders).|
| `Start Date`| No | The start date of the Insertion order (for legacy insertion orders).|
|`State`| No | The state of the Insertion order (e.g., active, inactive).|
| `Type` | Yes | The type of Insertion order associated with the impression (e.g. Legacy, Seamless).|
| `Line Item` | No| The Line item order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| `Line Item ID` (Selectable via "Show IDs as separate column" option) 	| Yes | The Line item ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Line Item Name` (Selectable via "Show IDs as separate column" option)| No | The Line item name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Comments`| No | Any comments that have been entered for this line item.|
| `Line Item.Start Date` | No | The start date of the Line item.|
| `Line Item.End Date`| No | The end date of the Line item. |
| `Line Item.Status` | No | The state of the line item (For example, Active or Inactive).|
| `Code`| No | The optional external code applied to the Line item.|
| `Priority`| Yese | The bidding priority for a Line item that targets direct inventory. For more information, see Bidding Priority in the UI Documentation. <br> **Possible values:** - 1 - 20, where 20 is the highest priority.|
| `Line Item Subtype` | Yes | The Line item subtype (e.g., Augmented, Deal, Guaranteed). |
| `Line Item Subtype ID`(Selectable via "Show IDs as separate column" option) | No | The Line item subtype ID.|
| `Line Item Subtype Name` (Selectable via "Show IDs as separate column" option)| No | The Line item subtype name. |
| `LI: Sales Rep (reporting label)`| Yes | A custom reporting label field containing the sales representative. You may only select one reporting label per report.|
| `LI: Trafficker(reporting label)` | Yes | A custom reporting label field containing the trafficker. You may only select one reporting label per report. |
| `LI: Type(reporting label)` | Yes | A custom reporting label field used to list the Line item type (For example, Retargeting LI). This is not the same as the Type attribute described above. You may only select one reporting label per report.|
| `IO: Type (reporting label)`| Yes | A custom reporting label field used to list the insertion order type (For example, Branding IO). This is not the same as the Type attribute described above. You may only select one reporting label per report.|
| `IO: Sales Rep (reporting label)` | Yes | A customer reporting label field used to list the sales representative associated with the Insertion order. You may only select one reporting label per report.|
| `IO: Trafficker (reporting label)` | Yes | A customer reporting label field used to list the trafficker associated with the insertion order. You may only select one reporting label per report.|
| `Placement`| No | The Xandr placement for the impression.|
| `Placement ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the Xandr placement for the impression.|
| `Placement Name` (Selectable via "Show IDs as separate column" option)| No | The name of the Xandr Placement for the impression.|
| `Code`| No | The code of the Xandr placement for the impression.|
| `Code2`| No | The code of the Xandr placement for the impression. |
| `Code3`| No | The code of the Xandr placement for the impression.|
| `Placement Group`| No | Xandr placement Group for the impression.|
| `Placement Group ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the Xandr placement group for the impression. |
| `Placement Group Name` (Selectable via "Show IDs as separate column" option)| No | The name of the Xandr placement group for the impression.|
| `Placement Group.Code`| No | The code of the Xandr placement group for the impression.|
| `Publisher` | No | The Xandr Publisher for the impression. |
| `Publisher ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID of the Xandr publisher for the impression.|
| `Publisher Name` (Selectable via "Show IDs as separate column" option)| No | The name of the Xandr publisher for the impression. |
| `Brand`| No | The Brand as determined by the Xandr creative audit or self assigned for managed traffic |
| `Brand ID` (Selectable via "Show IDs as separate column" option)| Yes | The ID for the Brand as determined by the Xandr creative audit or self assigned for managed traffic |
| `Brand Name` (Selectable via "Show IDs as separate column" option)| No | The name for the Brand as determined by the Xandr creative audit or self assigned for managed traffic|
| `Brand Category ID` | Yes | The parent category ID for the creative's assigned brand|
| `Brand Category Name` | No | The parent category name for the creative's assigned brand                                         |
| `Creative` | No | Creative that served. It will only be populated for managed impressions.|
| `Creative ID` (Selectable via "Show IDs as separate column" option) | Yes | The Xandr ID for the creative that served.                                                         |
| `Creative Name` (Selectable via "Show IDs as separate column" option) | No | The Xandr name for the creative that served. The name will only be populated for managed impressions. |
| `Creative Code`  | No | The code of the creative. |
| `Creative Media Type` | No | The media type of the creative that transacted                                                     |
| `Creative Media Type ID` (Selectable via "Show IDs as separate column" option) | No | The media type ID of the creative that transacted                                                  |
| `Size` | Yes | For display creatives, this is the creative `width` x `height` in pixels |
| `Domains Exposed Id` | No | Whether this inventory's domains are exposed for targeting by buyers. **Allowed values:** <br> - "Exposed" <br> - "Not exposed" |
| `Domains Exposed`| No | Whether this inventory's domains are exposed for targeting by buyers. **Allowed values:** <br> - "Exposed" <br> - "Not exposed" |
| `Exposed For Resale` | No | Viewability profile, used by sellers to expose/hide their `content_categories` info to buyers |
| `Exposed For Resale Id` | No | Viewability profile, used by sellers to expose/hide their publisher info to buyers |
| `Allowed Media Types` | No | An array of the permitted media types for the impression  |
| `Audit Type` | No | The type of audit performed on the domain where the impression occurred.                           |
| `Audit Type ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the type of audit performed on the domain where the impression occurred.|
| `Audit Type Name` (Selectable via "Show IDs as separate column" option) | No | The name of the type of audit performed on the domain where the impression occurred. |
| `Browser`| No | The Name and ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service. |
| `Browser ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service.         |
|`Content Category`| No | The ID and name of the universal content category associated with the audited domain.                                           |
| `Content Category ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the universal content category associated with the audited domain.                                                   |
| `Content Category Name` (Selectable via "Show IDs as separate column" option) | No | The name of the universal content category associated with the audited domain.|
| `Fold Position` | No | The fold position, i.e. where on the page the placement is located. For allowed values, see fold_position_id.|
| `Fold Position Id`| Yes | The ID of the fold position, i.e. where on the page the placement is located. **Possible values for impressions:**<br> - 0 = "unknown" <br> - 1 = "above" <br> - 2 = "below". |
| `Supply Type` | Yes | The ID of the type of inventory.|
| `Supply Type Name` | No | The type of inventory. **Possible values:** <br> - "web" <br> - "mobile_web" <br> - "mobile_app" <br> - "facebook_sidebar". |
| `Prebid Server Eligible` | Yes | Yes if PSP was eligible to bid into the auction for the impression. |
| `Prebid Server Eligible` | No | Yes if PSP was eligible to bid into the auction for the impression. |
| `SSP` | No | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `SSP ID` (Selectable via "Show IDs as separate column" option) | No | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `SSP Name` (Selectable via "Show IDs as separate column" option) | No | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `Deal` | No | The name and ID of the affected deal. |
| `Deal ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the deal.|
| `Deal Name` (Selectable via "Show IDs as separate column" option) | No | The name of the affected deal.|
| `Deal Type` | Yes | Possible values: Open Auction (1), Private Auction (2), First Look (3), Programmatic Guaranteed (4), Curated (5 - only relevant for Curators). |
| `Revenue Type` | No | For managed line items, this is the basis on which the booked revenue gets recorded for the Seller.  |
| `Revenue Type` (Selectable via "Show IDs as separate column" option) | Yes | The basis on which the advertiser has agreed to pay you for the impression.   |
| `Carrier` | No | The carrier for the device on which the impression was served.|
| `Carrier ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the carrier for the device on which the impression was served.|
| `Carrier Name` (Selectable via "Show IDs as separate column" option) | No | The name of the carrier for the device on which the impression was served.  |
| `Device Make`| No | The device manufacturer |
| `Device Make ID (Selectable via "Show IDs as separate column" option)` | Yes | The ID of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). |
| `Device Make Name` (Selectable via "Show IDs as separate column" option)| No | The name of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). To retrieve a complete list of device make IDs and names, use the Device Make Service.|
| `Device Model` | No | The ID and name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). |
| `Device Model ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the device model on which the impression was served. The model is generally the specific product (i.e., Iphone). |
| `Device Model Name` (Selectable via "Show IDs as separate column" option) | No | The name of the device model on which the impression was served. The model is generally the specific product (i.e., Iphone). |
| `Device Type` | No | The device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box |
| `Device Type ID`| Yes | The ID of the device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box |
| `Operating System` | No | The name of the operating system of the device followed by the ID (Microsoft Advertising format). |
| `Operating System ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the operating system of the device. |
| `Operating System Name` (Selectable via "Show IDs as separate column" option) | No | The name of the operating system of the device. |
| `Operating System Family` | No | The name of the operating system family (e.g., Android, Microsoft Windows) of the device followed by the ID (Microsoft Advertising format). |
| `Operating System Family ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the operating system family associated with the device the impression was served on. |
| `Operating System Family Name` (Selectable via "Show IDs as separate column" option) | No | The name of the operating system family associated with the device the impression was served on. |
| `Curator Member`| No | The ID of the curator that was present in the transaction |
| `Curator Member ID` (Selectable via "Show IDs as separate column" option) | Yes | The ID of the curator that was present in the transaction |
| `Curator Member Name` (Selectable via "Show IDs as separate column" option) | No | The name of the curator that was present in the transaction |
| `Is Curated` | Yes | True if the transaction occurred via a curator |
| `Demand Channel`  | No | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Demand Channel ID` (Selectable via "Show IDs as separate column" option) | Yes | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Demand Channel Name` (Selectable via "Show IDs as separate column" option) | No | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Imp Type` | No | The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) |
| `Imp Type Id` | Yes | The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) |
| `Call Type`| Yes | The Impbus handler the impression originated from |
| `Sdk Version`| No | The version of the Xandr SDK (AST or Mobile SDK) used to generate the ad request. |
| `Mobile Application`|  No | The application the bundle on the ad request was mapped to |
| `Mobile Application ID` (Selectable via "Show IDs as separate column" option) | No | The ID for the application the bundle on the ad request was mapped to |
| `Mobile Application Name` (Selectable via "Show IDs as separate column" option) | No | The name for the application the bundle on the ad request was mapped to |
| `Site Domain`| No | The domain detected for the ad request |
| `Country Code` | Yes | The country/region 2 digit code in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. Country/region information is detected by the IP address of the user. Note: Some discrepancies are normal with external data sources due to differences between country/region detection methods. |
| `Geo Country Name`| No | The country/region name in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. Country/region information is detected by|
| `Day`  |  No  | The day of the Auction |
| `Hour` | No  | The hour of the auction. Note: For impressions older than 100 days, the day will be returned rather than the hour.|
| `Month`  | No | The month of the auction|
| `Filtered Request Reason` |  No | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are: "Invalid Domain" (1), "Invalid IP" (2), "Suspected Domain Detection Tampering" (3, 4, 5), "Unknown" (6, 7), “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks, “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify, "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. |
| `Filtered Request Reason ID`|  No | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. <br> **Possible reasons are:** <br> - "Invalid Domain" (1) <br> - "Invalid IP" (2) <br> - "Suspected Domain Detection Tampering" (3, 4, 5) <br> - "Unknown" (6, 7) <br> - “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks <br> - “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify. <br> - "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. |


## Metrics

> [!NOTE]
> - When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.
> - Adjustment revenue is not currently reportable. Revenue metrics may have minor discrepancies due to varying aggregation levels. 

| **Column** | **Description** |
|---|--|
| `Imps` | The number of impressions recorded, of any imp_type. N.B. For some call_types such as /OpenRTB2 and /prebid blank impressions are not recorded as imps, as typically there is a further auction when Xandr returns bids, and it would not be known if the final impression blanked, or Xandr lost in the final auction. |
| `Old Network RPM` | The revenue per 1000 impressions that were not blanks, defaults or errors. |
| `Total Revenue eCPM` | The total revenue per 1000 impressions. |
| `Revenue` | The total net revenue. |
| `Imps (blank)` | The total number of impressions in which a blank creative served. |
| `Imps (default)` | The total number of impressions in which a default creative served because there were no valid bids. |
| `Imps (default error)` | The total number of impressions in which a default creative served due to a timeout issue. |
| `Imps (kept)` | The total number of impressions in which one of your managed advertisers served a creative. |
| `Imps (resold)` | The total number of impressions sold to a third-party buyer. |
| `Imps (primary creative)` | The number of page-level roadblocks that served the master creative. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `Imps (PSA)` | The total number of impressions in which a public service announcement served because no other creative was eligible. |
| `Imps (PSA error)` | The total number of impressions in which a public service announcement served due to timeout issue. |
| `Seller Revenue` | The net revenue resultant from a 3rd party buyer (to the seller)  |
| `Booked Revenue` | The net revenue applied on the Line Item that won the impression. |
| `Clicks` | The number of clicks recorded. Clicks are deduplicated by auction (so maximum 1 click per unique auction) and have a 6 hour TTL to be recorded. Clicks can be measured for display impresisons bought by Xandr Invest and for Video and Native creatives from all buyers. |
| `Total Revenue eCPC` | The total revenue per click. |
| `Cost` | The cost to purchase 3rd party inventory via a Line Item |
| `CPM` | The cost per 1000 impressions. |
| `Starts` | The number of start events received by Xandr, maximum 1 per auction. |
| `25 pcts` | The number of first quartile events received by Xandr, maximum 1 per auction. |
| `50 pcts` | The number of second quartile events received by Xandr, maximum 1 per auction. |
| `75 pcts` | The number of third quartile events received by Xandr, maximum 1 per auction. |
| `Completions` | The number of completion events received by Xandr, maximum 1 per auction. |
| `Errors` | The number of error events received by Xandr, maximum 1 per auction. |
| `Skips` | The number of skip events received by Xandr, maximum 1 per auction. |
| `Start Rate` | video_starts / imps |
| `25% Completion Rate` | video_25_pcts / video_starts |
| `50% Completion Rate` | video_50_pcts / video_starts |
| `75% Completion Rate` | video_75_pcts / video_starts |
| `Video Skip Rate` | video_skips / video_starts |
| `Started Video Completion Rate` | Video completions per load  (video_completions / video_starts) |
| `Revenue Per Video Complete` | The revenue per video completion. |
| `View Measured Imps` | The total number of impressions that were measured for viewability |
| `Imps Viewed` | The total number of impressions that were measured as viewable by the Xandr viewability script |
| `View Measurement Rate` | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `View Rate` | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `Total Revenue vCPM` | The total revenue per 1000 viewable impressions. |
| `Ad Requests` | The number of unique auctions Xandr considered for auction, before any filtration was applied. N.B. One ad call may contain multiple tags. In such a scenario we would count an ad request for every tag within the ad request message. |
| `Filtered Requests` | The number of unique auctions that Xandr filtered due to inventory quality checks |
| `External Click` | Clicks as recorded by the external clicktracker. |
| `External Impression` | Imps as recorded by the external impression tracker. |
| `total_revenue_ecpa` | The total revenue per acquisition. |
| `ad_requests` | Total count of unique impressions sent to Microsoft Monetize |
| `ad_requests_auctioned` | Total count of unique impressions evaluated for auction |
| `filtered_requests` | Total count of auctioned requests filtered pre-bid for inventory quality |
| `ad_requests_no_creative` | Total count of requests with no eligible managed, programmatic, or default demand |
| `ad_responses_total` | Total count of auctions with at least one eligible bid |
| `ad_responses` | Total count of auctions with at least one eligible video bid |
| `bid_sent_no_responses` | Bid responses returned but where the creative ultimately did not render |
| `defaults_no_responses` | Requests where a default creative was sent but no response was received |
| `video_default_errors` | Errors reported when a default video creative should have served |
| `video_player_errors` | Errors reported after VAST XML delivery (maximum 1 per auction) |
| `response_rate` | Total ad responses ÷ (Ad Requests − Filtered Requests) |
| `win_rate` | (Kept + Resold impressions) ÷ Total Ad Responses |
| `fill_rate` | (Kept + Resold impressions) ÷ Ad Requests Auctioned |
| `ad_request_rpm` | Seller revenue per 1,000 auctioned ad requests |

## Metric filters

Metric filters let you return data that’s greater than or less than a specified threshold. You can apply multiple threshold filters, and you can combine them with standard filters to get more precise results. This is especially useful for scenarios such as:

| Task                                                        | Dimension | Filter                   |
|-------------------------------------------------------------|-----------|---------------------------|
| Report on line items with a CTR above 0.25%                 | Line Item | CTR > 0.0025             |
| Report on placements with viewability less than 40%         | Placement | Viewability <= 0.40       |
| Report on buyers with more than $1000 in revenue            | Buyer     | Revenue > 1000           |
| Report on buyers with CPM < $1.00 and viewability > 40%     | Buyer     | CPM <= 1.00<br>Viewability > 0.40 |

> [!NOTE]
> - For percentage metrics, enter the value as a decimal. For example, enter 0.0025 for 0.25%.
> - Filter logic always uses **AND**. You can’t apply threshold filters with **OR** logic.

### Metrics supported

| Metrics Category | Metric in API | Metric in UI |
|----------|------------|-------------|
| Core Performance | imps | Impressions |
| Core Performance | revenue | Revenue |
| Core Performance | clicks | Clicks |
| Core Performance | ctr | Click Through Rate |
| Core Performance | view_rate | View Rate |
| Revenue & Cost | sold_network_rpm | Sold Imps eCPM |
| Revenue & Cost | total_revenue_ecpm | Total Imps eCPM |
| Revenue & Cost | total_revenue_ecpc | eCPC (Total Revenue per Click) |
| Revenue & Cost | total_revenue_ecpa | eCPA (Total Revenue per Acquisition) |
| Revenue & Cost | total_revenue_vcpm | Viewable eCPM |
| Revenue & Cost | media_cost | Media Cost |
| Revenue & Cost | total_cost | Total Cost |
| Revenue & Cost | total_cost_ecpm | Total Cost eCPM |
| Revenue & Cost | total_cost_ecpc | Total Cost eCPC |
| Revenue & Cost | total_cost_ecpa | Total Cost eCPA |
| Revenue & Cost | cpm | Media CPM |
| Revenue & Cost | seller_revenue | Programmatic Revenue |
| Revenue & Cost | booked_revenue | Managed Revenue |
| Video Analytics | starts | Starts |
| Video Analytics | skips | Skips |
| Video Analytics | completions | Completions |
| Video Analytics | 25_pcts | 25% Video Complete |
| Video Analytics | 50_pcts | 50% Video Complete |
| Video Analytics | 75_pcts | 75% Video Complete |
| Video Analytics | errors | Errors |
| Video Analytics | start_rate | Start Rate |
| Video Analytics | video_skip_rate | Skip Rate |
| Video Analytics | started_video_completion_rate | Started Video Completion Rate |
| Video Analytics | video_25_pct_completion_rate | 25% Completion Rate |
| Video Analytics | video_50_pct_completion_rate | 50% Completion Rate |
| Video Analytics | video_75_pct_completion_rate | 75% Completion Rate |
| Video Analytics | revenue_per_video_complete | Revenue Per Video Complete |
| Viewability | imps_viewed | Imps Viewed |
| Viewability | view_measured_imps | View Measured Imps |
| Viewability | view_measurement_rate | View Measurement Rate |
| Conversion | post_click_ip_conv | Post Click Conversions: IP |
| Conversion | post_view_ip_conv | Post View Conversions: IP |
| Conversion | post_click_crossdevice_conv | Post Click Conversions: Cross Device |
| Conversion | post_view_crossdevice_conv | Post View Conversions: Cross Device |
| Conversion | post_view_convs | Post View Conversions |
| Conversion | post_click_convs | Post Click Conversions |
| Conversion | total_convs | Total Conversions |
| Conversion | convs_rate | Conversions Rate |
| Conversion | convs_per_mm | Conversions Per MM |
| Conversion | post_view_convs_rate | Post View Conversion Rate |
| Conversion | post_click_convs_rate | Post Click Conversion Rate |
| Conversion | external_click | External Click |
| Conversion | external_impression | External Impression |
| Impression Type | imps_blank | Imps (blank) |
| Impression Type | imps_default | Imps (default) |
| Impression Type | imps_default_error | Imps (default error) |
| Impression Type | imps_kept | Imps (managed) |
| Impression Type | imps_primary_creative | Imps (primary creative) |
| Impression Type | imps_psa | Imps (PSA) |
| Impression Type | imps_psa_error | Imps (PSA error) |
| Impression Type | imps_resold | Imps (programmatic) |
| Supply & Demand | ad_requests | Ad Requests |
| Supply & Demand | bid_sent_no_responses | Bid Sent No Responses |
| Supply & Demand | ad_responses | Ad Responses |
| Supply & Demand | filtered_requests | Filtered Requests |

All threshold filters support two operators:

- > :  greater than
- <= : less than or equal to

### API JSON example 

**Syntax**
```
{
  "report": {
    "group_filters": [
      {
        "view_rate": {
          "operator": "<=",
          "value": 0.4
        }
      }
    ]
  }
}
```
**Example**
```
{
  "report": {
    "report_type": "monetize_creative_brand_analytics",
    "name": "Placement Viewability under 40%",
    "timezone": "EST5EDT",
    "columns": [
      "placement",
      "view_rate"
    ],
    "emails": null,
    "orders": [
      {
        "order_by": "placement",
        "direction": "DESC"
      }
    ],
    "format": "csv",
    "report_interval": "today",
    "filters": [
      {
        "seller_member_id": "958"
      }
    ],
    "time_granularity": "cumulative",
    "ui_columns": [
      "placement",
      "view_rate"
    ],
    "group_filters": [
      {
        "view_rate": {
          "operator": "<=",
          "value": 0.4
        }
      }
    ]
  }
}
```

## Revenue types

Revenue types supported by Historical report include:

| Name                   | Description                                                             |
|----------------------- |------------------------------------------------------------------------ |
| **No Payment**         |                                                                         |
| **Flat CPM**           | A flat payment per 1000 impressions.                                    |
| **Cost plus CPM**      | Cost (what you spend on inventory) plus an extra CPM.                   |
| **Cost plus margin**   | Cost (what you spend on inventory) plus a percentage of what you spend. |
| **CPC**                | A flat payment per click.                                               |
| **CPA**                | A flat payment per conversion.                                          |
| **Revshare**           | A payment on a revshare basis (CPC or CPA).                             |
| **Estimated CPM**      | The estimated payment per 1000 impressions.                             |
| **CPVM**               | A flat payment per 1000 viewable impressions.                           |

### Impression types

The following impression types are reported:

| Name                 | Definition                                                                                      |
|----------------------|-------------------------------------------------------------------------------------------------|
| Blank                | No creative served.                                                                             |
| PSA                  | A public service announcement served because no other creative was eligible.                    |
| Default Error        | A default creative served due to a timeout issue.                                               |
| Default              | A default creative served because no line item bid or no other creative was eligible.           |
| Kept                 | One of your managed advertisers served a creative.                                              |
| Resold               | The impression was sold to a third-party buyer.                                                 |
| RTB                  | Your creative served on third-party inventory.                                                  |
| PSA Error            | A public service announcement served due to a timeout issue.                                    |
| External Impression  | An impression from an impression tracker.                                                       |
| External Click       | A click from a click tracker.                                                                   |
| Insertion            | Your creative served on third-party inventory where it persists across page-loads and sessions. |

### Run your reports

Follow these steps to generate your report:

1. Select **Reports** from the main menu.
1. Customize your `Filters`, `Dimensions`, `Metrics`, and `Advanced Options`.

   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](../monetize/dimensions-metrics-filtering-and-grouping.md).

1. Click **Run Report** to view your data.

   **Tip**: For larger datasets, consider using the API for quicker downloads.

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking Edit), a selection panel appears. Select items in the Available list (left), then click Add to include them in the Chosen list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer. 
    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.
    
1. Dimensions are grouped into major categories. Click the arrow next to a category to see all dimensions under it, or use the search bar to find the desired dimension.
1. **Select Your Metrics**: Metrics are grouped into major categories. Click the arrow next to a category to see all available metrics, or use the search bar to find the metric you need.
1. Select your time range and interval from the menu. Under **Advanced Options**, you can also choose your preferred **Currency** and **Time zone**.

   > [!TIP]
   > You can select either member or USD as the currency. This affects how monetary fields are displayed in your report. For example, if you select **Advertiser** and choose **Member** for currency, the report shows all monetary data in the member’s currency, including data related to child objects like line items.

1. Click **Run Report**.

   > [!WARNING]
   > The more dimensions you group by, the larger the dataset returned. This may impact processing time.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    1. **Run in background & email results:** Run the report in the background and email the results to one or more email addresses.
    1. **Run in background & download results:** Run the report in the background and a popup notification will let you know when the report is ready to view or download.
> [!TIP]
> The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the API for that reporting service (The limit here is 10 million rows).


## Related topics

- [Microsoft Monetize - Impression counting](impression-counting.md)
- [Mobile SDK - Impression counting methods](../mobile-sdk/impression-counting-methods.md)
- [Microsoft Monetize - Introduction to viewability](introduction-to-viewability.md)
- [Microsoft Monetize - Availability of reporting data](availability-of-reporting-data.md)
- [Microsoft Monetize - Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)
- [Microsoft Monetize - Report throttling](report-throttling.md)
