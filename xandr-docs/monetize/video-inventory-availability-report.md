---
title: Microsoft Monetize - Video Inventory Availability Report
description: Learn how buyers can use the Video Inventory Availability Report to know whether an inventory, that meets their specific requirement, is available for buying. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Video inventory availability report

Buyers can use the Video Inventory Availability report to determine whether inventory that meets their specific buying requirements is likely to be available for purchase. While most of the data in the report is historical and may not accurately reflect today's available inventory, reviewing recent availability is a good way to predict the success of inventory targeting in the future. To access this report, go to **Network** \> **Inventory** \> **Reporting** and select **Video Inventory Availability** from the **Type** dropdown. For more information on the available data fields and their definitions, see **Dimensions** and **Metrics** below.

## Navigation

1. Go to **Reporting** > **Report Center** and click **Create New**
2. In **Search for a Report** search box, type the report name
3. The relevant report widget will be shown under its category such as **Analytics**, **Troubleshooting** or **Reach**.
4. Click on **Create new report** button to create the new report.
   
## Time frame

All dates and times are given in UTC.

**Time ranges**

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

**Intervals**

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Ad Request Call Type | No | The type of handler that was used to send the impression to Microsoft Advertising (e.g., `vmap`, `ut`, `mob`, `ptv`, `openrtb`). |
| Application Id | Yes | For mobile app inventory, the ID of the app that will host the placement. |
| Content Category | Yes | The content category associated with the inventory where these impressions occurred, for example Business & Industry. |
| Country | Yes | The country in which the impression took place. |
| Device Type | Yes | The type of hardware device that will deliver the ad, for example a desktop computer or a game console. |
| Inventory Type | Yes | The type of Managed, Programmatic, or Deals. |
| Maximum Ad Duration | No | Specifies the maximum duration of the video placement. |
| Maximum VAST version | Yes | Filter only. Sets the maximum publisher player VAST version for inventory to be included in the report. |
| Min/Max Completion Rate | Yes | Filter only. Sets the threshold for the video completion rate of inventory to be included in the report. |
| Min/Max CTR | Yes | Filter only. Sets the threshold for the clickthrough rate of inventory to be included in the report. |
| Min/Max Viewability Rate | Yes | Filter only. Sets the viewability threshold of inventory to be included in the report. |
| Minimum Ad Duration | No | Specifies the minimum duration of the video placement. |
| Seller | No | The seller of the inventory. |
| Seller Group | Yes | The group of sellers the seller belongs to. |
| Seller Type | Yes | Microsoft Advertising buckets sellers into different types for billing purposes. For example, publisher, intermediary or both. |
| Site Domain | Yes | For web video inventory, the domain of the site where the inventory is available. |
| Skippability Support | Yes | Whether the publisher player was set to honor the Skip setting in the VAST document. |
| Supply Type | Yes | The supply type for the impression – Web, Mobile Web, or Mobile App. |
| VAST Version Support | No | The version of VAST supported by the publisher player. |
| Video Context | Yes | When and where the video ad plays – pre-roll, mid-roll, post-roll, or outstream. |
| Video Playback Method | Yes | The playback method for the creative, for example 'Autoplay, Sound On'. |
| Video Player Height | Yes | The height of the player in pixels. |
| Video Player Size | Yes | The size of the player based on width in pixels: Small, Medium, Large, or Unknown. |
| Video Player Width | Yes | The width of the player in pixels. |
| VPAID Support | Yes | Whether the publisher player supported a VPAID wrapper. |

## Metrics

| Column | Description |
|--|--|
| Completion Rate | The ratio of video completions to impressions, expressed as a percentage. |
| CTR | Clickthrough rate. |
| Video Avails | The number of videos predicted to be available for purchase, based on historical data |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured), or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      >  The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
