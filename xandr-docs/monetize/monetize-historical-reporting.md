---
title: Microsoft Monetize - Historical Reporting
description: Learn how Monetize Historical Reporting consolidates legacy reports, offering enhanced analytics, streamlined navigation, and improved performance insights.
ms.date: 10/18/2024
---

# Microsoft Monetize -  Historical reporting


> [!NOTE]
> Historical report in Microsoft Monetize is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

## Overview

Historical report is the primary analytics report in Microsoft Monetize, offering comprehensive data across a wide range of dimensions and metrics. It consolidates more than ten legacy report types, including Network Analytics, Seller Brand Review, and Seller Fill and Delivery. It reduces the number of report types a user needs to interact with, providing features to improve usability such as categorization of Dimensions and Metrics and comprehensive search capabilities. Historical report is built from two datasets accessible through a single interface, with Dimension and Metric incompatibilities surfaced during selection. The expanded range of options provides a more detailed view of data across multiple aspects of delivery and inventory, with additional reportable dimension combinations, such as placement and device. The Historical report includes most of the data available in the legacy reporting system. 

> [!NOTE]
> During the Alpha phase, additional dimensions and metrics are added to address key feature gaps compared to the legacy reports. Data in the Historical report is available from 10 October 2024 for general access, with earlier availability in 2024 for clients participating in the Alpha phase. The reporting interface in Microsoft Monetize provides access to the Historical report for Network users. Access to all existing report types is available during the Alpha phase, along with support for Publisher and Advertiser users.


<!-->
The new Microsoft Monetize reporting UI and the Historical report are currently in Alpha, enabled for select clients. Please contact your account manager if you require further information.

The Historical report already includes most of the data that is available in the legacy reporting. During the Alpha phase, we will be adding additional dimensions and metrics to close outstanding key feature gaps compared to the legacy reports. Data in the Historical Report is available from 10th October 2024 generally, and from earlier in 2024 for clients involved in the Alpha.

Currently, the new reporting UI only provides access to the Historical report for Network users. Access to all existing report types will be added during the Alpha, along with support for Publisher and Advertiser users.

### New report types and user interface for Monetize

The new **Historical report** in the new Microsoft Monetize reporting UI offers comprehensive data across a wide range of dimensions and metrics. This report will replace several legacy Network and Advertiser/Publisher reports, enhancing and simplifying reporting capabilities.

The Historical report is built from two datasets that are accessible from one UI, with dimension and metric incompatibilities shown to the user as they make selections. In the API, the datasets are available independently as two report types.

The updated, expanded range enables a more granular understanding of data across multiple aspects of delivery and inventory, with new reportable combinations of dimensions that were not possible before, such as placement and device.

The new UI is a significant upgrade, reducing the number of report types a user needs to interact with, providing features to improve usability such as categorization of Dimensions and Metrics and comprehensive search capability. -->

### Report mappings

Delivery Analytics and Inventory Analytics reports are consolidated into a single Historical report builder experience. This integration streamlines reporting workflows and provides expanded insights into performance and inventory that provides:
- Consolidated reporting for comprehensive performance analysis
- Broader coverage of metrics and dimensions

| Legacy Report Name      | Mapped Report Name | API Name                           |
|---------------------|-------------------|-----------------------------------  |
| Delivery Analytics  | Historical Report | `monetize_creative_brand_analytics` |
| Inventory Analytics | Historical Report | `monetize_supply_analytics`         |

> [!NOTE]
> Coverage of dimensions and metrics is in progress. Additional fields are being added to support the deprecation of legacy report types.

<!--
## New features

### Report enhancements

- Bringing together the new Delivery and Inventory analytics reports into one **Historical report builder** experience:

  - Consolidated reporting for better performance insights.
  - Broader coverage of metrics and dimensions.

| Legacy UI Name      | New UI Report Name | API Name                           |
|---------------------|-------------------|-----------------------------------  |
| Delivery Analytics  | Historical Report | `monetize_creative_brand_analytics` |
| Inventory Analytics | Historical Report | `monetize_supply_analytics`         |

