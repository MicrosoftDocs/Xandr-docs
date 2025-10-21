---
title: Microsoft Monetize - Seller Site Domain Report
description: This page is an overview on Seller Site Domain Report. Learn how you can use this report to see what kind of web or mobile app inventory is coming through a publisher, guarantee inventory quality and understand business impact.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Seller site domain report

The **Seller Site Domain** report is designed to give sellers information about what kind of web and mobile app inventory is coming through a publisher. For example, as a seller, you might distribute placement tags to your publishers and then want to verify that those tags are running on the inventory you intended. In addition, this report allows you to:

- See what kind of web or mobile app inventory is coming through a publisher so you can understand how to value it
- Guarantee a certain degree of inventory quality to managed buyers
- Optimize on domains or mobile application ID for managed campaigns
- Understand the business impact of Microsoft Advertising audit and categorization

**Available to Members and Publishers:** This page describes both the member-level version **and** the publisher version; they are essentially the same.

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

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Name | Description |
|--|--|
| Age | The age of the user associated with the impression. For impressions older than 100 days, the age will be "unknown". |
| Audit Type | The type of audit performed on the domain where the impression occurred. Possible values:<br> - `"By Seller"`: The domain was self-audited.<br> - `"By AppNexus"`: The domain was audited by AppNexus.<br> - `"By Seller & AppNexus"`: The domain was audited by both the seller and AppNexus.<br> - `"Unknown Audit Type"`: This usually means that the domain is unaudited. In some cases, this means that the domain was not auditable for technical reasons. |
| Content Category | The name and ID of the universal content category associated with this site or placement. For more information about content categories, see [Content Categories](content-categories.md). |
| Domains Exposed | Whether this inventory's domains are exposed for targeting by buyers. Possible values:<br> - `"Exposed"`<br> - `"Not exposed"` |
| Exposed for Resale | Whether this inventory is exposed for resale. Possible values:<br> - `"Exposed"`<br> - `"Not Exposed"` |
| Filtered Request Reason | The reason the ad request was filtered out by Microsoft Advertising prior to bidding. |
| Fold Position | The fold position of the impression (i.e., where on the page the placement is located).<br>Possible values for non-Facebook impressions:<br> - unknown<br> - above<br> - below<br>Possible values for Facebook impressions:<br> - Top FB Ad Slot<br> - 2nd FB Ad Slot<br> - 3rd FB Ad Slot<br> - 4th FB Ad Slot<br> - 5th FB Ad Slot<br> - 6th FB Ad Slot<br> - 7th FB Ad Slot<br> - 8th FB Ad Slot<br> - 9th FB Ad Slot<br> - 10th FB Ad Slot |
| Gender | The gender of the user. For impressions older than 100 days, the gender will be "unknown". |
| Impression Type | The type of impression that occurred. Possible impression types:<br> - `"PSA (2)"`: The auction ended in default due to a lack of bids, or there may not have been any bids that met the seller's reserve price. No default creative was assigned to the placement, and a PSA was served.<br> - `"Default Error (3)"`: The auction ended in default due to a technical error, and the placement's default creative was served.<br> - `"Default (4)"`: The auction ended in default due to a lack of bids, or there may not have been any bids that met the seller's reserve price. A default creative was served.<br> - `"Kept (5)"`: The auction ended with a managed buyer winning.<br> - `"Resold (6)"`: The auction ended with an external buyer winning.<br> - `"PSA Error (8)"`: The auction ended in default due to a technical error. No default creative was assigned to the placement, and a PSA was served. |
| Mobile Application | For mobile app impressions, the Apple App Store or Google Play name and ID of the mobile application where the impression occurred, for example, `"Angry Birds (343200656)"` or `"Angry Birds (com.rovio.angrybirds)" "---"`: This means that we didn't receive a valid mobile app name as the referrer or the app has received too few impressions to be included in reporting. |
| Operating System | The operating system of the device where the impression occurred. |
| Operating System Family | The name of the operating system family associated with the device the impression was served on (e.g., Android, Apple iOS). |
| Placement | The name and ID of the placement on which the impression occurred.<br>**Note**: A placement ID of `0` may appear for 3rd-party impression trackers. For more information about impression trackers, see [Working with Impression and Click Trackers](working-with-impression-and-click-trackers.md). |
| Placement Group | The name and ID of the placement group where the impression occurred. |
| Publisher | The name and ID of the publisher on whose site the impression occurred. |
| Remarketing Type | Indicates whether the domain is part of a remarketing segment (e.g., yes/no). |
| Site Domain | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed.<br>**Note**: In some cases, this field will be populated with a domain that is different than where the impression actually occurred, such as an ad server domain. For more information about why this happens, see [Passing Domains Across iFrames](#passing-domains-across-iframes) below. |
| Supply Type | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values:<br> - `"web"`<br> - `"mobile_app"`<br> - `"mobile_web"` |

## Filters

| Name | Description |
|--|--|
| Age | The age of the user associated with the impression. For impressions older than 100 days, the age will be "unknown". |
| Audit Type | The type of audit performed on the domain where the impression occurred. Possible values:<br> - `"By Seller"`: The domain was self-audited.<br> - `"By AppNexus"`: The domain was audited by AppNexus.<br> - `"By Seller & AppNexus"`: The domain was audited by both the seller and AppNexus.<br> - `"Unknown Audit Type"`: This usually means that the domain is unaudited. In some cases, this means that the domain was not auditable for technical reasons. |
| Content Category | The universal content category associated with this site or placement. For more information about content categories, see [Content Categories](content-categories.md). |
| Filtered Request Reason | The reason the ad request was filtered out by Microsoft Advertising prior to bidding. |
| Fold Position | The fold position of the impression (i.e., where on the page the placement is located).<br>Possible values for non-Facebook impressions:<br> - unknown<br> - above<br> - below<br>Possible values for Facebook impressions:<br> - Top FB Ad Slot<br> - 2nd FB Ad Slot<br> - 3rd FB Ad Slot<br> - 4th FB Ad Slot<br> - 5th FB Ad Slot<br> - 6th FB Ad Slot<br> - 7th FB Ad Slot<br> - 8th FB Ad Slot<br> - 9th FB Ad Slot<br> - 10th FB Ad Slot |
| Gender | The gender of the user. For impressions older than 100 days, the gender will be "unknown". |
| Impression Type | The type of impression. Possible values (associated IDs in parentheses):<br> - "Blank" (1): No creative served.<br> - "PSA" (2): A public service announcement served because no other creative was eligible.<br> - "Default Error" (3): A default creative served due to timeout issue.<br> - "Default" (4): A default creative served because no campaigns bid or no other creative was eligible.<br> - "Kept" (5): One of your managed advertisers served a creative.<br> - "Resold" (6): The impression was sold to a third-party buyer.<br> - "RTB" (7): Your creative served on third-party inventory.<br> - "PSA Default Error" (8): A public service announcement served due to timeout issue.<br> - "External Impression" (9): An impression from an impression tracker.<br> - "External Click" (10): A click from a click tracker.<br> - "Insertion" (11): Your creative served on third-party inventory where it persists across page-loads and sessions. Note: This impression type is currently only for Facebook News Feed creatives. |
| Minimum Impression | Rows with less than this number of impressions will be excluded from the report. |
| Operating System | The operating system of the device where the impression occurred. |
| Operating System Family | The name of the operating system family associated with the device the impression was served on (e.g., Android, Apple iOS). |
| Placement | The placement on which the impression occurred. |
| Placement Group | The placement group where the impression occurred. |
| Publisher | The publisher on whose site the impression occurred. |
| Seller ID | The ID of the seller member associated with the site domain. |
| Seller Name | The name of the seller member associated with the site domain. |
| Supply Type | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values:<br> - `"web"<br>` <br> - `"mobile_app"`<br> - `"mobile_web"` |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Clicks | The number of clicks coming through this site or placement. |
| Filtered Request | The total number of impressions which have been filtered out by Microsoft Advertising Inventory Quality (e.g. from a blocklisted domain, IP, etc.). |
| Imps | The number of impressions coming through this site or placement. |
| Network Revenue | The amount of network revenue running through this site or placement. This is the revenue coming into the network, booked through direct advertisers and resold to real time buyers. |
| Publisher Revenue | The amount of publisher revenue running through this site or placement. This is the revenue paid out to the publisher (on a Revshare or CPM basis). |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |

## Passing domains across iFrames

Serving ads inside of iFrames is preferred by publishers for a number of reasons, to include:

- Increased Security: For security reasons, communication between iFrames serving from different domains is prohibited by the browser. This is known as the "Same Origin Policy". For more information, see the W3C's [Same Origin Policy](https://www.w3.org/Security/wiki/Same_Origin_Policy) page.
- Page Load Speed: Page load speed is guaranteed to be unaffected by advertisements inside iFrames because iFrames allow asynchronous loading of both page content and advertisements. This ensures that the user does not have to wait for the rest of the page to load in the event that serving an advertisement happens more slowly than expected.

For these and other reasons, some networks provide their publishers with an iFrame in which to display advertisements. If this iFrame delivers its contents from the network's domain and not the publisher's, it can lead to difficulties in determining the domain on which an impression actually occurred.

For example, a publisher is given a snippet of HTML code to put on their pages that includes an iFrame referencing a network's domain, `best-network.net`:

``` 
            <!-- Publisher's Web Page -->
            <iframe src="http://best-network.net"> 
            <!-- iFrame Referencing Network Domain --> 
            <script src="http://cooladexchange.net/tag?id=12345">
            </script>
            <!-- Ad Exchange Placement serving on Network Domain --> 
            </iframe> 
         
```

The iFrame is located on the publisher's web page, but it is serving its contents from the network's domain. Because the page and the iFrame are hosted on different domains, the security restrictions of the "Same Origin Policy" apply, and communication between the publisher's page and the network's iFrame is forbidden. Therefore the network is unable to determine the actual domain of the publisher's page. As a result, the network passes along its own domain as the referring URL to the placement.

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured), or, from the Publishers top menu, click on **Prebid Server Premium** \>**Analytics** \> **Prebid Server Analytics**.
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
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Network Reporting](network-reporting.md)
- [Network Site Domain Performance Report](network-site-domain-performance-report.md)
- [Network Analytics Report](network-analytics-report.md)
