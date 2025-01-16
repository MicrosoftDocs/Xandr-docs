---
title: Platform Buyer Report
description: In this article, find information about the Platform buyer report, the metrics and dimensions associated with it, and delivery methods for the report.
ms.date: 10/28/2023
---

# Platform buyer report

The **Run Report** tab is where you configure the type of report you want to run. The **Platform Buyer Report** is displayed by default when you access the Run Report tab. This report has analytics/transaction data, and allows you to drill down into very specific dimensions.

The API documentation for the **Platform Buyer Report** is located [here](bidder-platform-buyer-report.md).

Select details to include in your report in the follow sections of the **Run Report** tab.

## Basic

| Field | Description | Options |
|---|---|---|
| **Interval** (drop-down menu) | Select the time interval you would like the data to be broken down by. Selecting "cumulative" means there will be no time breakout in your report. | - Hourly <br> - Daily <br> - Monthly <br> - Cumulative |
| **Range** (drop-down menu) | Select the date range you would like to include for the report. | - Custom <br> - Current Hour <br> - Today <br> - Yesterday <br> - Last 48 Hours <br> - Last 7 Days <br> - Month to Date <br> - Month to Yesterday <br> - Last Month |
| **Time Zone** (drop-down menu) | Select the time zone you would like your data to be represented in. | All 24 global time zones |
| **Type** (drop-down menu) | Select the type of report you would like to use based on the data you need. | - Platform Buyer Report (default) <br> - [Bidder Billing Report](bidder-billing-report.md) <br> - [Bidder Bid Error Report](bidder-bid-error-report-api.md) <br> - [Completed Creatives Audits Report](completed-creatives-audits-report.md) |

## Metrics

Select the **metrics** you want to be displayed in the report. Click the **Edit** button on the right to select/deselect.

| Metric | Definition |
|---|---|
| **Buyer eCPM** | The buyer's cost per impression expressed in eCPM. |
| **Buyer Spend** | The amount the buyer pays for the cost of media. |
| **Buyer Spend Buyer Currency** | The buyer's total spend in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| **Imps** (bought) | The total number of impressions bought. |
| **Measurement Rate** | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| **View-Measured Imps** | The total number of impressions that were measured for viewability. |
| **Viewability Rate** | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewable Imps / View Measured Imps) |
| **Viewable Imps** | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during one consecutive second. |

## Filters

Select the **filters** you want to be used to generate the report. Click the **Edit** button on the right to select/deselect.

| Metric | Definition |
|---|---|
| **Buyer Currency** | Select to filter by the buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| **Buyer Member** | Select to filter by the internal ID of the buyer member. |
| **Content Category** | Select to filter by content category that the inventory where the impression occurred was associated with. For more information about content categories, see the [Content Category Service](content-category-service.md). |
| **Country** | Select to filter by the country or region the impression originated from |
| **Creative** | Select to filter by ID of the creative that served on the impression where the "event" you're counting occurred. For more information about creatives, see the [Creative Service](creative-service.md). |
| **Creative Size** | Select to filter by the size of the creative. |
| **Impression Type** | Select to filter by the type of impression served. Possible values: <br> - 1 = blank <br> - 2 = PSA <br> - 3 = default error <br> - 4 = default <br> - 5 = kept <br> - 6 = resold <br> - 7 = RTB <br> - 8 = PSA resulting from a default error <br> - 9 = external impression <br> - 10 = external click |
| **Publisher** | Select to filter by internal ID of the publisher, which is one level more detailed than seller member. |
| **Seller Member** | Select to filter by internal ID of the seller member. |
| **Site** | Select to filter by site, which is a group of tags (publisher placements) |
| **Tag** | Select to filter by specific placements from a seller member. Most granular level of publisher inventory. |

## Dimensions

### Include IDs as separate column

(checkbox to the left)

Select the **dimensions** you want to be used to generate the report. Click the **check box** on the left to select/deselect. Select **Include IDs as separate column** if you would like the object ID listed as a separate column in the report.

| Metric | Description |
|---|---|
| **Buyer** | The internal member ID of the buyer member. |
| **Buyer Currency** | Buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| **Buyer Seat Code** | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression |
| **Buyer Seat Name** | The display name for the buyer seat code |
| **Content Category** | Category that the inventory where the impression occurred was associated with. For more information about content categories, see the [Content Category Service](content-category-service.md). |
| **Country** | The country or region the impression originated from |
| **Creative** | ID of the creative that served on the impression where the "event" you're counting occurred. For more information about creatives, see the [Creative Service](creative-service.md). |
| **Creative Size** | Size of the creative served |
| **Impression Type** | Type of impression served. Possible values: <br> - 1 = blank <br> - 2 = PSA <br> - 3 = default error <br> - 4 = default <br> - 5 = kept <br> - 6 = resold <br> - 7 = RTB <br> - 8 = PSA resulting from a default error <br> - 9 = external impression <br> - 10 = external click |
| **Publisher** | Internal ID of the publisher, which is one level more detailed than seller member |
| **Seller Member** | Internal ID and name of the seller member. |
| **Supply Type** | The type of supply impressions are originating from. Possible values: <br> - 0=web <br> - 1=mobile web <br> - 2=mobile app |
| **Tag** | Specific placements from a seller member. Most granular level of publisher inventory. |

## Delivery

This section determines how the report will be delivered to you as well as any reports you would like to save.

### Options on how to run the report

(Select one of the options)

| Option | Description |
|---|---|
| **Run now, show results in screen** | This will display the report in the **View Report** tab of the report screen. Recommended delivery format for reports with less dimensions and/or metrics. |
| **Run in background, notify me when results are ready to view** | Report will run in the background and a pop-up will notify you when the report is complete. Access complete report from the **Your Reports** tab. Recommended delivery format for reports with less dimensions and/or metrics. |
| **Export, send results via email** | Report will be sent to the email included in the text box. Use the **drop down option** to select the format of the file to be sent via email. Recommended delivery format for larger reports with lots of dimensions and/or metrics. |

### Options to save the report

(Select both or one of the options)

| Option | Description |
|---|---|
| **Add to scheduled reports** | If there is a report that you want every day, week, or month: <br> - Configure what you want that report to look like. <br> - Click **Add to scheduled reports**. |
| **Save as report template** | This allows you to configure different types of templates of reports that you plan on running frequently, or slightly modifying. <br> Enter the name of the report in the **Report Name** text box. |

## Run report

After your selections are made, click **Run Report** to run the report. The **View Report** screen will automatically be accessed, where the report results are displayed.

## Related topics

- [Reporting Screen](reporting-screen.md)
- [Bidder Billing Report](bidder-billing-report.md)
- [Bidder Bid Error Report](bidder-bid-error-report.md)
- [Completed Creatives Audits Report](completed-creatives-audits-report.md)
- [Your Reports](your-reports.md)
