---
title: Microsoft Invest - Advertiser Video Analytics Report
description: Use the Advertiser Video Analytics report to view video event metrics for a specific advertiser.
ms.date: 10/28/2023
---

# Microsoft Invest - Advertiser Video Analytics report

The Advertiser Video Analytics report can be used to view video event metrics for a specific advertiser. To view such metrics across multiple advertisers and publishers, use the [Member Video Analytics Report](./network-video-analytics-report.md).

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

For more information about how quickly report data is processed, see [Availability of Reporting Data](./availability-of-reporting-data.md).

### Data retention period

Data in this report is retained for 100 days.

### Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, select the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|:-|:-|:-|
| Sellers | Yes | The seller of the impression. |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement | Yes | The placement through which this impression occurred. <br> **Note**: For impressions older than 100 days, placements are aggregated into one row with `-1` as the ID and a generic name.</br> |
| Line Item | Yes | The line item under which this impression was purchased. For more information about line items, see [Working with Line Items](./working-with-line-items.md). |
| Campaign | Yes | The campaign that purchased this impression. (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Creative | Yes | The creative that served on this impression. For more information about creatives, see [Working with Creatives](./working-with-creatives.md). <br>**Note**: For impressions older than 100 days, creatives will be aggregated into one row with `0` as the ID and a generic name.</br> |
| Creative Duration | No | The duration of the video creative in seconds. |
| Country | Yes | The country/region in which the impression took place. |
| Insertion Order | Yes | The insertion order under which this impression was purchased. |
| Creative Recency | Yes | How recently the creative was viewed by the user. For more information, see [Creative Frequency and Recency Report](./creative-frequency-and-recency-report.md). |
| Creative Frequency | Yes | How many times the creative has been viewed by the user. For more information, see Creative Frequency Definitions in the [Creative Frequency and Recency Report](./creative-frequency-and-recency-report.md) page. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| IO: Trafficker (reporting label) | Yes | The trafficker associated with this insertion order. This is an insertion order reporting label; for more information, see [Working with Insertion Orders](./working-with-insertion-orders.md). |
| IO: Sales Rep (reporting label) | Yes | The sales rep associated with this insertion order. This is an insertion order reporting label; for more information, see [Working with Insertion Orders](./working-with-insertion-orders.md). |
| Site Domain | Yes | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| Application ID | No | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| Buying Currency | No | The currency used by the buyer. This dimension is available only when Currency 2.0 is disabled. |
| Clearing Event | Yes | The clearing event associated with the impression. <br> - Impressions <br> - Views - Standard Display <br> - Views - Standard Display - Moat <br> - Views - Custom Display - 100pv1s <br> - Views - Custom Display - 100pv1s - Moat <br> - Views - Standard Video <br> - Views - Custom Video - 100pv50pd|
| Supply Type | Yes | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are web, mobile_app, and mobile_web. |
| Video Context | Yes | The context of the video creative, e.g., 'pre-roll'. |
| Video Playback Method | Yes | The playback method for the creative, e.g, 'auto-start, sound on'. |
| Video Player Size | Yes | The size of the player based on pixel width, e.g., 'small', 'medium', 'large'. |
| Device Type | Yes | The type of device where the creative was set to play. Options include Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles, Media Players, Set Top Box, and Other Devices. |
| Video Content Duration | No | The length of the video content in seconds.|
| Video Content Genre | No | The main genre of the program in which the ad will be played. For example, Action, Adventure, Biography, Business, Comedy, etc.|
| Video Content Language | No | The language of the video program in which ad will be played. For example, Spanish.|
| Video Content Network | No | The network delivering the video content. For example, 9 Story, CBC, Disney, AMC, Fox, etc.|
| Video Content Rating | No | The publisher-identified audience group for which the content is rated. For example, All, Children (7+) , Teens (13+), Young Adults (14+), or Adults (18+).|
| Video Delivery Type | No | The type of streaming content delivery. For example, Video On Demand (VOD) and Live.|
| Video Program Type | No | The higher level categorization of the video program's format on which the ad will be played. For example, Movie, Series, Special, Show, Event, Clip, etc.|

> [!NOTE]
>
> - You can also filter on a particular number of impressions using the **Minimum Impressions** filter.
> - The data for the following video related dimensions are only available if the publisher has implemented video taxonomy:
>   - Video Content Duration
>   - Video Content Genre
>   - Video Content Language
>   - Video Content Network
>   - Video Content Rating
>   - Video Delivery Type
>   - Video Program Type

## Metrics

| Column | Description |
|:--|:--|
| Imps | The total number of impressions. |
| Clicks | The total number of clicks. |
| Clearing Event Booked Revenue Per Event | The booked revenue per event. |
| Clearing Events Booked Revenue CPM | The booked revenue in CPM per event. |
| Booked Revenue vCPM | The booked revenue expressed in terms of viewable CPM. |
| Media Cost vCPM | The media cost expressed in terms of viewable CPM. |
| Profit Margin | The average profit margin. |
| Clearing Event Buyer Media Cost Per Event | The Buyer's media cost per clearing event. |
| Clearing Event Buyer Media Cost eCPM | The Buyer's media cost in CPM per clearing event. |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Total Convs | The total number of post-view and post-click conversions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Revenue | The total revenue; the sum of booked and resold revenue. |
| Revenue eCPM | The total revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPC | The total revenue, expressed as eCPC. For definitions of eCPM and other terms, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPA | The revenue per conversion or acquisition, expressed as eCPA. For the definition of eCPA, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Cost eCPM | The cost per thousand impressions. |
| Cost | The total media cost across direct publishers and RTB inventory. |
| Cost eCPC | The cost per click. |
| Cost eCPA | The cost per acquisition (conversion). |
| Profit | Booked revenue minus total cost. |
| Profit eCPM | The profit per thousand impressions. Here, profit is defined as booked revenue minus total cost. |
| Profit Margin | Profit divided by booked revenue. Here, profit is defined as booked revenue minus total cost. |
| Post View Conversion Rate | The ratio of post-view conversions to impressions. |
| Post Click Conversion Rate | The ratio of post-click conversions to impressions. |
| Errors | The total number of times an error occurred. |
| Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Skip Rate | The percentage of times the user opted to skip the video. |
| 25% Complete | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Complete | The total number of times the video completed 50% of the entire duration of time. |
| 75% Complete | The total number of times the video completed 75% of the entire duration of time. |
| 100% Complete | The total number of times the video played for the entire duration of time. |
| Completion Rate | The ratio of video completions to impressions, expressed as a percentage. |
| Revenue per Video Complete (RPVC) | The revenue per video completion. |
| Cost per Video Complete (CPVC) | The cost per video completion. |
| Ad Responses | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that 50% of the pixels of a creative are in-view during 1 consecutive second. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (viewed imps / view-measured imps) |
| Custom Viewability Rate | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability. |
| Custom Viewable Imps | The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Microsoft Advertising account representative). |
| Render Rate | The percentage of videos delivered based on the response rate from buyers. (impressions /ad responses) For video ads, an impression takes place when the first frame of the video is loaded. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Profit eCPC | Profit per click. Here, profit is defined as booked revenue minus total cost. |
| Profit eCPA | Profit per conversion. Here, profit is defined as booked revenue minus total cost. |
| Video Content Duration | The length of the video content in seconds.|
| Average View Time | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| Average View Time Percent | The average view time expressed as a percentage of the total possible view time. |

> [!NOTE]
>
> - When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.
> - The data for Video Content Duration metric are only available if the publisher has implemented video taxonomy.

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   <br>Or<br>
   From the Publishers top menu, select **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**
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

## Related topic

[Member Reporting](./network-reporting.md)
