---
title: Microsoft Invest - Seller Detected Site Domain Report
description: The Seller Detected Site Domain report provides visibility into the actual domains that are being sold, and provides a tag or publisher level health-check.
ms.date: 10/28/2023
---

# Microsoft Invest - Seller Detected Site Domain report

> [!NOTE]
> This report was deprecated in 2021.

The **Seller Detected Site Domain** report is designed to provide visibility into the actual domains that are being sold, and provide a tag or publisher level "health-check". Giving sellers visibility into the actual domains provides deeper insight into the inventory that is coming into their network. The detected domains, however, do not have any impact on the auction itself.

The report is best utilized as an investigation tool. That is, a seller runs the report for specific tags or publishers that they want to dig into further. The seller may know off-hand what they want to investigate; for example, it could be a new publisher that they've signed up. But, it would be very useful to give them an easy way to identify potential problems in tags or publishers.

In addition, sellers mostly cares about the tags or publishers that are giving them the most revenue - there may be a long tail that is not worth the time to investigate. So, a seller runs this report to see their best performing tags or publishers as well as whether a tag or publisher is problematic.

<!-- **Available to Members and Publishers** -->

This page describes both the **member-level** and the **publisher** version; they are essentially the same.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports. However, all time ranges are not available for every report.

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

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|:---|:---|
| Imps | The number of impressions coming through this site or placement. |

## Filters

| Name | Description |
|:---|:---|
| Publisher | The publisher on whose site the impression occurred. |
| Placement Group | The placement group where the impression occurred. |
| Placement | The placement on which the impression occurred. |
| Blocked Inventory | Specify if the impression is in a blocklist. |
| Minimum Impression | Rows with less than this number of impressions will be excluded from the report. |

## Dimensions

| Name | Description |
|:---|:---|
| Site Domain | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. <br><br> **Note**: In some cases, this field will be populated with a domain that is different than where the impression actually occurred, such as an ad server domain. For more information about why this happens, see [Passing Domains Across iFrames](#passing-domains-across-iframes) below. |
| Publisher | The name and ID of the publisher on whose site the impression occurred. |
| Placement Group | The name and ID of the placement group where the impression occurred. |
| Placement | The name and ID of the placement on which the impression occurred.<br> Note that a placement ID of 0 may appear for 3rd-party impression trackers. For more information about impression trackers, see [Working with Impression and Click Trackers](./working-with-impression-and-click-trackers.md). |
| Site Domain Audit Status | Specifies the audit status of the auctioned site domain. Permissible values are Audited, Blocklisted, AdServer, Unauditable, Pending, and Unaudited. |
| Detected Site Domain | The actual domains that are being sold and where the impression actually occured. |
| Detected Site Domain Audit Status | Specifies the audit status of the detected site domain .Permissible values are Audited, Blocklisted, AdServer, Unauditable, Pending, and Unaudited. |
| Blocked Inventory | Specifies if the impression is in a blocklist. |

## Pass domains across iFrames

Serving ads inside of iFrames is preferred by publishers for a number of reasons, to include:

- **Increased Security**: For security reasons, communication between iFrames serving from different domains is prohibited by the browser. This is known as the "Same Origin Policy". For more information, see the W3C's [Same Origin Policy](http://www.w3.org/Security/wiki/) page.
- **Page Load Speed**: Page load speed is guaranteed to be unaffected by advertisements inside iFrames because iFrames allow asynchronous loading of both page content and advertisements. This ensures that the user does not have to wait for the rest of the page to load in the event that serving an advertisement happens more slowly than expected.

For these and other reasons, some networks provide their publishers with an iFrame in which to display advertisements. If this iFrame delivers its contents from the network's domain and not the publisher's, it can lead to difficulties in determining the domain on which an impression actually occurred.

For example, a publisher is given a snippet of HTML code to put on their pages that includes an iFrame referencing a network's domain, `best-network.net`:

```
<!-- Publisher's Web Page --> <iframe src="http://best-network.net"> <!-- iFrame Referencing Network Domain --> <script src="http://cooladexchange.net/tag?id=12345"></script> <!-- Ad Exchange Placement serving on Network Domain --> </iframe> 
```

The iFrame is located on the publisher's web page, but it is serving its contents from the network's domain. Because the page and the iFrame are hosted on different domains, the security restrictions of the "Same Origin Policy" apply, and communication between the publisher's page and the network's iFrame is forbidden. Therefore the network is unable to determine the actual domain of the publisher's page. As a result, the network passes along its own domain as the referring URL to the placement.

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   <br>Or<br>
   From the Publishers top menu, select **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**.

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.
   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](./dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.
    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:

    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.

    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.
        > [!TIP]
        > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
  
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
  
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.

    - **Name this report**: Give this report with its current settings a name for future reference.

1. Select **Run report** to send your report request.

## Related topics

- [Member Reporting](./network-reporting.md)
- [Member Site Domain Performance Report](./network-site-domain-performance-report.md)
- [Member Analytics Report](./network-analytics-report.md)
