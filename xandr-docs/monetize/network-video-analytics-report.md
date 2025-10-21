---
title: Network Video Analytics Report
description: Explore the Network Video Analytics report, revealing video event metrics across buyers and sellers for network members.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Network video analytics report

The Network Video Analytics report can be used to view video event metrics across multiple buyers and sellers for a network member.

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

### Data retention period

Data in this report has the following retention period:

- Hourly retention: 100 days
- Daily retention: 500 days

**Currency 2.0**

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Buyer | Yes | The buyer of this impression. |
| Seller | Yes | The seller of this impression. |
| Advertiser | Yes | The advertiser whose creative served on this impression. |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, the ID will be `0`.|
| Placement | Yes | The placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Insertion Order | Yes | The insertion order under which this impression was purchased. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Campaign | Yes | The campaign which purchased this impression. (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Brand | Yes | The brand associated with the creative. Microsoft Advertising keeps a list of advertiser brands in our systems that can be applied to a creative when it's uploaded. For impression type "`Resold`", no information is available in the Brand field for this report. |
| Country | Yes | The country in which the impression took place. |
| Creative | Yes | The creative served for the impression. |
| Creative Recency | Yes | How recently the creative was viewed by the user. For more information, see the [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md). |
| Creative Frequency | Yes | How many times the creative has been viewed by the user. For more information, see [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md) page. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Deal Code | Yes | The custom code for the deal. For deals with external supply partners, this is typically the string used to identify the deal.|
| IO: Trafficker (reporting label) | Yes | The trafficker associated with this insertion order. This is an insertion order reporting label. |
| IO: Sales Rep (reporting label) | Yes | The sales rep associated with this insertion order. This is an insertion order reporting label. |
| Is Takeover |Yes| Indicates whether an impression was `Blanked` or `Defaulted` due to at least one ad in the multi-ad request being a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|
| Site Domain | Yes | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: "`deals.unknown`" or "`managed.unknown`". These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| Application ID | No | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| Impression Type | Yes | See **[Impression Types](network-video-analytics-report.md#impression-types)** below for definitions of the different types of impressions. |
| Supply Type | Yes | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are '`web`', '`mobile_app`', and '`mobile_web`'. |
| Video Context | Yes | When and where the video creative was served. Possible values are `Pre-roll`, `Mid-roll`, `Post-roll`, `Outstream`, and `Unknown`. |
| Video Playback Method | Yes | The playback method for the creative, e.g, 'auto-start, sound on'. |
| Video Player Size | Yes | The size of the player based on pixel width, e.g., '`small`', '`medium`', '`large`'. |
| Bidder | No | The name of a would-be buyer that submitted a bid on the impression. |
| Call Type | No | The type of handler that was used to send the impression to Microsoft Advertising (e.g., ttj, `ut`, `mob`, `ptv`, `openrtb`). |
| Creative Duration | No | The duration of the video creative in seconds. |
| Device Type | Yes | The type of device where the creative was set to play. Options include Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles, Media Players, Set Top Box, and Other Devices. |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. This dimension is available only when Currency 2.0 is disabled. |
| Selling Currency | No | The transaction currency used by the seller to sell this impression. This dimension is available only when Currency 2.0 is disabled. |
| Clearing Event | Yes | The underlying auction event that was transacted (e.g., impression, viewable impression, completed video). |
| Video Content Duration | No | The length of the video content in seconds. |
| Video Content Genre | No | The main genre of the program in which the ad will be played. For example, Action, Adventure, Biography, Business, Comedy, etc. |
| Video Content Language | No | The language of the video program in which ad will be played. For example, Spanish. |
| Video Content Network | No | The network delivering the video content. For example, 9 Story, CBC, Disney, AMC, Fox, etc. |
| Video Content Rating | No | The publisher-identified audience group for which the content is rated. For example, All, Children (7+) , Teens (13+), Young Adults (14+), or Adults (18+). |
| Video Delivery Type | No | The type of streaming content delivery. For example, Video On Demand (VOD) and Live. |
| Video Program Type | No | The higher level categorization of the video program's format on which the ad will be played. For example, Movie, Series, Special, Show, Event, Clip, etc. |
| Code 1 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers.|
| Code 2 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| Code 3 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |

> [!NOTE]
> The data for this dimension is only available if the publisher has implemented video taxonomy.
> [!NOTE]
> In addition, you can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions. For video ads, an impression takes place when the first frame of the video is loaded. |
| Imps (default) | The number of default creatives served because there were no valid bids. |
| Imps (default error) | The number of default creatives served due to a timeout issue. |
| Imps (kept) | The number of impressions where a managed advertiser's creative served on a managed publisher's site. |
| Imps (PSA) | The number of impressions that showed PSAs (Public Service Announcements). PSAs are served only if there is no other creative to serve. |
| Imps (resold) | The number of impressions that were resold to a third-party buyer. |
| Imps (RTB) | The number of creatives served on third-party inventory. |
| Imps (blank) | The number of blank creatives served. Blanks can be served when no default creative or PSA is specified in the tag. |
| Video Imps Blank | The number of blank video creatives served. Blanks can be served when no default creative or PSA is specified in the tag. |
| Clicks | The total number of clicks. |
| CTR | The click-through rate, or the ratio of clicks to impressions, expressed as a percentage. (clicks/impressions) |
| Total Conversions | The total number of post-view and post-click conversions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage (conversions/impressions) |
| Revenue | The total revenue; the sum of booked and resold revenue. |
| Revenue per Video Complete (RPVC) | The revenue per video completion. |
| Total RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. |
| Total Network RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. |
| Cost | The total media cost across direct publishers and RTB inventory. |
| Cost per Video Complete (CPVC) | The cost per video completion. |
| Profit | Booked revenue minus total cost |
| CPM | The total media cost per 1000 impressions. |
| Profit | The total Network revenue minus cost |
| PPM | **Deprecated**. The total profit per 1000 impressions. |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that 50% of the pixels of a creative are in view during 1 consecutive second. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Custom Viewable Imps | The number of measured impressions that were viewable, per the member-level custom definition configuration. For more details, contact your Microsoft Advertising account representative. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (view-measured impressions/total impressions) |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (viewed impressions/view-measured impressions) |
| Custom Viewability Rate | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability. |
| Completion Rate | The ratio of video completions to impressions, expressed as a percentage. (video completions/total impressions) |
| Render Rate | The percentage of videos delivered based on the response rate from buyers (impressions/ad responses). For video ads, an impression takes place when the first frame of the video is loaded. |
| Response Rate | The percentage of videos served to the video player (ad responses/ad requests) |
| Ad Requests | The number of times the player initiated a request for video ad content. |
| Skip Rate | The percentage of times the user opted to skip the video. |
| Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Error Rate | The percentage of videos that generated an error. |
| 25% Complete | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Complete | The total number of times the video completed 50% of the entire duration. |
| 75% Complete | The total number of times the video completed 75% of the entire duration. |
| Companion Ad Clicks | The total number of times someone clicked on an ad adjacent to the video. |
| Companion Ad Responses | The total number of companion ads served adjacent to the video. |
| Ad Responses | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| 100% Complete | The total number of times the video played for the entire duration. |
| Errors | The total number of times an error occurred. |
| Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Fill Rate | The percentage of video impressions delivered out of the total number of video ad requests received. (total impressions/total requests) |
| Clearing Event Booked Revenue Per Event | The total booked revenue per clearing event. |
| Clearing Events Booked Revenue CPM | The booked revenue per 1000 events. |
| Booked Revenue vCPM | The booked revenue, expressed as a viewable CPM. |
| Media Cost vCPM | The media cost, expressed as a viewable CPM. |
| Clearing Event Buyer Media Cost Per Event | The media cost per clearing event. |
| Clearing Event Buyer Media Cost eCPM | The media cost per 1000 events. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Profit eCPM | Profit per thousand impressions. |
| Profit eCPC | Profit per click. |
| Profit eCPA | Profit per conversion. |
| Profit Margin | Buyer profit margin. |
| Network Profit | The sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPM | Network profit per thousand impressions. |
| Network Profit eCPC | Network profit per click. |
| Network Profit eCPA | Network profit per conversion. |
| Network Profit Margin | Network profit margin. |
| Video Content Duration | The length of the video content in seconds. |
| Average View Time | An estimate for the average duration in seconds (rounded to `0` decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| Average View Time Percent | The average view time expressed as a percentage of the total possible view time. |

> [!NOTE]
> The data for Video Content Duration metric is only available if the publisher has implemented video taxonomy.

## Impression types

| Value | Name | Definition |
|---|---|---|
| 1 | Blank | No creative served. |
| 2 | PSA | A public service announcement served because no other creative was eligible. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 4 | Default | A default creative served because no line item or campaign bid or no other creative was eligible. |
| 5 | Kept | One of your managed advertisers served a creative. |
| 6 | Resold | The impression was sold to a third-party buyer. |
| 7 | RTB | Your creative served on third-party inventory. |
| 8 | PSA Error | A public service announcement served due to a timeout issue. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |

## To run Your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   1. Or, from the Publishers top menu, click on **Prebid Server Premium \> Analytics \> Prebid Server Analytics**.
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