> [!NOTE]
> Coverage of dimensions and metrics is under development. Additional fields are planned to enable the deprecation of legacy report types. 

## New user interface

### Improved navigation

Access reports with fewer clicks for enhanced usability.   -->

## Legacy reports

Legacy reports will no longer receive Microsoft Monetize data starting mid-2025. Historical data will remain accessible based on each report’s standard retention period or 730 days, whichever is shorter. This is applicable to reports such as Network Analytics and Advertiser Video Analytics. Users should transition to new reports to access data generated after 10 October 2024. These new report types automatically include data for all impression types except for 7=RTB (a buying transaction on supply from another seat to your own) for Microsoft Monetize sellers. 
> [!NOTE]
> - Communication will be provided in advance to support the transition process.
> - Reporting for Microsoft Invest and External SSPs is not included in these datasets.

<!--
Legacy reports are planned to not be populated with new Monetize data from mid 2025. Historic data will be available up to the individual report's standard retention and or 730 days, whichever is lower. This includes reports like *Network Analytics* and *Advertiser Video Analytics*. Users are encouraged to transition to the new reports as soon as possible for reports accessing data after 10th October 2024.

> [!NOTE]
> Communication will be sent in advance to support the transition.

### Scope of data

These new report types automatically include data for all impression types except for 7=RTB (a buying transaction on supply from another seat to your own) for Monetize Sellers. Reporting for Invest and External SSPs is not included in these datasets. -->

## Legacy report types

### Network report types

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
| Video Analytics                     | video_analytics_network               |
| Video Error Analytics               | video_error_analytics_network         |
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
| Publisher Video Analytics Report  | video_analytics_network_publisher   |
| Publisher Video Error Report      | video_error_analytics_network       |

## Historical report creation

The Historical report enables streamlined report creation. Users can select from various **Dimensions**, **Metrics**, and **Filters** to customize their reports.

:::image type="content" source="media/create-new-report.png" alt-text="The screenshot shows how to create new reports.":::

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
| `Buyer Member`| No| Buyside| The name of the Xandr buyer member that purchased the impression. 	|
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
| total_revenue_ecpa | The total revenue per acquisition. |

<!--
### Dimensions

