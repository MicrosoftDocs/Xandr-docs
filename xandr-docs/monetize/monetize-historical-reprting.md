---
title: Monetize Historical Reporting
description: Learn how Monetize Historical Reporting consolidates legacy reports, offering enhanced analytics, streamlined navigation, and improved performance insights.
ms.date: 10/18/2024
ms.author: shsrinivasan
---

# Monetize historical reporting

## Overview

### Project status

The new reporting UI and the Historical Report are currently in Alpha, enabled for select clients. Please contact your account manager if you require further information.

The Historical report already covers most of the data that is available in the legacy reporting. During the Alpha phase for this report, we will be adding additional dimensions and metrics to close out key outstanding feature gaps compared to the legacy reports. Data is available from **10th October 2024** in the Historical report generally, and earlier in 2024 for clients involved in the Alpha.

Currently, the new reporting UI only provides access to the Historical report for Network users. Access to all existing report types will be added during the Alpha, along with support for Publisher and Advertiser users.

### New report types and User interface for Monetize

The new **Historical report** in the new Microsoft Monetize reporting UI offers comprehensive data across a wide range of dimensions and metrics. This report will replace several legacy Network and Advertiser/Publisher reports, enhancing and simplifying reporting capabilities.

The Historical report is built from two datasets that are accessible from one UI, with dimension and metric incompatibilities shown to the user as they make selections. In the API, the datasets are available independently as two report types.

This update’s expanded range enables a more granular understanding of data across multiple aspects of delivery and inventory, with new reportable combinations of dimensions that were not possible before, such as placement and device.

The new UI is a significant upgrade, reducing the number of report types a user needs to interact with. It provides features to improve usability, such as:

- Categorization of Dimensions and Metrics.
- Comprehensive search capability.

## New features

### Report enhancements

- **Bringing together the new Delivery and Inventory analytics reports into one **Historical report builder** experience**:
      - Consolidate reporting for better performance insights.
      - Broader coverage of metrics and dimensions.

| Legacy UI Name      | New UI Report Name | API Name                          |
|---------------------|-------------------|-----------------------------------|
| Delivery Analytics  | Historical Report | `monetize_creative_brand_analytics` |
| Inventory Analytics | Historical Report | `monetize_supply_analytics`         |

> [!NOTE]
> Coverage of dimensions and metrics is under development. Additional fields are planned to enable the deprecation of legacy report types.

## New user interface

### Improved navigation

Access reports with fewer clicks, enhancing usability.

## Deprecation of legacy reports

Legacy reports are planned to not be populated with new Monetize data from mid 2025. Historic data will be available up to the individual report's standard retention and or 730 days, whichever is lower. This includes reports like *Network Analytics* and *Advertiser Video Analytics*. Users are encouraged to transition to the new reports as soon as possible for reports accessing data after 10th October 2024.

> [!NOTE]
> Communication will be sent in advance to support the transition.

### Scope of data

These new report types automatically include data for all impression types except for 7=RTB (a buying transaction on supply from another seat to your own) for Monetize Sellers. Reporting for Invest and External SSPs is not included in these datasets.

## Network legacy report types

The new reports consolidate Delivery and Inventory analytics, simplifying access to data. The table below maps new reports to their legacy counterparts and API names:

| **UI Report Name**                  | **API Name**                          |
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
| Video Analytics                     | video_analytics_network               |
| Video Error Analytics               | video_error_analytics_network         |
| Audio Analytics                     | audio_analytics_network               |

## Advertiser / Publisher Legacy Report types

| **UI Report Name**                | **API Name**                        |
|-----------------------------------|-------------------------------------|
| Advertiser Analytics              | advertiser_analytics                |
| Site Domain Performance           | site_domain_performance             |
| Advertiser Video Analytics        | video_analytics_network_advertiser  |
| Publisher Analytics               | network_publisher_analytics         |
| Not Available                     | publisher_brand_review              |
| Seller Fill and Delivery Publisher| seller_fill_and_delivery_publisher  |
| Publisher Video Analytics Report  | video_analytics_network_publisher   |
| Publisher Video Error Report      | video_error_analytics_network       |

## New UI report creation

The new user interface enables streamlined report creation. Users can select from various **dimensions**, **metrics**, and **filters** to customize their reports.

:::image type="content" source="media/create-new-report.png" alt-text="The screenshot shows how to create new reports.":::

## Time ranges and retention

### Time ranges

The following time ranges are available for extracting report data:

- **Custom**
- **Current Hour** (`current_hour`)
- **Last Hour** (`last_hour`)
- **Today** (`today`)
- **Yesterday** (`yesterday`)
- **Last 48 Hours** (`last_48_hours`)
- **Last 2 Days** (`last_2_days`)
- **Last 7 Days** (`last_7_days`)
- **Last 14 Days** (`last_14_days`)
- **Last 30 Days** (`last_30_days`)
- **Month to Date** (`month_to_date`)
- **Month to Yesterday** (`month_to_yesterday`)

:::image type="content" source="media/time-ranges.png" alt-text="The screenshot shows time ranges that define the period from which data is extracted for reports.":::

- ### Retention Policy

- **Hourly Data:** Retained for the last 100 days.
- **Cumulative Data:** Retained for up to 2 years and 2 months.

## Intervals

Intervals determine how data is grouped in the report:

- **Hourly:** Grouped by the hour.
- **Daily:** Grouped by the day.
- **Monthly:** Grouped by the month.
- **Cumulative:** Data covers the entire selected period.

:::image type="content" source="media/intervals-cumulative.png" alt-text="The screenshot illustrates Intervals, which define how data is grouped in the report, such as hourly, daily, monthly, or cumulative.":::

## Data availability

- **Maximum retention:** 2 years and 2 months.
- **Current maximum data availability:** 90 days (planned extensions forthcoming).

## Filters

Filters allow you to limit displayed data by specific dimensions. Available filters include:

- **Advertiser name**
- **Publisher name**
- **Impression type**

:::image type="content" source="media/data-availability-filters.png" alt-text="The screenshot shows filter options to include or exclude data for specific dimensions.":::

## Dimensions and Metrics

Users can filter and group data using various **dimensions** and **metrics**.

> [!WARNING]
> Some dimensions, such as **Device Make** and **Creative**, cannot be used together. An info message will indicate unavailable combinations.

### Metrics

> [!NOTE]
> Adjustment revenue is not currently reportable. Revenue metrics may have minor discrepancies due to varying aggregation levels.

| **api_field_name** | **Type** | **Grouping** | **Description** |
|---|---|---|---|
| imps | int | Core Metrics | The number of impressions recorded, of any imp_type. N.B. For some call_types such as /OpenRTB2 and /prebid blank impressions are not recorded as imps, as typically there is a further auction when Xandr returns bids, and it would not be known if the final impression blanked, or Xandr lost in the final auction. |
| sold_network_rpm | double | Core Metrics | The revenue per 1000 impressions that were not blanks, defaults or errors. |
| total_revenue_ecpm | money | Core Metrics | The total revenue per 1000 impressions. |
| revenue | money | Core Metrics | The total net revenue. |
| imps_blank | int | Impression Type Metrics | The total number of impressions in which a blank creative served. |
| imps_default | int | Impression Type Metrics | The total number of impressions in which a default creative served because there were no valid bids. |
| imps_default_error | int | Impression Type Metrics | The total number of impressions in which a default creative served due to a timeout issue. |
| imps_kept | int | Impression Type Metrics | The total number of impressions in which one of your managed advertisers served a creative. |
| imps_resold | int | Impression Type Metrics | The total number of impressions sold to a third-party buyer. |
| imps_primary_creative | int | Impression Type Metrics | The number of page-level roadblocks that served the master creative. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| imps_psa | int | Impression Type Metrics | The total number of impressions in which a public service announcement served because no other creative was eligible. |
| imps_psa_error | int | Impression Type Metrics | The total number of impressions in which a public service announcement served due to timeout issue. |
| seller_revenue | money | Impression Type Metrics | The net revenue resultant from a 3rd party buyer (to the seller)  |
| booked_revenue | money | Impression Type Metrics | The net revenue applied on the Line Item that won the impression. |
| clicks | int | Clicks | The number of clicks recorded. Clicks are deduplicated by auction (so maximum 1 click per unique auction) and have a 6 hour TTL to be recorded. Clicks can be measured for display impresisons bought by Xandr Invest and for Video and Native creatives from all buyers. |
| total_revenue_ecpc | money | Clicks | The total revenue per click. |
| cost | money | Media Buying | The cost to purchase 3rd party inventory via a Line Item |
| cpm | money | Media Buying | The cost per 1000 impressions. |
| starts | int | Video | The number of start events received by Xandr, maximum 1 per auction. |
| 25_pcts | int | Video | The number of first quartile events received by Xandr, maximum 1 per auction. |
| 50_pcts | int | Video | The number of second quartile events received by Xandr, maximum 1 per auction. |
| 75_pcts | int | Video | The number of third quartile events received by Xandr, maximum 1 per auction. |
| completions | int | Video | The number of completion events received by Xandr, maximum 1 per auction. |
| errors | int | Video | The number of error events received by Xandr, maximum 1 per auction. |
| skips | int | Video | The number of skip events received by Xandr, maximum 1 per auction. |
| start_rate | double | Video | video_starts / imps |
| video_25_pct_completion_rate | double | Video | video_25_pcts / video_starts |
| video_50_pct_completion_rate | double | Video | video_50_pcts / video_starts |
| video_75_pct_completion_rate | double | Video | video_75_pcts / video_starts |
| video_skip_rate | double | Video | video_skips / video_starts |
| started_video_completion_rate | double | Video | Video completions per load  (video_completions / video_starts) |
| revenue_per_video_complete | double | Video | The revenue per video completion. |
| view_measured_imps | int | Viewability Metrics | The total number of impressions that were measured for viewability |
| imps_viewed | int | Viewability Metrics | The total number of impressions that were measured as viewable by the Xandr viewability script |
| view_measurement_rate | double | Viewability Metrics | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| view_rate | double | Viewability Metrics | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| total_revenue_vcpm | money | Viewability Metrics | The total revenue per 1000 viewable impressions. |
| ad_requests | int | Request / Response | The number of unique auctions Xandr considered for auction, before any filtration was applied. N.B. One ad call may contain multiple tags. In such a scenario we would count an ad request for every tag within the ad request message. |
| filtered_requests | int | Request / Response | The number of unique auctions that Xandr filtered due to inventory quality checks |
| external_click | int | External Trackers | Clicks as recorded by the external clicktracker. |
| external_impression | int | External Trackers | Imps as recorded by the external impression tracker. |
| total_revenue_ecpa | money | Conversions | The total revenue per acquisition. |

