---
title: Microsoft Monetize - Import or Export Split CSVs
description: In this article, learn how to create or edit splits in bulk by importing a CSV specifying the details of your splits.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Import or export split CSVs

You can create or edit splits in bulk by importing a CSV specifying the details of your splits.

## Import or export a CSV

> [!NOTE]
> When you import a CSV, it replaces all of the existing splits on your line item. To keep targeting the existing splits, they must be specified in the spreadsheet with the same split IDs.

1. Navigate to the Line item screen, select the **Programmable Splits** section. For more information on Line item, see [Working with Line Items](working-with-line-items.md).
1. Choose the number of splits and select **Start**
1. Click **Actions** > **Import CSV** to import a CSV file or **Actions** > **Export CSV** to export a CSV file.

## CSV rules

- Each row defines a split.
- Columns optionally specify the split ID, name, capped/uncapped status, allocation, active status, feature, or user test group allocation. Optionally, columns can also associate creatives, bids, or expected values with a split. The columns are in an AND relationship. That is, a split matches the criteria specified by all the columns.
- Separate multiple values with commas.
- You can modify any feature to exclude a value with the operator "not". This matches impressions where one or more of the specified values is not true.

Segment operators work slightly differently from other operators:

- Separate multiple segments with commas
- "include" or "exclude" must be specified for all segments
- "ANY" or "ALL" must be specified for segments within a group (even if the group only contains one segment)
  - "ALL" represents AND (it matches impressions when all of the specified values are true)
  - "ANY" represents OR (it matches impressions where one or more of the specified values is true)

## Split settings

The following tables describe the allowed values for each column under various feature classes. All columns are optional.

### Basic information

| Column Title | Description |
|---|---|
| ID | The split ID. If specified, the row will replace the existing split definition. If left blank, a new split will be created and an ID will be assigned automatically. |
| Name | The name of the split. |
| Active | The status of the split. "1" is active and "0" is inactive. If left blank, the split will default to active. |

### Behaviors

| Column Title | Description |
|---|---|
| Spend Allocation | The percentage of the line item budget allocated to the split. The spend allocation for each split should be between 1 and 99. If the sum of all specified splits does not equal 100, the remainder will be assigned to impressions that pass ALI targeting but don't meet any split conditions. |
| Priority | This feature is not yet available through CSV import. |
| Cap | Acceptable values are "constrained" (capped) or "unconstrained" (uncapped). If you don't specify, the split will default to uncapped. |
| Max Bid | How much you are willing to pay for impressions, in the local currency set at the Advertiser level |
| Bid Multiplier | This feature is not yet available through CSV import. |
| Creatives | List the IDs of creatives you would like to serve on this split. <br> **Example:** <br> `98603894, 98714312, 98754614` |
| Custom Macros | This feature is not yet available through CSV import. |
| Test Groups | Activates the user test groups feature, targeting a unique group of users per split for A/B testing. The value represents the percentage of eligible users on the line item to be targeted. <br> **Example:** <br> Target 20% of eligible users: <br> `20` <br> :::image type="content" source="media/splits-test-groups.png" alt-text="Spreadsheet specifying User Test Group allocations and features for all the splits on a line item."::: |

### Geo

For more information, see [Additional Geo Restrictions - ALI](additional-geo-restrictions-ali.md).

| Column Title | Description |
|---|---|
| Country | User country. Values are country IDs, not names. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Country Service](../digital-platform-api/country-service.md). <br> **Example:** <br> Include the United States and Canada: <br> `any 233, 41` |
| Region | User geographic region. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Region Service](../digital-platform-api/region-service.md). <br> **Example:** <br> Include North-East and North-West: <br> `any 538, 541` |
| City | User city. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [City Service](../digital-platform-api/city-service.md). <br> **Example:** <br> Exclude New York and Los Angeles: <br> `not 198423, 181953` |
| Metro Code | User [metro code](additional-geo-restrictions-ali.md). The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md). <br> **Example:** <br> Include Atlanta GA and Augusta GA: <br> `any 524,520` |
| Postal Code | User [postal code](additional-geo-restrictions-ali.md). The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Postal Code Service](../digital-platform-api/postal-code-service.md). <br> **Note:** When specifying postal code, you must also include the country code. For example, to target postcode 2096 in Australia, enter "AU:2096". <br> **Example:** <br> Include US zip codes 11238 and 10010: <br> `any US:11238, US:10010` |

