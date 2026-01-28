---
title: Microsoft Curate - Curator Analytics Report
description: Explore this article to understand the Curator Analytics report, including its metrics, dimensions, and a detailed guide on running a report.
ms.date: 1/28/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Curator Analytics report

> [!IMPORTANT]
> This report is only available to curators.

The **Curator Analytics Report** provides curators insight into how money is flowing from demand to supply within their curated marketplace.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports.

However, all time ranges are not available for every report.

- Custom
- Current Hour
- Last Available Day
- Last Hour
- Today
- Last 24 Hours
- Last 48 Hours
- Yesterday
- Last 2 Days
- Last 7 Days
- Last 7 Available Days
- Last 14 Days
- Last 14 Available Days
- Last 30 Days
- Last 30 Available Days
- Last Month
- Last 100 Days
- Last 365 Days
- Quarter to Date
- Month to Date
- Month to Yesterday
- Lifetime

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

## Data retention period

Data retention period for this report is 1100 days.

## Dimensions

> [!IMPORTANT]
> The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.
>
> For all revenue fields, the currency is defined by the **Buying Currency** field.

| Column | Filter? | Description |
|:---|:---|:---|
| Curated Advertiser | No | Advertiser name/ID of the curator member object that owns the deal line item associated with the curated deal. |
| Curated Deal Insertion Order | Yes | Insertion Order name/ID of the curator member object that owns the deal line item associated with the curated deal. |
| Curated Deal | Yes | Curated deal name/ID. |
| Curated Deal Line Item | Yes | Line Item name/ID of the curator member object that owns the deal line item associated with the curated deal. |
| Curated Deal Advertiser Id | No | The advertiser ID of the advertiser whose creative served on this impression. |
| Member Currency | No | The currency associated with the curator member's seat. |
| Billing Currency | No | The currency that Microsoft Advertising bills the curator in. |
| Bidder | No | Name/ID of the bidder who bought on the transaction. |
| Buyer | Yes | Member name/ID of the buyer who bought on the transaction. |
| Brand | Yes | Brand name/ID associated with the creative that served on the curated deal. |
| Seller | Yes | Member name/ID of the seller where the curated transaction served on. |
| Publisher | Yes | Publisher name/ID of the seller where the curated transaction served on. |
| Placement Group | Yes | Placement Group name/ID of the seller where the curated transaction served on. |
| Placement | Yes | Placement name/ID of the seller where the curated transaction served on. |
| Seller Deal | No | The seller deal name/ID being included in a curated deal.<br><br>**Note:** If applicable, since not all curated deals will include a seller. |
| Size | Yes | The size of the creative (e.g., 320x50). |
| Country | Yes | The country or region in which the impression took place. For impression requests for which Microsoft Advertising received no indication that the ad was rendered (i.e., non-transacted), country or region information is not provided. |
| Site Domain | No | Site Domain/App where the curated transaction served on. |
| Mobile Application | No | The mobile application associated with the creative that served on this impression. |
| Media Type | No | The media type associated with the creative that served on this impression. |
| Device Type | Yes | The device type associated with the creative that served on this impression. |
| Video Context | Yes | When and where the video ad plays: pre-roll, mid-roll, post-roll, outstream. |
| Curator Margin Type | Yes | Margin type (if a curator has a margin associated to the line item). Possible values: percent, fixed, or null. |

## Metrics

When values of a metric are displayed as percentages in the UI, they will appear as decimals when you export the report.

Select metrics are available for impressions bought through Microsoft Invest, while video metrics are available for impressions bought through any DSP.

| Column | Description |
|:---|:---|
| Imps | Delivered impressions |
| Viewed Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| View Measurable Imps | The total number of impressions that were measured for viewability. |
| Curator Revenue | The amount of spend a buyer sends to the curator, net of buyer fees, if applicable. This is the same as buyer media cost, exclusive of buyer rev share (BASC). |
| Curator Tech Fees | The fees Microsoft Advertising charges to a curator on a transaction. |
| Curator Net Media Cost | The amount of spend a curator sends to exchange sellers, net of curator fees and margins, if applicable. This is the same as gross seller revenue, inclusive of seller rev share (SASC). |
| Curator Margin | The profit a curator makes on a transaction.<br><br>**Note:** When taken as a percentage, Curator Margin is calculated based on Curator Revenue. |
| Curator Total Cost | The amount of spend a curator sends to the exchange and exchange sellers, net of curator margin but gross of curator fees. |
| Clicks | The total number of clicks across all impressions. For Invest DSP, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| CTR % | The proportion of Clicks versus Imps. |
| Buyer CPC | Curator Revenue divided by Clicks. |
| Video Errors | The total number of times an error occurred. |
| Video Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Video Start Rate % | The proportion of Video Starts versus Imps. |
| Video Skips | The total number of times a user skipped the video. |
| Video Skip Rate % | The proportion of Video Skips versus Imps. |
| Video 25% Complete | The total number of times the video completed 25% of the entire duration. |
| Video 50% Complete | The total number of times the video completed 50% of the entire duration. |
| Video 75% Complete | The total number of times the video completed 75% of the entire duration. |
| Video Completions | The total number of times the video played for the entire duration. |
| Video Completion Rate % | The proportion of Video Completions versus Imps. |
| Buyer Cost Per Video Complete | Curator Revenue divided by Video Completions. |
| Buyer CPM | Curator Revenue divided by Imps, expressed as a CPM. If a **Fixed Price** curated deal sources impressions from a seller using second-price auctions, the curated deal’s clearing price may be lower than the configured fixed price. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, Select **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery
    method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your
      browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report
      when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to
      view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name
      this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Select **Run report** to send your report request.