### Dimensions

| UI column| API column| Report Type| Type| Filter?| Grouping| Description|
|---	|---	|---	|---	|---	|---	|---	|
| Advertiser 	| advertiser 	| both 	| string 	| False 	| Buyside 	| The advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Advertiser ID (Selectable via "Show IDs as separate column" option) 	| advertiser_id 	| both 	| int 	| True 	| Buyside 	| The ID of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Advertiser Name (Selectable via "Show IDs as separate column" option) 	| advertiser_name 	| both 	| string 	| False 	| Buyside 	| The name of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Bidder 	| bidder 	| both 	| int 	| False 	| Buyside 	| The Bidder object (in most cases this is a DSP). 	|
| Bidder ID (Selectable via "Show IDs as separate column" option) 	| bidder_id 	| both 	| int 	| True 	| Buyside 	| The ID of the Xandr Bidder object (in most cases this is a DSP). 	|
| Bidder Name (Selectable via "Show IDs as separate column" option) 	| bidder_name 	| both 	| int 	| False 	| Buyside 	| The name of the Xandr Bidder object (in most cases this is a DSP). 	|
| Billing Period 	| billing_period_id 	| both 	| int 	| True 	| Buyside 	| The ID of the Billing Period 	|
| Billing Period.Booked Imps Budget Daily 	| billing_period.booked_imps_budget_daily 	| both 	| int 	| False 	| Buyside 	| The daily impression budget of the insertion order's billing period. 	|
| Billing Period.Booked Imps Budget Lifetime 	| billing_period.booked_imps_budget_lifetime 	| both 	| int 	| False 	| Buyside 	| The lifetime impression budget of the insertion order's billing period. 	|
| Billing Period.Start Date 	| billing_period.start_date 	| both 	| datetime 	| False 	| Buyside 	| The earliest date of the insertion order's billing period. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. 	|
| Billing Period.End Date 	| billing_period.end_date 	| both 	| datetime 	| False 	| Buyside 	| The last date of the insertion order's billing period. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. 	|
| Billing Period.External Code 	| billing_period.external_code 	| both 	| int 	| False 	| Buyside 	| The custom code for the billing period. 	|
| Buyer Member 	| buyer_member 	| both 	| string 	| False 	| Buyside 	| The name with ID in brackets of the Xandr buyer member that purchased the impression 	|
| Buyer Member ID (Selectable via "Show IDs as separate column" option) 	| buyer_member_id 	| both 	| int 	| True 	| Buyside 	| The ID of the Xandr buyer member that purchased the impression 	|
| Buyer Member Name (Selectable via "Show IDs as separate column" option) 	| buyer_member_name 	| both 	| string 	| False 	| Buyside 	| The Name of the Xandr buyer member that purchased the impression 	|
| Buyer Seat 	| buyer_seat 	| both 	| string 	| False 	| Buyside 	| The seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts. 	|
| Buyer Seat ID (Selectable via "Show IDs as separate column" option) 	| buyer_seat_id 	| both 	| int 	| True 	| Buyside 	| The ID of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts. 	|
| Buyer Seat Name (Selectable via "Show IDs as separate column" option) 	| buyer_seat_name 	| both 	| string 	| False 	| Buyside 	| The name of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts. 	|
| Buyer Seat Code 	| buyer_seat_code 	| both 	| string 	| False 	| Buyside 	| The custom buyer seat ID (submitted by DSP) which was used to bid on the impression 	|
| Flight Id 	| flight_id 	| both 	| int 	| False 	| Buyside 	| The ID of the line item flight under which the impression was purchased. 	|
| Flight.Booked Impressions Budget Daily 	| flight.booked_impressions_budget_daily 	| both 	| int 	| False 	| Buyside 	| The daily impression budget for the line item's flight. 	|
| Flight.Booked Impressions Budget Lifetime 	| flight.booked_impressions_budget_lifetime 	| both 	| int 	| False 	| Buyside 	| The lifetime impression budget for the line item's flight. 	|
| Flight.Start Date 	| flight.start_date 	| both 	| datetime 	| False 	| Buyside 	| The start date of the line item's flight. 	|
| Flight.End Date 	| flight.end_date 	| both 	| datetime 	| False 	| Buyside 	| The end date of the line item's flight. 	|
| Insertion Order 	| insertion_order 	| both 	| string 	| True 	| Buyside 	| The insertion order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Insertion Order ID (Selectable via "Show IDs as separate column" option) 	| insertion_order_id 	| both 	| int 	| False 	| Buyside 	| The insertion order ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Insertion Order Name (Selectable via "Show IDs as separate column" option) 	| insertion_order_name 	| both 	| string 	| False 	| Buyside 	| The insertion order name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Insertion Order.Billing Code 	| insertion_order.billing_code 	| both 	| string 	| False 	| Buyside 	| The billing code associated with the insertion order (if there is one). 	|
| Insertion Order.End Date 	| insertion_order.end_date 	| both 	| datetime 	| False 	| Buyside 	| The end date of the insertion order (for legacy insertion orders). 	|
| Insertion Order.Start Date 	| insertion_order.start_date 	| both 	| datetime 	| False 	| Buyside 	| The start date of the insertion order (for legacy insertion orders). 	|
| Insertion Order.State 	| insertion_order.state 	| both 	| string 	| False 	| Buyside 	| The state of the insertion order (e.g., active, inactive). 	|
| Insertion Order.Type 	| insertion_order.type 	| both 	| int 	| True 	| Buyside 	| The type of insertion order associated with the impression (e.g. Legacy, Seamless). 	|
| Line Item 	| line_item 	| both 	| string 	| False 	| Buyside 	| The line item order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Line Item Id (Selectable via "Show IDs as separate column" option) 	| line_item_id 	| both 	| int 	| True 	| Buyside 	| The line item ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Line Item Name (Selectable via "Show IDs as separate column" option) 	| line_item_name 	| both 	| string 	| False 	| Buyside 	| The line item name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| Line Item.Comments 	| line_item.comments 	| both 	| string 	| False 	| Buyside 	| Any comments that have been entered for this line item. 	|
| Line Item.Start Date 	| line_item.start_date 	| both 	| datetime 	| False 	| Buyside 	| The start date of the line item. 	|
| Line Item.End Date 	| line_item.end_date 	| both 	| datetime 	| False 	| Buyside 	| The end date of the line item. 	|
| Line Item.Status 	| line_item.status 	| both 	| string 	| False 	| Buyside 	| The state of the line item (e.g., active, inactive). 	|
| Line Item.Code 	| line_item_code 	| both 	| string 	| False 	| Buyside 	| The optional external code applied to the line item. 	|
| Li Priority 	| li_priority 	| both 	| string 	| True 	| Buyside 	| The bidding priority for a line item that targets direct inventory. For more information, see Bidding Priority in the UI Documentation. Possible values: 1 - 20, where 20 is the highest priority. 	|
| Li Subtype 	| li_subtype 	| both 	| string 	| True 	| Buyside 	| The line item subtype (e.g., Augmented, Deal, Guaranteed). 	|
| Li Subtype ID (Selectable via "Show IDs as separate column" option) 	| li_subtype_id 	| both 	| int 	| False 	| Buyside 	| The line item subtype ID. 	|
| Li Subtype Name (Selectable via "Show IDs as separate column" option) 	| li_subtype_name 	| both 	| string 	| False 	| Buyside 	| The line item subtype name. 	|
| Salesrep For Line Item 	| salesrep_for_line_item 	| both 	| string 	| True 	| Reporting Labels 	| A custom reporting label field containing the sales representative. You may only select one reporting label per report. 	|
| Trafficker For Line Item 	| trafficker_for_line_item 	| both 	| string 	| True 	| Reporting Labels 	| A custom reporting label field containing the trafficker. You may only select one reporting label per report. 	|
| Type For Line Item 	| type_for_line_item 	| both 	| string 	| True 	| Reporting Labels 	| A custom reporting label field used to list the line item type (e.g., Retargeting LI). This is not the same as the Type attribute described above. You may only select one reporting label per report. 	|
| Insertion Order Type Label 	| insertion_order_type 	| both 	| string 	| True 	| Reporting Labels 	| A custom reporting label field used to list the insertion order type (e.g., Branding IO). This is not the same as the Type attribute described above. You may only select one reporting label per report. 	|
| Insertion Order.Sales Rep Label 	| insertion_order.sales_rep_label 	| both 	| string 	| True 	| Reporting Labels 	| A customer reporting label field used to list the sales representative associated with the insertion order. You may only select one reporting label per report. 	|
| Insertion Order.Trafficker Label 	| insertion_order.trafficker_label 	| both 	| string 	| True 	| Reporting Labels 	| A customer reporting label field used to list the trafficker associated with the insertion order. You may only select one reporting label per report. 	|
| Placement 	| placement 	| both 	| string 	| False 	| Sellside 	| The Xandr Placement for the impression. 	|
| Placement ID (Selectable via "Show IDs as separate column" option) 	| placement_id 	| both 	| int 	| True 	| Sellside 	| The ID of the Xandr Placement for the impression. 	|
| Placement Name (Selectable via "Show IDs as separate column" option) 	| placement_name 	| both 	| string 	| False 	| Sellside 	| The name of the Xandr Placement for the impression. 	|
| Placement.Code 	| placement.code 	| both 	| string 	| False 	| Sellside 	| The code of the Xandr Placement for the impression. 	|
| Placement.Code2 	| placement.code2 	| both 	| string 	| False 	| Sellside 	| The code of the Xandr Placement for the impression. 	|
| Placement.Code3 	| placement.code3 	| both 	| string 	| False 	| Sellside 	| The code of the Xandr Placement for the impression. 	|
| Placement Group 	| plmt_grp 	| both 	| string 	| False 	| Sellside 	| Xandr Placement Group for the impression. 	|
| Placement Group ID (Selectable via "Show IDs as separate column" option) 	| plmt_grp_id 	| both 	| int 	| True 	| Sellside 	| The ID of the Xandr Placement Group for the impression. 	|
| Placement Group Name (Selectable via "Show IDs as separate column" option) 	| plmt_grp.name 	| both 	| string 	| False 	| Sellside 	| The name of the Xandr Placement Group for the impression. 	|
| Placement Group.Code 	| plmt_grp.code 	| both 	| string 	| False 	| Sellside 	| The code of the Xandr Placement Group for the impression. 	|
| Publisher 	| publisher 	| both 	| string 	| False 	| Sellside 	| The Xandr Publisher for the impression. 	|
| Publisher ID (Selectable via "Show IDs as separate column" option) 	| publisher_id 	| both 	| int 	| True 	| Sellside 	| The ID of the Xandr Publisher for the impression. 	|
| Publisher Name (Selectable via "Show IDs as separate column" option) 	| publisher_name 	| both 	| string 	| False 	| Sellside 	| The name of the Xandr Publisher for the impression. 	|
| Seller Member 	| seller_member 	| both 	| string 	| False 	| Sellside 	| The name and ID of the seller member. 	|
| Seller Member Id (Selectable via "Show IDs as separate column" option) 	| seller_member_id 	| both 	| int 	| False 	| Sellside 	| Seller's member id 	|
| Brand 	| brand 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| The Brand as determined by the Xandr creative audit or self assigned for managed traffic 	|
| Brand ID (Selectable via "Show IDs as separate column" option) 	| brand_id 	| monetize_creative_brand_analytics 	| int 	| True 	| Creative 	| The ID for the Brand as determined by the Xandr creative audit or self assigned for managed traffic 	|
| Brand Name (Selectable via "Show IDs as separate column" option) 	| brand_name 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| The name for the Brand as determined by the Xandr creative audit or self assigned for managed traffic 	|
| Brand Category ID 	| brand_category_id 	| monetize_creative_brand_analytics 	| int 	| True 	| Creative 	| The parent category ID for the creative's assigned brand 	|
| Brand Category Name 	| brand_category_name 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| The parent category name for the creative's assigned brand 	|
| Creative 	| creative 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| Creative that served. It will only be populated for managed impressions. 	|
| Creative ID (Selectable via "Show IDs as separate column" option) 	| creative_id 	| monetize_creative_brand_analytics 	| int 	| True 	| Creative 	| The Xandr ID for the creative that served. 	|
| Creative Name (Selectable via "Show IDs as separate column" option) 	| creative_name 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| The Xandr name for the creative that served. The name will only be populated for managed impressions. 	|
| Creative Code 	| creative_code 	| monetize_creative_brand_analytics 	| string 	| False 	| Creative 	| The code of the creative. 	|
| Creative Media Type 	| creative_type 	| both 	| string 	| False 	| Creative 	| The media type of the creative that transacted 	|
| Creative Media Type ID (Selectable via "Show IDs as separate column" option) 	| creative_type_id 	| both 	| int 	| False 	| Creative 	| The media type ID of the creative that transacted 	|
| Size 	| size 	| both 	| string 	| True 	| Creative 	| For display creatives, this is the creative width x height in pixels 	|
| Domains Exposed Id 	| domains_exposed_id 	| monetize_supply_analytics 	| int 	| False 	| Visibility 	| Whether this inventory's domains are exposed for targeting by buyers. Allowed values: "Exposed", "Not exposed" 	|
| Domains Exposed 	| domains_exposed 	| monetize_supply_analytics 	| int 	| False 	| Visibility 	| Whether this inventory's domains are exposed for targeting by buyers. Allowed values: "Exposed", "Not exposed" 	|
| Exposed For Resale 	| exposed_for_resale 	| monetize_supply_analytics 	| string 	| False 	| Visibility 	| Viewability profile, used by sellers to expose/hide their content_categories info to buyers 	|
| Exposed For Resale Id 	| exposed_for_resale_id 	| monetize_supply_analytics 	| int 	| False 	| Visibility 	| Viewability profile, used by sellers to expose/hide their publisher info to buyers 	|
| Allowed Media Types 	| allowed_media_types_bitmap_name 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| An array of the permitted media types for the impression. 	|
| Audit Type 	| audit_type 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The type of audit performed on the domain where the impression occurred. Possible values: "By Seller": The domain was self-audited. "By AppNexus": The domain was audited by AppNexus. "By Seller & AppNexus": The domain was audited by both the seller and AppNexus. "Unknown Audit Type": This usually means that the domain is unaudited. In some cases, this means that the domain was not auditable for technical reasons. 	|
| Audit Type ID (Selectable via "Show IDs as separate column" option) 	| audit_type_id 	| monetize_supply_analytics 	| int 	| True 	| Inventory 	| The ID of the type of audit performed on the domain where the impression occurred. 	|
| Audit Type Name (Selectable via "Show IDs as separate column" option) 	| audit_type_name 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The name of the type of audit performed on the domain where the impression occurred. 	|
| Browser 	| browser 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The Name and ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service. 	|
| Browser ID (Selectable via "Show IDs as separate column" option) 	| browser_id 	| monetize_supply_analytics 	| int 	| True 	| Inventory 	| The ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service. 	|
| Content Category 	| content_category 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The ID and name of the universal content category associated with the audited domain. 	|
| Content Category ID (Selectable via "Show IDs as separate column" option) 	| content_category_id 	| monetize_supply_analytics 	| int 	| True 	| Inventory 	| The ID of the universal content category associated with the audited domain. 	|
| Content Category Name (Selectable via "Show IDs as separate column" option) 	| content_category_name 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The name of the universal content category associated with the audited domain. 	|
| Fold Position 	| fold_position 	| monetize_supply_analytics 	| string 	| False 	| Inventory 	| The fold position, i.e. where on the page the placement is located. For allowed values, see fold_position_id. 	|
| Fold Position Id 	| fold_position_id 	| monetize_supply_analytics 	| int 	| True 	| Inventory 	| The ID of the fold position, i.e. where on the page the placement is located. Possible values for impressions: 0 = "unknown", 1 = "above", 2 = "below". 	|
| Supply Type 	| supply_type_id 	| both 	| int 	| True 	| Inventory 	| The ID of the type of inventory. 	|
| Supply Type Name 	| supply_type_name 	| both 	| string 	| False 	| Inventory 	| The type of inventory. Possible values: "web", "mobile_web", "mobile_app", "facebook_sidebar". 	|
| Prebid Server Eligible 	| prebid_server_eligible 	| both 	| int 	| True 	| Prebid Server 	| True if PSP was eligible to bid into the auction for the impression. 	|
| Prebid Server Eligible 	| prebid_server_eligible_name 	| both 	| string 	| False 	| Prebid Server 	| True if PSP was eligible to bid into the auction for the impression. 	|
| SSP 	| ssp 	| both 	| string 	| False 	| Prebid Server 	| When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise the SSP will be recorded as Monetize. 	|
| SSP ID (Selectable via "Show IDs as separate column" option) 	| ssp_id 	| both 	| int 	| False 	| Prebid Server 	| When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise the SSP will be recorded as Monetize. 	|
| SSP Name (Selectable via "Show IDs as separate column" option) 	| ssp_name 	| both 	| string 	| False 	| Prebid Server 	| When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise the SSP will be recorded as Monetize. 	|
| Deal 	| deal 	| both 	| string 	| False 	| Deals 	| The name and ID of the affected deal. 	|
| Deal ID (Selectable via "Show IDs as separate column" option) 	| deal_id 	| both 	| int 	| True 	| Deals 	| The ID of the deal 	|
| Deal Name (Selectable via "Show IDs as separate column" option) 	| deal_name 	| both 	| string 	| False 	| Deals 	| The name of the affected deal. 	|
| Deal Type 	| deal_type 	| both 	| string 	| True 	| Deals 	| Possible values: Open Auction (1), Private Auction (2), First Look (3), Programmatic Guaranteed (4), Curated (5 - only relevant for Curators) 	|
| Revenue Type 	| revenue_type 	| both 	| string 	| False 	| Payment 	| For managed line items, this is the basis on which the booked revenue gets recorded for the Seller. +----+------------------+ \| id \| name \| +----+------------------+ \| 5 \| cost_plus_cpm \| \| 6 \| cost_plus_margin \| \| 4 \| cpa \| \| 3 \| cpc \| \| 2 \| cpm \| \| 10 \| cpvm \| \| 9 \| est_cpm \| \| 7 \| flat_fee \| \| 1 \| none \| \| 8 \| vcpm \| +----+------------------+ 	|
| Revenue Type (Selectable via "Show IDs as separate column" option) 	| revenue_type_id 	| both 	| int 	| True 	| Payment 	| The basis on which the advertiser has agreed to pay you for the impression. For more information, see Revenue Types. 	|
| Carrier 	| carrier 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The carrier for the device on which the impression was served. To retrieve a complete list of carrier IDs and names, use the Carrier Service. 	|
| Carrier ID (Selectable via "Show IDs as separate column" option) 	| carrier_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the carrier for the device on which the impression was served. To retrieve a complete list of carrier IDs and names, use the Carrier Service. 	|
| Carrier Name (Selectable via "Show IDs as separate column" option) 	| carrier_name 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the carrier for the device on which the impression was served. To retrieve a complete list of carrier IDs and names, use the Carrier Service. 	|
| Device Make 	| device_make 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The device manufacturer 	|
| Device Make ID (Selectable via "Show IDs as separate column" option) 	| device_make_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). 	|
| Device Make Name (Selectable via "Show IDs as separate column" option) 	| device_make_name 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). To retrieve a complete list of device make IDs and names, use the Device Make Service. 	|
| Device Model 	| device_model 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The ID and name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). 	|
| Device Model ID (Selectable via "Show IDs as separate column" option) 	| device_model_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). 	|
| Device Model Name (Selectable via "Show IDs as separate column" option) 	| device_model_name 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). 	|
| Device Type 	| device_type 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box 	|
| Device Type ID 	| device_type_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box 	|
| Operating System 	| operating_system 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the operating system of the device followed by the ID (Microsoft Advertising format). 	|
| Operating System ID (Selectable via "Show IDs as separate column" option) 	| operating_system_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the operating system of the device. 	|
| Operating System Name (Selectable via "Show IDs as separate column" option) 	| operating_system_name 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the operating system of the device. 	|
| Operating System Family 	| operating_system_family 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the operating system family (e.g., Android, Microsoft Windows) of the device followed by the ID (Microsoft Advertising format). 	|
| Operating System Family ID (Selectable via "Show IDs as separate column" option) 	| operating_system_family_id 	| monetize_supply_analytics 	| int 	| True 	| Device 	| The ID of the operating system family associated with the device the impression was served on. 	|
| Operating System Family Name (Selectable via "Show IDs as separate column" option) 	| operating_system_family_name 	| monetize_supply_analytics 	| string 	| False 	| Device 	| The name of the operating system family associated with the device the impression was served on. 	|
| Curator Member 	| curator_member 	| both 	| string 	| False 	| Curation 	| The ID of the curator that was present in the transaction 	|
| Curator Member ID (Selectable via "Show IDs as separate column" option) 	| curator_member_id 	| both 	| int 	| True 	| Curation 	| The ID of the curator that was present in the transaction 	|
| Curator Member Name (Selectable via "Show IDs as separate column" option) 	| curator_member_name 	| both 	| string 	| False 	| Curation 	| The name of the curator that was present in the transaction 	|
| Is Curated 	| is_curated 	| both 	| boolean 	| True 	| Curation 	| True if the transaction occurred via a curator 	|
| Demand Channel 	| demand_channel 	| both 	| string 	| False 	| Transaction 	| The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). 	|
| Demand Channel ID (Selectable via "Show IDs as separate column" option) 	| demand_channel_id 	| both 	| int 	| True 	| Transaction 	| The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). 	|
| Demand Channel Name (Selectable via "Show IDs as separate column" option) 	| demand_channel_name 	| both 	| string 	| False 	| Transaction 	| The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). 	|
| Imp Type 	| imp_type 	| both 	| string 	| False 	| Transaction 	| The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) 	|
| Imp Type Id 	| imp_type_id 	| both 	| int 	| True 	| Transaction 	| The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) 	|
| Call Type 	| call_type 	| both 	| string 	| True 	| Integration 	| The Impbus handler the impression originated from 	|
| Sdk Version 	| sdk_version 	| monetize_supply_analytics 	| string 	| False 	| Integration 	| The version of the Xandr SDK (AST or Mobile SDK) used to generate the ad request. 	|
| Mobile Application 	| mobile_application 	| both 	| string 	| False 	| Domain / App 	| The application the bundle on the ad request was mapped to 	|
| Mobile Application ID (Selectable via "Show IDs as separate column" option) 	| mobile_application_id 	| both 	| int 	| False 	| Domain / App 	| The ID for the application the bundle on the ad request was mapped to 	|
| Mobile Application Name (Selectable via "Show IDs as separate column" option) 	| mobile_application_name 	| both 	| string 	| False 	| Domain / App 	| The name for the application the bundle on the ad request was mapped to 	|
| Site Domain 	| site_domain 	| both 	| string 	| False 	| Domain / App 	| The domain detected for the ad request 	|
| Country Code 	| geo_country 	| both 	| string 	| True 	| Geography 	| The country 2 digit code in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country information is not provided. Country information is detected by the IP address of the user. Note: Some discrepancies are normal with external data sources due to differences between country detection methods. 	|
| Geo Country Name 	| geo_country_name 	| both 	| string 	| False 	| Geography 	| The country name in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country information is not provided. Country information is detected by the IP address of the user. Country information is detected by the IP address of the user. Note: Some discrepancies are normal with external data sources due to differences between country detection methods. 	|
| Day 	| day 	| both 	| date 	| False 	| Time and Date 	| The day of the auction 	|
| Hour 	| hour 	| both 	| date 	| False 	| Time and Date 	| The hour of the auction. Note: For impressions older than 100 days, the day will be returned rather than the hour. 	|
| Month 	| month 	| both 	| date 	| False 	| Time and Date 	| The month of the auction 	|
| Filtered Request Reason 	| filtered_request_reason 	| both 	| string 	| False 	| Request / Response 	| The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are: "Invalid Domain" (1), "Invalid IP" (2), "Suspected Domain Detection Tampering" (3, 4, 5), "Unknown" (6, 7), “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks, “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify, "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. 	|
| Filtered Request Reason Id 	| filtered_request_reason_id 	| both 	| int 	| False 	| Request / Response 	| The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are: "Invalid Domain" (1), "Invalid IP" (2), "Suspected Domain Detection Tampering" (3, 4, 5), "Unknown" (6, 7), “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks, “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify, "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. 	|