### Inventory

For more information, see [Inventory Targeting](inventory-targeting-ali.md).

| Column Title | Description |
|---|---|
| Size | The placement size of impressions. <br> **Note:** The format for size values is heightXwidth. <br> **Example:** <br> Include 300x600 and 300x800 placements: <br> `any 300X600,300X800` |
| Domain or App | Impression domain ID or app ID. The IDs are listed in the drop-down menu for the field in the UI. Mobile app IDs are also available through the API with the [Mobile App Service](../digital-platform-api/mobile-app-service.md). <br> **Example:** <br> Include cnn.com: <br> `any 324` |
| Placement | Placement ID. The IDs are available through the API with the [Placement Service](../digital-platform-api/placement-service.md). <br> **Example:** <br> Include placements 482348, 506200, and 506199: <br> `any 482348, 506200, 506199` |
| Publisher | Publisher ID. The IDs are available through the API with the [Publisher Service](../digital-platform-api/publisher-service.md). <br> **Example:** <br> Exclude Publisher: <br> `any 233,41` |
| Seller Member | Seller Member ID. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Platform Member Service](../digital-platform-api/platform-member-service.md). <br> **Example:** <br> Exclude Microsoft Advertising Demo and Microsoft Advertising Testing Account: <br> `not 233,41` |
| Inventory type | Inventory type. Options: web, app, all <br> **Example:** <br> Include web inventory: <br> `any web` |
| Inventory list | Inventory blocklist or allowlist. <br> **Examples:** <br> Target allowlist 16245: <br> `all 16245` <br> Exclude blocklist 150: <br> `not_any 150` |

### System

For more information, see [Buy-Side Targeting](buy-side-targeting.md).

| Column Title | Description |
|---|---|
| Operating System Family | User operating system family ID. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Operating System Family Service](../digital-platform-api/operating-system-family-service.md). <br> **Example:** <br> Include Microsoft Windows: <br> `any 5` |
| Operating System Version | User operating system ID. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Operating System Service](../digital-platform-api/operating-system-service.md). <br> **Example:**<br> Include Android Gingerbread 2.3.3 and 2.3.4: <br> `any 22,23` |
| Browser | Browser ID. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Browser Service](../digital-platform-api/browser-service.md). <br> **Example:** <br> Exclude Firefox 3, 4, and other versions: <br> `not 6, 4, 7` |
| Browser Language | Browser language ID. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Language Service](../digital-platform-api/language-service.md). <br> **Example:** <br> Include English: <br> `any 1` |
| Device type | The type of device to be targeted. Options are "pc & other devices", "phone", and "tablet". <br> **Example:** <br> Exclude phones and tablets: <br> `not phone, tablet` |
| Device carrier | The ID of the specific mobile carrier. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Carrier Service](../digital-platform-api/carrier-service.md). <br> **Example:** <br> Include AT&T and Verizon: <br> `any 60, 14` |
| Model | The ID of the device model. The IDs are listed in the drop-down menu for the field in the UI or available through the API with the [Device Model Service](../digital-platform-api/device-model-service.md). <br> **Example:** <br> Include Samsung Galaxy Tab GT-P1000, GTP1000T, GTP1010: <br> `any 5941, 5946, 5947` |

### Inventory performance

For more information, see [Introduction to Viewability](introduction-to-viewability.md).

