---
title: Microsoft Invest - Device Analytics Report
description: In this article, learn about the Device Analytics report to access performance data from both the buy-side and sell-side, where impressions were delivered.
ms.date: 10/28/2023
---

# Microsoft Invest - Device Analytics report

The Device Analytics report enables you to retrieve buy-side and sell-side performance data based on devices where impressions were served. This is especially important for networks working with in-app advertisers who traffic creatives that encourage app installation and who therefore want confirmation that their creatives are targeting devices compatible with their apps. It also helps you answer the following questions:

- How many impressions have you seen for specific device makes and models?
- How many impressions have you seen for specific connection types (i.e., WiFi/Static or Carrier-based)?
- How do certain types of devices perform relative to others (i.e., tablets vs. phones)?
- How do certain makes and models of devices perform relative to others (i.e., Android vs. Apple)?
- How do certain types of connections perform relative to others (i.e., Wifi/Static vs. Carrier-based)?

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

Most data in this report is maintained for 14 months. However, after 100 days, you are no longer able to report on hourly data (daily, monthly and cumulative intervals are still available).

> [!NOTE]
> The first hour for which hourly reporting is supported is **2019-06-03 00:00 UTC**.

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, select the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| Buyer | string | Yes | "My Member (123)" | The name of the buying member followed by the ID (Microsoft Advertising format). |
| Seller | string | Yes | "That Seller (456)" | The name of the selling member followed by the ID (Microsoft Advertising format). |
| Advertiser | string | Yes | "Mobile Zombies (789)" | The name of the advertiser followed by the ID (Microsoft Advertising format). |
| Publisher | string | Yes | "Undead.com (456)" | The name of the publisher followed by the ID (Microsoft Advertising format). |
| Insertion Order | string | Yes | "Mobile Insertion Order (321)" | The name of the insertion order followed by the ID (Microsoft Advertising format). |
| Line Item | string | Yes | "Mobile Line Item (111)" | The name of the line item followed by the ID (Microsoft Advertising format). |
| Campaign | string | Yes | "Mobile Campaign (222)" | The name of the campaign followed by the ID (Microsoft Advertising format). (Does not apply to all advertisers.) |
| Split | string | Yes | "Mobile Split A (342)" | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Deal ID | string | Yes | "My New Deal" | The ID/name of the deal associated with the transaction for the impression. |
| Media Type | string | Yes | "Banner" | The media type of the creative. Possible values: "Banner", "Pop", "Interstitial", "Video", "Text", "Expandable", "Skin", or "Facebook". |
| Country | string | Yes | "US" | The code for the country/region. |
| Size | string | Yes | "728x90" | The size of the creative served. |
| Bid Type | string | Yes | "Manual" | The optimization phase the node was in when it bid for the impression. Note that the term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". <br>Allowed values:<br> - "Manual": Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - "Learn": Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - "Optimized": Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - "Unknown": The node was in an unknown optimization phase.<br> - "Optimized give up"<br> - "Learn give up"<br> - "Manual give up" |
| Impression Type | string | Yes | "Resold" | The type of impression. Possible values (associated IDs in parentheses):<br> - "Blank" (1): No creative served.<br> - "PSA" (2): A public service announcement served because no other creative was eligible.<br> - "Default Error" (3): A default creative served due to timeout issue.<br> - "Default" (4): A default creative served because no campaigns bid or no other creative was eligible.<br> - "Kept" (5): One of your managed advertisers served a creative.<br> - "Resold" (6): The impression was sold to a third-party buyer.<br> - "RTB" (7): Your creative served on third-party inventory.<br> - "PSA Default Error" (8): A public service announcement served due to timeout issue.<br> - "External Impression" (9): An impression from an impression tracker.<br> - "External Click" (10): A click from a click tracker.<br> - "Insertion" (11): Your creative served on third-party inventory where it persists across page-loads and sessions.<br>**Note:**<br>The "Insertion" impression type is currently only for Facebook News Feed creatives. |
| Payment Rule | string | Yes | "Homepage Rule (993)" | The name of the payment rule followed by the ID. |
| Revenue Type | string | Yes | "CPA" | The basis on which the advertiser pays the member. |
| Payment Type | string | Yes | "cpm", "revshare" | The type of payment to a broker. |
| Device Type | string | No | desktops & laptops | The type of device on which the impression was served. |
| Connection Type | string | Yes | "Carrier-based" | The type of internet connection at the time of the impression. Possible values: "Carrier-based" or "Wifi or Static". |
| Device Make | string | Yes | "4G Systems (1)" | The name of the device make followed by the ID (Microsoft Advertising format). |
| Device Model | string | Yes | "DX650 (15)" | The name of the device model followed by the ID (Microsoft Advertising format). |
| Operating System | string | Yes | "Android 6.0.1 Marshmallow (155)" | The name of the operating system of the device followed by the ID (Microsoft Advertising format). |
| Operating System Family | string | Yes | "Android (2)" | The name of the operating system family (e.g., Android, Microsoft Windows) of the device followed by the ID (Microsoft Advertising format). |
| Browser | string | Yes |  | The name of the browser followed by the ID (Microsoft Advertising format). |
| Buying Currency | string | No | "EUR" | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the monetary metrics to be displayed in the buying currency. This dimension is available only when Currency 2.0 is disabled. |
| Selling Currency | string | No | "EUR" | The transaction currency used by the seller to sell this impression. Including this dimension will cause the monetary metrics to be displayed in the selling currency. This dimension is available only when Currency 2.0 is disabled. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| Imps | int | 2340 | imps | The total number of impressions (served and resold). |
| Clicks | int | 1 | clicks | The total number of clicks across all impressions. |
| CTR % | double | 0.0002218 | clicks / imps | The rate of clicks to impressions. |
| Total Conversions | int | 1 | total_convs | The total number of post-view and post-click conversions. |
| Conversion Rate | double | 0.0002218 | total_convs / imps | The rate of conversions to impressions. |
| Conversions per Million | double | 221.87708 | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| Revenue | money | 25.767257 | booked_revenue + reseller_revenue | The total revenue booked through direct advertisers (line item) and direct publishers (resold impressions). This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Booked Revenue | money | 25.767257 | booked_revenue | The total revenue booked through direct advertisers (line item). This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Resold Revenue | money | 0 | reseller_revenue | The total revenue on resold impressions through direct publishers. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Post View Conversions | int | 15 | post_view_convs | The total number of recorded post-view conversions. |
| Post Click Conversions | int | 15 | post_click_convs | The total number of recorded post-click conversions. |
| Cost | money | 16.833378 | cost | The total amount of media cost for direct publisher and purchased third-party inventory. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Profit | money | 0.084102 | Booked revenue - Total cost | Booked revenue minus total cost. |
| CPM | money | 1.6605168 | (cost / imps) x 1000 | The media cost per 1000 impressions. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Total RPM | money | 2.6054831 | (revenue / imps) x 1000 | The revenue per 1000 impressions. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| PPM | money | 0.9449662 | (profit / imps) x 1000 | **To be deprecated.** The profit per 1000 impressions. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| Total Cost | money | 123.45 | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | money | 123.45 | (Total Cost/Imps) * 1000 | The total cost per 1,000 imps. |
| Total Cost eCPC | money | 123.45 | (Total Cost/Click) | The total cost per click. |
| Total Cost eCPA | money | 123.45 | (Total Cost/Conversion) | The total cost per conversion. |
| Profit eCPM | money | 123.45 | ((Booked revenue - Total cost)/Imps) * 1,000 | Profit per thousand impressions. |
| Profit eCPC | money | 123.45 | (Booked revenue - Total cost)/Click | Profit per click. |
| Profit eCPA | money | 123.45 | (Booked revenue - Total cost)/Conversion | Profit per conversion. |
| Profit Margin | money | 123.45 | (Booked revenue - Total cost)/Booked revenue | Buyer profit margin. |
| Network Profit | money | 123.45 | Booked revenue + Reseller revenue - Total Cost | The sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPM | money | 123.45 | (Network profit/Imps) * 1000 | Network profit per thousand impressions. |
| Network Profit eCPC | money | 123.45 | Network profit/Clicks | Network profit per click. |
| Network Profit eCPA | money | 123.45 | Network profit/Conversions | Network profit per conversion. |
| Network Profit Margin | money | 123.45 | Network profit/(Booked revenue + reseller revenue) | Network profit margin. |
| Device Type |  | Tablets, mobile phones |  | This is the type of device being used. |
| Conversion Device Make | string | Apple (26) |  | This is the device that the conversion occurred on. This can be compared against Device Make to determine what device the impression occurred on. |
| Device Make |  | Apple (26) |  | This is the brand name of the device. |
| Conversion Device Type | string | Tablets, mobile phones |  | This can be compared against Device Type to determine what device the conversion occurred on. |
| Video Skips | int | 10 |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Starts | int | 11 |  | The total number of times the first segment of the video creative was downloaded and started. |
| 25% Video Complete | int | 10 |  | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | int | 10 |  | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | int | 10 |  | The total number of times the video creatives completed 75% of the entire duration. |
| Video Completions | int | 12 |  | The total number of times the video creatives played for the entire duration. |
| Videos Served | int | 10 |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Video Errors | int | 2 |  | The total number of times a video error occurred. |
| Revenue Per Video Complete | money | 25.767257 |  | The revenue per video completion. |
| Cost Per Video Complete | money | 22.767257 |  | The cost per video completion. |
| Video Completion Rate | double | 1.12359550561797% | (Video Completions/Total Impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage . |
| Video Start Rate | double | 1.12359550561797% |  | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Skip Rate | double | 1.12359550561797% |  | The percentage of times the user opted to skip the video. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, select on **Prebid Server Premium &gt; Analytics &gt; Prebid Server Analytics**
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

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

- [Carrier Analytics Report](carrier-analytics-report.md)
- [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md)
- [Buying Mobile Inventory](buying-mobile-inventory.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
- [Reporting Guide](reporting-guide.md)
- [Member Reporting](network-reporting.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