### Revenue types

Revenue types supported by the new reports include:

- **Flat CPM**: Fixed payment per 1,000 impressions.
- **CPC**: Payment per click.
- **Revshare**: Revenue-sharing model based on CPC or CPA.

| Name               | Description                                             |
|--------------------|---------------------------------------------------------|
| **No Payment**     |                                                         |
| **Flat CPM**       | A flat payment per 1000 impressions.                    |
| **Cost plus CPM**  | Cost (what you spend on inventory) plus an extra CPM.   |
| **Cost plus margin**| Cost (what you spend on inventory) plus a percentage of what you spend. |
| **CPC**            | A flat payment per click.                              |
| **CPA**            | A flat payment per conversion.                         |
| **Revshare**       | A payment on a revshare basis (CPC or CPA).             |
| **Estimated CPM**  | The estimated payment per 1000 impressions.            |
| **CPVM**           | A flat payment per 1000 viewable impressions.          |

### Impression types

The following impression types are reported:

| Value | Name                 | Definition                                          |
|-------|----------------------|-----------------------------------------------------|
| 1     | Blank                | No creative served.                                 |
| 2     | PSA                  | A public service announcement served because no other creative was eligible. |
| 3     | Default Error        | A default creative served due to a timeout issue.   |
| 4     | Default              | A default creative served because no line item bid or no other creative was eligible. |
| 5     | Kept                 | One of your managed advertisers served a creative.  |
| 6     | Resold               | The impression was sold to a third-party buyer.     |
| 7     | RTB                  | Your creative served on third-party inventory.      |
| 8     | PSA Error            | A public service announcement served due to a timeout issue. |
| 9     | External Impression  | An impression from an impression tracker.           |
| 10    | External Click       | A click from a click tracker.                       |
| 11    | Insertion            | Your creative served on third-party inventory where it persists across page-loads and sessions. |