| Column Title | Description |
|---|---|
| Viewability Threshold | Evaluate web display impressions by how likely they are to be measured as viewable by the IAB standard, as determined by Microsoft Advertising optimization. <br>**Example:** <br> Include impressions that are at least 80% likely to achieve IAB viewability rate: <br> `>=0.8` |
| Video Viewability Threshold | Evaluate web video impressions by how likely they are to be measured as viewable by the IAB standard, as determined by Microsoft Advertising optimization. <br> **Example:** <br> Include impressions that are at least 60% likely to achieve IAB video viewability rate: <br> `>=0.6` |
| Completion Rate Threshold | Evaluate web video impressions by how likely they are to be completed, as determined by Microsoft Advertising optimization. <br> **Example:** <br> Exclude impressions that are no more than 20% likely to be completed: <br> `not <=0.20` |

### Segment

| Column Title | Description |
|---|---|
| Segment Presence/Absence | Segment presence or absence, age, and value. <br> **Example:** <br> Target the following users: <br>1. Include users that have a value of 0 that are in segment ID - 3359836 <br> 2. Include users that are either in segment ID - 1879649 or in segment ID - 39246 <br> 3. Include users that are not in segment ID - 3359827 <br> `ANY include (3359836) [value = 0], ANY include (1879649), include (39246), ANY exclude (3359827)` <br> Target the following users: <br> 4. Exclude users who have been in Segment 108 for less than two hours <br> 5. Include users who have been in Segment 109 for at least 10 minutes and Segment 110 for at least 15 minutes <br> `ALL exclude 108[age<120], ALL include 109[age>=10], include 110[age>=15]` <br> Include if Segment 110 is greater than 3 or Segment 112 is less than 4: <br> `ANY include 110[value>3], include 112[value<4]` <br> Include users who have been in Segment 110 for less than 1440 minutes and whose value is greater than 3: <br> `ANY include 110[age<1440 value>3]` <br> See [CSV Rules](#csv-rules) above for special constraints on segments. |

### Frequency and recency

For more information, see [Frequency Targeting](frequency-and-recency-caps.md).

| Column Title | Description |
|---|---|
| Daily frequency | The number of times the user has seen an ad on this split on the present day. <br> **Example:** <br> Exclude if the user has seen an ad more than 5 times today: <br> `not >5` |
| Lifetime frequency | The number of times the user has seen an ad on this split over their lifetime. <br> **Example:** <br> Include if the user has seen the ad fewer than 5 times over their lifetime: <br> `any <5` |
| Split recency | How recently (in minutes) the user has seen an ad on this split. <br> **Example:** <br> Exclude if the user has seen an ad on this split in the past 10 minutes: <br> `not <=10` |
| Advertiser lifetime frequency | The number of times the user has seen an ad from this advertiser over the user's lifetime. <br> **Example:** <br> Exclude if the user has seen ads from this advertiser more than 20 times in their lifetime: <br> `not >20` |
| Advertiser daily frequency | The number of times the user has seen an ad from this advertiser on the present day. <br> **Example:** <br> Include if the user has seen ads from this advertiser fewer than 3 times today. <br> `any < 3` |
| Advertiser recency | How recently (in minutes) the user has seen an ad from this advertiser. <br> **Example:** <br> Exclude if the user has seen an ad from this advertiser in the past 30 minutes: <br> `not > 30` |
| Line item lifetime frequency | The number of times the user has seen an ad on this line item over the user's lifetime. <br> **Example:** <br> Include if the user has seen an ad from this advertiser 15 or fewer times over their lifetime: <br> `any <=15` |
| Line item daily frequency | The number of times the user has seen an ad on this line item on the present day. <br> **Example:** <br> Exclude if the user has seen an ad on this line item more than 5 times today: <br> `not > 5` |
| Line item recency | How recently (in minutes) the user has seen an ad on this line item. <br> **Example:** <br> Include if the user last saw an ad on this line item more than 3 hours ago: <br> `any > 180` |

## Example CSV

This is a [Sample Splits CSV](https://download.microsoft.com/download/e/e/5/ee544211-092a-45c4-8076-57b5c5aaceb3/28%20Dec%202023/sample-splits-csv.csv).

## Related topics

- [Configure a Programmable Split](configure-a-programmable-split.md)
- [Understanding Splits](understanding-splits.md)
- [Update Splits](update-splits.md)
- [Explore Splits](explore-splits.md)