| UI column| API column| Report Type| Type| Filter?| Grouping| Description|
|---|---|---|---|---|---|---|
|`Advertiser`| `advertiser`| both| string| No| Buyside | The advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Advertiser ID` (Selectable via "Show IDs as separate column" option)| `advertiser_id`| both| int| Yes | Buyside | The ID of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Advertiser Name` (Selectable via "Show IDs as separate column" option)| `advertiser_name`|both| string | No| Buyside| The name of the advertiser that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Bidder`| `bidder`| both| int | No| Buyside| The Bidder object (in most cases this is a DSP).|
| `Bidder ID` (Selectable via "Show IDs as separate column" option)| `bidder_id`| both| int| Yes| Buyside| The ID of the Xandr Bidder object (in most cases this is a DSP).|
| `Bidder Name` (Selectable via "Show IDs as separate column" option)| `bidder_name`| both| int| No| Buyside | The name of the Xandr Bidder object (in most cases this is a DSP).|
| `Billing Period`| `billing_period_id` | both | int | Yes| Buyside| The ID of the Billing Period |
| `Billing Period. Booked Imps Budget Daily`| `billing_period.booked_imps_budget_daily`| both| int| No | Buyside | The daily impression budget of the insertion order's billing period.|
| `Billing Period.Booked Imps Budget Lifetime`| `billing_period.booked_imps_budget_lifetime` | both | int| No | Buyside | The lifetime impression budget of the insertion order's billing period.|
| `Billing Period.Start Date`| `billing_period.start_date`| both| datetime| No| Buyside| The earliest date of the insertion order's billing period. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.|
| `Billing Period.End Date`| `billing_period.end_date` | both| datetime| No| Buyside| The last date of the insertion order's billing period. Note: Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `Billing Period.External Code`| b`illing_period.external_code`| both| int| No| Buyside| The custom code for the billing period.|
| `Buyer Member`| `buyer_member`| both| string| No| Buyside| The name with ID in brackets of the Xandr buyer member that purchased the impression 	|
| `Buyer Member ID` (Selectable via "Show IDs as separate column" option)| `buyer_member_id`| both| int | Yes| Buyside| The ID of the Xandr buyer member that purchased the impression|
| `Buyer Member Name` (Selectable via "Show IDs as separate column" option)| `buyer_member_name`| both| string | No| Buyside| The Name of the Xandr buyer member that purchased the impression 	|
| `Buyer Seat`| `buyer_seat`| both | string| No| Buyside| The seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts.|
| `Buyer Seat ID` (Selectable via "Show IDs as separate column" option) | `buyer_seat_id` | both| int| Yes| Buyside | The ID of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts. |
| `Buyer Seat Name` (Selectable via "Show IDs as separate column" option)| `buyer_seat_name`| both | string| No| Buyside| The name of the seat for the Bidder. This enables reporting on sub-seats for bidders that do not have buyer_member_id breakouts.|
| `Buyer Seat Code`| `buyer_seat_code` | both| string | No | Buyside | The custom buyer seat ID (submitted by DSP) which was used to bid on the impression|
| `Flight Id`| `flight_id`| both | int | No | Buyside | The ID of the line item flight under which the impression was purchased.|
| `Flight.Booked Impressions Budget Daily`| `flight.booked_impressions_budget_daily`| both | int| No | Buyside| The daily impression budget for the line item's flight.|
| `Flight.Booked Impressions Budget Lifetime`| `flight.booked_impressions_budget_lifetime`| both| int| No| Buyside| The lifetime impression budget for the line item's flight.|
| `Flight.Start Date` | `flight.start_date`| both| datetime| No| Buyside| The start date of the line item's flight.|
| `Flight.End Date`|` flight.end_date`| both| datetime| No| Buyside| The end date of the line item's flight.|
| `Insertion Order`| `insertion_order`| both| string | Yes| Buyside| The insertion order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Insertion Order ID` (Selectable via "Show IDs as separate column" option)| `insertion_order_id`| both | int| No| Buyside| The insertion order ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Insertion Order Name` (Selectable via "Show IDs as separate column" option)| `insertion_order_name`| both| string | No| Buyside | The insertion order name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression.|
| `Insertion Order.Billing Code`| `insertion_order.billing_code`| both| string| No| Buyside| The billing code associated with the insertion order (if there is one).|
| `Insertion Order.End Date`| `insertion_order.end_date`| both| datetime| No| Buyside| The end date of the insertion order (for legacy insertion orders).|
| `Insertion Order.Start Date`| `insertion_order.start_date` | both | datetime| No| Buyside 	| The start date of the insertion order (for legacy insertion orders).|
|`Insertion Order.State`| insertion_order.state| both| string| No | Buyside| The state of the insertion order (e.g., active, inactive).|
| `Insertion Order.Type` | `insertion_order.type` | both| int| Yes| Buyside| The type of insertion order associated with the impression (e.g. Legacy, Seamless).|
| `Line Item` | `line_item` | both | string | No| Buyside 	| The line item order that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. 	|
| `Line Item Id` (Selectable via "Show IDs as separate column" option) 	| `line_item_id` 	| both 	| int 	| Yes| Buyside| The line item ID that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Line Item Name` (Selectable via "Show IDs as separate column" option)| `line_item_name`| both 	| string | No | Buyside| The line item name that bought the impression. This will be an object owned by the seller and will be populated for a managed bought or deal v2 impression. |
| `Line Item.Comments`| `line_item.comments`| both | string | No 	| Buyside 	| Any comments that have been entered for this line item.|
| `Line Item.Start Date` | `line_item.start_date`| both| datetime | No 	| Buyside 	| The start date of the line item.|
| `Line Item.End Date`|`line_item.end_date`| both| datetime| No | Buyside 	| The end date of the line item. |
| `Line Item.Status` | line_item.status | both| string| No| Buyside 	| The state of the line item (e.g., active, inactive).|
| `Line Item.Code`| `line_item_code`| both| string | No| Buyside| The optional external code applied to the line item.|
| `Li Priority`| `li_priority`| both| string | Yes | Buyside | The bidding priority for a line item that targets direct inventory. For more information, see Bidding Priority in the UI Documentation. Possible values: 1 - 20, where 20 is the highest priority.|
| `Li Subtype` | `li_subtype`| both| string | Yes| Buyside| The line item subtype (e.g., Augmented, Deal, Guaranteed). |
| `Li Subtype ID`(Selectable via "Show IDs as separate column" option) | `li_subtype_id`| both| int| No| Buyside| The line item subtype ID.|
| `Li Subtype Name` (Selectable via "Show IDs as separate column" option)| `li_subtype_name`| both| string| No | Buyside| The line item subtype name. |
| `Salesrep For Line Item`| `salesrep_for_line_item` | both| string| Yes| Reporting Labels| A custom reporting label field containing the sales representative. You may only select one reporting label per report.|
| `Trafficker For Line Item` | `trafficker_for_line_item`| both| string | Yes| Reporting Labels| A custom reporting label field containing the trafficker. You may only select one reporting label per report. |
| `Type For Line Item` | `type_for_line_item`| both| string | Yes| Reporting Labels| A custom reporting label field used to list the line item type (e.g., Retargeting LI). This is not the same as the Type attribute described above. You may only select one reporting label per report.|
| `Insertion Order Type Label`| `insertion_order_type` | both| string | Yes| Reporting Labels 	| A custom reporting label field used to list the insertion order type (e.g., Branding IO). This is not the same as the Type attribute described above. You may only select one reporting label per report.|
| `Insertion Order.Sales Rep Label` | `insertion_order.sales_rep_label`| both| string | Yes| Reporting Labels| A customer reporting label field used to list the sales representative associated with the insertion order. You may only select one reporting label per report.|
| `Insertion Order.Trafficker Label` | `insertion_order.trafficker_label`| both| string| Yes| Reporting Labels| A customer reporting label field used to list the trafficker associated with the insertion order. You may only select one reporting label per report.|
| `Placement`| `placement`| both| string | No| Sellside| The Xandr Placement for the impression.|
| `Placement ID` (Selectable via "Show IDs as separate column" option)| `placement_id`| both| int| Yes| Sellside | The ID of the Xandr Placement for the impression.|
| `Placement Name` (Selectable via "Show IDs as separate column" option)| `placement_name`| both| string| No | Sellside| The name of the Xandr Placement for the impression.|
| `Placement.Code`| `placement.code`| both| string| No| Sellside| The code of the Xandr Placement for the impression.|
| `Placement.Code2`| `placement.code2`| both | string| No| Sellside| The code of the Xandr Placement for the impression. |
| `Placement.Code3`| `placement.code3`| both| string | No| Sellside| The code of the Xandr Placement for the impression.|
| `Placement Group`| `plmt_grp`| both | string | No| Sellside| Xandr Placement Group for the impression.|
| `Placement Group ID` (Selectable via "Show IDs as separate column" option)| `plmt_grp_id`| both| int| Yes | Sellside| The ID of the Xandr Placement Group for the impression. |
| `Placement Group Name` (Selectable via "Show IDs as separate column" option)| `plmt_grp.name`| both| string| No| Sellside | The name of the Xandr Placement Group for the impression.|
| `Placement Group.Code`| `plmt_grp.code`| both| string| No| Sellside| The code of the Xandr Placement Group for the impression.|
| `Publisher` | `publisher`| both | string | No | Sellside | The Xandr Publisher for the impression. |
| `Publisher ID` (Selectable via "Show IDs as separate column" option)| `publisher_id`| both| int| Yes | Sellside| The ID of the Xandr Publisher for the impression.|
| `Publisher Name` (Selectable via "Show IDs as separate column" option)| `publisher_name`| both| string | No | Sellside| The name of the Xandr Publisher for the impression. |
| `Brand`| `brand`| monetize_creative_brand_analytics| string | No| Creative| The Brand as determined by the Xandr creative audit or self assigned for managed traffic |
| `Brand ID` (Selectable via "Show IDs as separate column" option)| `brand_id`|monetize_creative_brand_analytics| int| Yes | Creative | The ID for the Brand as determined by the Xandr creative audit or self assigned for managed traffic |
| `Brand Name` (Selectable via "Show IDs as separate column" option)| `brand_name` | monetize_creative_brand_analytics| string | No | Creative | The name for the Brand as determined by the Xandr creative audit or self assigned for managed traffic|
| `Brand Category ID` | `brand_category_id`| monetize_creative_brand_analytics| int|Yes| Creative| The parent category ID for the creative's assigned brand|
| `Brand Category Name` | `brand_category_name` | monetize_creative_brand_analytics | string | No   | Creative | The parent category name for the creative's assigned brand                                         |
| `Creative` | `creative` | monetize_creative_brand_analytics | string | No   | Creative | Creative that served. It will only be populated for managed impressions.|
| `Creative ID` (Selectable via "Show IDs as separate column" option) | `creative_id`| monetize_creative_brand_analytics | int| Yes| Creative | The Xandr ID for the creative that served.                                                         |
| `Creative Name` (Selectable via "Show IDs as separate column" option) | `creative_name` | monetize_creative_brand_analytics | string | No | Creative | The Xandr name for the creative that served. The name will only be populated for managed impressions. |
| `Creative Code`  | `creative_code` | monetize_creative_brand_analytics | string | No| Creative | The code of the creative. |
| `Creative Media Type` | `creative_type` | both| string | No   | Creative | The media type of the creative that transacted                                                     |
| `Creative Media Type ID` (Selectable via "Show IDs as separate column" option) | `creative_type_id` | both | int | No | Creative | The media type ID of the creative that transacted                                                  |
| `Size` | `size` | both  | string | Yes  | Creative | For display creatives, this is the creative width x height in pixels |
| `Domains Exposed Id` | `domains_exposed_id`| monetize_supply_analytics | int | No   | Visibility | Whether this inventory's domains are exposed for targeting by buyers. Allowed values: "Exposed", "Not exposed" |
| `Domains Exposed`| `domains_exposed` | monetize_supply_analytics     | int    | No   | Visibility | Whether this inventory's domains are exposed for targeting by buyers. Allowed values: "Exposed", "Not exposed" |
| `Exposed For Resale` | `exposed_for_resale`       | monetize_supply_analytics     | string | No   | Visibility | Viewability profile, used by sellers to expose/hide their content_categories info to buyers |
| `Exposed For Resale Id` | `exposed_for_resale_id` | monetize_supply_analytics     | int    | No   | Visibility | Viewability profile, used by sellers to expose/hide their publisher info to buyers |
| `Allowed Media Types` | `allowed_media_types_bitmap_name` | monetize_supply_analytics | string | No | Inventory | An array of the permitted media types for the impression  |
| `Audit Type` | `audit_type`| monetize_supply_analytics | string | No | Inventory | The type of audit performed on the domain where the impression occurred.                           |
| `Audit Type ID` (Selectable via "Show IDs as separate column" option) | `audit_type_id` | monetize_supply_analytics | int | Yes | Inventory | The ID of the type of audit performed on the domain where the impression occurred.|
| `Audit Type Name` (Selectable via "Show IDs as separate column" option) | `audit_type_name` | monetize_supply_analytics | string | No | Inventory | The name of the type of audit performed on the domain where the impression occurred. |
| `Browser`| `browser` | monetize_supply_analytics| string  | No   | Inventory   | The Name and ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service. |
| `Browser ID` (Selectable via "Show IDs as separate column" option) | `browser_id`| monetize_supply_analytics  | int     | Yes    | Inventory   | The ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the Browser Service.         |
|`Content Category`| `content_category` | monetize_supply_analytics  | string  | No   | Inventory   | The ID and name of the universal content category associated with the audited domain.                                           |
| `Content Category ID` (Selectable via "Show IDs as separate column" option) | `content_category_id` | monetize_supply_analytics  | int | Yes    | Inventory   | The ID of the universal content category associated with the audited domain.                                                   |
| `Content Category Name` (Selectable via "Show IDs as separate column" option) | `content_category_name` | monetize_supply_analytics  | string  | No   | Inventory   | The name of the universal content category associated with the audited domain.|
| `Fold Position` | `fold_position`| monetize_supply_analytics  | string  | No   | Inventory   | The fold position, i.e. where on the page the placement is located. For allowed values, see fold_position_id.                |
| `Fold Position Id`| `fold_position_id`  | monetize_supply_analytics  | int     | Yes    | Inventory   | The ID of the fold position, i.e. where on the page the placement is located. Possible values for impressions: 0 = "unknown", 1 = "above", 2 = "below". |
| `Supply Type` | `supply_type_id` | both | int     | Yes    | Inventory   | The ID of the type of inventory.                                                                                             |
| `Supply Type Name` | `supply_type_name`     | both  | string  | No   | Inventory   | The type of inventory. Possible values: "web", "mobile_web", "mobile_app", "facebook_sidebar".                                |
| `Prebid Server Eligible` | `prebid_server_eligible` | both  | int | Yes    | Prebid Server | Yes if PSP was eligible to bid into the auction for the impression. |
| `Prebid Server Eligible` | `prebid_server_eligible_name` | both  | string  | No   | Prebid Server | Yes if PSP was eligible to bid into the auction for the impression. |
| `SSP` | `ssp`  | both    | string  | No   | Prebid Server | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `SSP ID` (Selectable via "Show IDs as separate column" option) | `ssp_id` | both  | int | No   | Prebid Server | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `SSP Name` (Selectable via "Show IDs as separate column" option) | `ssp_name` | both                       | string  | No | Prebid Server | When the transaction is bought by PSP (bidder_id=443) this field will show the individual SSP that transacted. Otherwise, the SSP will be recorded as Monetize. |
| `Deal` | `deal` | both  | string  | No   | Deals | The name and ID of the affected deal. |
| `Deal ID` (Selectable via "Show IDs as separate column" option) | `deal_id`   | both   | int     | Yes    | Deals | The ID of the deal.|
| `Deal Name` (Selectable via "Show IDs as separate column" option) | `deal_name` | both  | string  | No   | Deals | The name of the affected deal.|
| `Deal Type` | `deal_type`  | both | string  | Yes | Deals  | Possible values: Open Auction (1), Private Auction (2), First Look (3), Programmatic Guaranteed (4), Curated (5 - only relevant for Curators). |
| `Revenue Type` | `revenue_type` | both    | string  | No   | Payment     | For managed line items, this is the basis on which the booked revenue gets recorded for the Seller.  |
| `Revenue Type` (Selectable via "Show IDs as separate column" option) | `revenue_type_id` | both | int | Yes | Payment | The basis on which the advertiser has agreed to pay you for the impression.   |
| `Carrier` | `carrier`  | monetize_supply_analytics  | string  | No   | Device      | The carrier for the device on which the impression was served.                                                              |
| `Carrier ID` (Selectable via "Show IDs as separate column" option) | `carrier_id` | monetize_supply_analytics  | int | Yes    | Device      | The ID of the carrier for the device on which the impression was served.|
| `Carrier Name` (Selectable via "Show IDs as separate column" option) | `carrier_name` | monetize_supply_analytics| string| No   | Device      | The name of the carrier for the device on which the impression was served.  |
| `Device Make`| `device_make` | monetize_supply_analytics  | string  | No | Device| The device manufacturer |
| `Device Make ID (Selectable via "Show IDs as separate column" option)` | `device_make_id`  | monetize_supply_analytics| int| Yes  | Device | The ID of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). |
| `Device Make Name` (Selectable via "Show IDs as separate column" option)| `device_make_name` | monetize_supply_analytics  | string  | No | Device | The name of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). To retrieve a complete list of device make IDs and names, use the Device Make Service.|
| `Device Model` | `device_model`  | monetize_supply_analytics  | string| No   | Device   | The ID and name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). |
| `Device Model ID` (Selectable via "Show IDs as separate column" option) | `device_model_id` | monetize_supply_analytics  | int  | Yes | Device | The ID of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). |
| `Device Model Name` (Selectable via "Show IDs as separate column" option) | `device_model_name`| monetize_supply_analytics  | string  | No   | Device | The name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). |
| `Device Type` | `device_type`  | monetize_supply_analytics  | string  | No   | Device | The device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box |
| `Device Type ID`| `device_type_id` | monetize_supply_analytics  | int | Yes | Device | The ID of the device type the impression originated from. 0=Unknown, 1=PC, 2=Phone, 3=Tablet, 4=TV, 5=Game Console, 6=Media Player, 7=Set top box |
| `Operating System` | `operating_system`  | monetize_supply_analytics  | string  | No   | Device  | The name of the operating system of the device followed by the ID (Microsoft Advertising format). |
| `Operating System ID` (Selectable via "Show IDs as separate column" option) | `operating_system_id` | monetize_supply_analytics  | int | Yes| Device | The ID of the operating system of the device. |
| `Operating System Name` (Selectable via "Show IDs as separate column" option) | `operating_system_name`  | monetize_supply_analytics  | string  | No| Device  | The name of the operating system of the device. |
| `Operating System Family` | `operating_system_family` | monetize_supply_analytics  | string  | No   | Device| The name of the operating system family (e.g., Android, Microsoft Windows) of the device followed by the ID (Microsoft Advertising format). |
| `Operating System Family ID` (Selectable via "Show IDs as separate column" option) | `operating_system_family_id` | monetize_supply_analytics| int | Yes | Device | The ID of the operating system family associated with the device the impression was served on. |
| `Operating System Family Name` (Selectable via "Show IDs as separate column" option) | `operating_system_family_name` | monetize_supply_analytics  | string  | No   | Device | The name of the operating system family associated with the device the impression was served on. |
| `Curator Member`| `curator_member` | both| string| No| Curation | The ID of the curator that was present in the transaction |
| `Curator Member ID` (Selectable via "Show IDs as separate column" option) | `curator_member_id` | both  | int | Yes | Curation  | The ID of the curator that was present in the transaction |
| `Curator Member Name` (Selectable via "Show IDs as separate column" option) | `curator_member_name` | both  | string  | No| Curation | The name of the curator that was present in the transaction |
| `Is Curated` | `is_curated`  | both  | boolean | Yes | Curation| Yes if the transaction occurred via a curator |
| `Demand Channel`  | `demand_channel` | both  | string  | No   | Transaction  | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Demand Channel ID` (Selectable via "Show IDs as separate column" option) | `demand_channel_id`  | both | int | Yes| Transaction  | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Demand Channel Name` (Selectable via "Show IDs as separate column" option) | `demand_channel_name`| both  | string  | No   | Transaction  | The type of demand that bought the impression. Possible values: Managed (imp_type=5), PSP (bidder_id=443), Standard Deal, Priority Deal, PG Deal, Curation (curator_member_id > 0) and Open Exchange (imp_type=6). |
| `Imp Type` | `imp_type`  | both| string | No| Transaction  | The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) |
| `Imp Type Id` | `imp_type_id`  | both  | int | Yes | Transaction  | The type of transaction. (1=blank, 2=PSA, 3=Default Error, 4=default, 5=kept, 6=resold, 7=RTB, 8=PSA Error, 9=External Impression, 10=External Click, 11=Insertion) |
| `Call Type`| `call_type`  | both| string  | Yes | Integration  | The Impbus handler the impression originated from |
| `Sdk Version`| `sdk_version` | monetize_supply_analytics  | string | No | Integration  | The version of the Xandr SDK (AST or Mobile SDK) used to generate the ad request. |
| `Mobile Application`| `mobile_application`| both  | string  | No | Domain / App | The application the bundle on the ad request was mapped to |
| `Mobile Application ID` (Selectable via "Show IDs as separate column" option) | `mobile_application_id`  | both  | int | No | Domain / App | The ID for the application the bundle on the ad request was mapped to |
| `Mobile Application Name` (Selectable via "Show IDs as separate column" option) | `mobile_application_name` | both| string  | No | Domain / App | The name for the application the bundle on the ad request was mapped to |
| `Site Domain`| `site_domain` | both | string| No   | Domain / App | The domain detected for the ad request |
| `Country Code` | `geo_country` | both  | string  | Yes | Geography  | The country/region 2 digit code in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. Country/region information is detected by the IP address of the user. Note: Some discrepancies are normal with external data sources due to differences between country/region detection methods. |
| `Geo Country Name`| `geo_country_name` | both| string  | No | Geography | The country/region name in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. Country/region information is detected by|
| `Day`  | `day`  | both | date  | No   | Time and Date | The day of the Auction |
| `Hour` | `hour` | both  | date  | No  | Time and Date | The hour of the auction. Note: For impressions older than 100 days, the day will be returned rather than the hour.|
| `Month`  | `month`  | both | date  | No   | Time and Date | The month of the auction|
| `Filtered Request Reason` | `filtered_request_reason`| both | string| No | Request / Response | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are: "Invalid Domain" (1), "Invalid IP" (2), "Suspected Domain Detection Tampering" (3, 4, 5), "Unknown" (6, 7), “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks, “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify, "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. |
| `Filtered Request Reason Id`| `filtered_request_reason_id`| both | int| No | Request / Response | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are: "Invalid Domain" (1), "Invalid IP" (2), "Suspected Domain Detection Tampering" (3, 4, 5), "Unknown" (6, 7), “White Ops: General IVT” (17) - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks, “White Ops: Sophisticated IVT” (18) - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify, "Valid Impression" (0) is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. | -->