### Run your reports

Follow these steps to generate your report:

1. Select **Reports** from the main menu.
1. Customize your Filters, Dimensions, Metrics, and Advanced Options.

   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](#).

1. Click **Run Report** to view your data.

   **Tip**: For larger datasets, consider using the API for quicker downloads.

1. Apply the relevant filters to limit the data displayed to only the information you want. For example, you may want to view impressions for a select few inventory sources instead of all available sources. When you click **Data Filters**, a selection panel appears where you can choose filters from the menu or use the search bar to find a specific filter.

1. **Group by Dimension**: Grouping allows you to organize data rows as needed. Dimensions are grouped into major categories. Click the arrow next to a category to see all dimensions under it, or use the search bar to find the desired dimension.
1. **Select Your Metrics**: Metrics are grouped into major categories. Click the arrow next to a category to see all available metrics, or use the search bar to find the metric you need.
1. Select your time range and interval from the menu. Under **Advanced Options**, you can also choose your preferred **Currency** and **Time zone**.

   > [!TIP]
   > You can select either member or USD as the currency. This affects how monetary fields are displayed in your report. For example, if you select **Advertiser** and choose **Member** for currency, the report shows all monetary data in the member’s currency, including data related to child objects like line items.

1. Click **Run Report**.

   > [!WARNING]
   > Dangerous certain consequences of an actionThe more dimensions you group by, the larger the dataset returned. This may impact processing time.

## Report results

Once the data is ready, it will be displayed in the report interface.

### Key features of report results

- **Initial Display**: The first 500 rows of data are shown in the interface.
- **Downloading Options**: Users can download the full report for comprehensive analysis.

   > [!TIP]
   > The maximum size for reports downloaded from the UI is 100 MB, with a limit of 100,000 rows in Excel or xlsx formats. For larger datasets, use the API, which supports up to 10 million rows.

### Pivot table settings

Users can modify report columns:

- **Add/Remove Dimensions and Metrics**: Use the **Modify Selections** panel.
- **Reorder Columns**: Drag and drop dimensions and metrics for a custom layout.

   > [!WARNING]
   > Large datasets may take longer to process. Group data by only the necessary dimensions to optimize performance.

## API Report

### Create a JSON formatted report request

The JSON request should include the following key fields:

- **report_type**: `monetize_supply_analytics` or `monetize_creative_brand_analytics`.
- **columns**: List of dimensions and metrics.
- **report_interval**: Time period for the report.
- **format**: CSV, Excel, or HTML.

For a complete list of fields that can be included in the JSON file, see the Report Service.

### Example JSON request

To create an API report request, format the JSON file as shown below:

```

$ {code}$ cat monetize_supply_analytics
{
    "report": {
        "report_type": "monetize_supply_analytics",
        "columns": ["hour", "seller_member_name", "buyer_member_name", "advertiser_name", "publisher_name", "imps", "clicks"],
        "report_interval": "last_48_hours",
        "format": "csv"
    }
}
```

**Submit the request**.

## POST the request to the reporting service

Use the following *curl* command to submit the request:

```

{code}$ curl -b cookies -X POST -d @ monetize_supply_analytics 'https://api.appnexus.com/report'
{
   "response": {
      "status": "OK",
      "report_id": "097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

## GET the report status from the report service

After submitting a report request, use the GET method to check the status.

### Example request

```
{code}$ curl -b cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69' 
```
{ 

   "response":{ 
      "status":"OK", 
      "report":{ 
         "name":null, 
         "created_on":"2010-05-25 19:19:53", 
         "json_request":"{\"report\":{\"report_type\":\"monetize_supply_analytics\",\"columns\":[\"hour\",\"seller_member_name\", 
            \"buyer_member_name\",\"advertiser_name\",\"publisher_name\",\"imps\",\"clicks\"], 
            \"row_per\":[\"hour\",\"seller_member_id\",\"buyer_member_id\",\"advertiser_id\",\"publisher_id\"], 
            \"report_interval\":\"last_48_hours\"}}", 
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592" 
      }, 
      "execution_status":"ready" 
   } 
}

### Response
 
  - execution_status: Shows the current status (pending, ready, etc.).

> [!TIP]
> Continue polling until execution_status is ready.

## GET the report data from the report download service 
 

Once the report is ready, download the data using the report-download service.

### Example request

```bash
curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/monetize_supply_analytics.csv

```

> [!NOTE]
> The following points outline key considerations for file downloads and API usage:
>
> - File Format: Ensure the downloaded file’s extension (e.g., .csv, .xlsx) matches the format specified in the request.
> - Error Handling: Use -i or -v in your curl call to display response headers and identify any HTTP errors.
> - Limitations: Reports downloaded as .xlsx or Excel files are limited to 100,000 rows. For larger datasets, use the API limit of 10 million rows.

## Related topics

- [Microsoft Monetize - Impression counting](impression-counting.md)
- [Mobile SDK - Impression counting methods](../mobile-sdk/impression-counting-methods.md)
- [Microsoft Monetize - Introduction to viewability](introduction-to-viewability.md)
- [Microsoft Monetize - Availability of reporting data](availability-of-reporting-data.md)
- [Microsoft Monetize - Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)
- [Microsoft Monetize - Report throttling](report-throttling.md)
- [Digital Platform API - Report service](../digital-platform-api/report-service.md)