## Revenue types

Revenue types supported by Historical report include:
<!-->
- **Flat CPM**: Fixed payment per 1,000 impressions.
- **CPC**: Payment per click.
- **Revshare**: Revenue-sharing model based on CPC or CPA. -->

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

<!--
## Report results

Once the data is ready, it will be displayed in the report interface. -->

<!--
### Key features of report results

- **Initial Display**: The first 500 rows of data are shown in the interface.
- **Downloading Options**: Users can download the full report for comprehensive analysis. 

   > [!TIP]
   > The maximum size for reports downloaded from the UI is 100 MB, with a limit of 100,000 rows in Excel or xlsx formats. For larger datasets, use the API, which supports up to 10 million rows. -->

<!--
### Pivot table settings

Users can modify report columns:

- **Add/Remove Dimensions and Metrics**: Use the **Modify Selections** panel.
- **Reorder Columns**: Drag and drop dimensions and metrics for a custom layout. 

   > [!WARNING]
   > Large datasets may take longer to process. Group data by only the necessary dimensions to optimize performance.
<!--
## API report

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
```

### Response

  - **execution_status**: Shows the current status (pending, ready, etc.).

> [!TIP]
> Continue polling until `execution_status` is ready.

## GET the report data from the report download service
 

Once the report is ready, download the data using the report-download service.

### Example request

```bash
curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/monetize_supply_analytics.csv

```

## Notes and tips

- **File Format**: Ensure the downloaded file’s extension (e.g., .csv, .xlsx) matches the format specified in the request.
- **Error Handling**: Use -i or -v in your curl call to display response headers and identify any HTTP errors.
- **Limitations**: Reports downloaded as .xlsx or Excel files are limited to 100,000 rows. For larger datasets, use the API limit of 10 million rows.
-->


## Related topics

- [Microsoft Monetize - Impression counting](impression-counting.md)
- [Mobile SDK - Impression counting methods](../mobile-sdk/impression-counting-methods.md)
- [Microsoft Monetize - Introduction to viewability](introduction-to-viewability.md)
- [Microsoft Monetize - Availability of reporting data](availability-of-reporting-data.md)
- [Microsoft Monetize - Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)
- [Microsoft Monetize - Report throttling](report-throttling.md)

