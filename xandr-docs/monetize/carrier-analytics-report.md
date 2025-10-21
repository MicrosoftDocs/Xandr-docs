---
title: Microsoft Monetize - Carrier Analytics Report
description: Explore Carrier Analytics, analyze device performance, assess carrier impact on campaigns, and identify carriers for line items.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Carrier analytics report

The **Carrier Analytics** report enables you to retrieve buy-side and sell-side performance data based on carriers for devices. This is especially helpful for analyzing how carriers affect line item or campaign performance and advertiser payment. Also, in cases where advertisers set up specific landing pages for each carrier, this report helps you identify the carriers that a line item or campaign ran on.

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

## Data retention period

This report's data is retained for 46 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

**Currency 2.0**

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Example | Description |
|--|--|--|--|
| Advertiser | Yes | "Mobile Zombies (789)" | The name of the advertiser followed by the ID (Microsoft Advertising format). |
| Bid Type | Yes | "Manual" | The optimization phase the node was in when it bid for the impression. Note that the term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". Allowed values:<br>"Manual": Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br>"Learn": Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br>"Optimized": Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br>"Unknown": The node was in an unknown optimization phase.<br>"Optimized give up"<br>"Learn give up"<br>"Manual give up" |
| Buyer | Yes | "My Network (123)" | The name of the buying member followed by the ID (Microsoft Advertising format). |
| Campaign | Yes | "Mobile Campaign (222)" | The name of the campaign followed by the ID (Microsoft Advertising format). (Does not apply to all advertisers.) |
| Carrier | Yes | "Sprint - FR (20)" | The name of the carrier followed by the ID (Microsoft Advertising format). If the carrier is smaller, you may see this value appear as -1 because it is aggregated. |
| Connection Type | Yes | "Carrier" | The type of internet connection at the time of the impression. Possible values: "Carrier-based" or "WiFi or Static". |
| Country | Yes | "US" | The code for the country. |
| Device Type | Yes | 15 | The type of device on which the impression was served. Possible values: "Phone", "Tablet", or "Other Devices". |
| Impression Type | Yes | "Resold" | The type of impression. Possible values (associated IDs in parentheses):<br>`Blank (1)`: No creative served.<br>PSA (2): A public service announcement served because no other creative was eligible.<br>Default Error (3): A default creative served due to timeout issue.<br>Default (4): A default creative served because no line item or campaign bid or no other creative was eligible.<br>Kept (5): One of your managed advertisers served a creative.<br>Resold (6): The impression was sold to a third-party buyer.<br>RTB (7): Your creative served on third-party inventory.<br>PSA Default Error (8): A public service announcement served due to timeout issue.<br>External Impression (9): An impression from an impression tracker.<br>External Click (10): A click from a click tracker.<br>Insertion (11): Your creative served on third-party inventory where it persists across page-loads and sessions. |
| Insertion Order | Yes | "Mobile Insertion Order (321)" | The name of the insertion order followed by the ID (Microsoft Advertising format). |
| Line Item | Yes | "Mobile Line Item (111)" | The name of the line item followed by the ID (Microsoft Advertising format). |
| Media Type | Yes | "Banner" | The media type of the creative. Possible values: "Banner", "Pop", "Interstitial", "Video", "Text", "Expandable", "Skin", or "Facebook". |
| Payment Rule | Yes | "Homepage Payment Rule (1215)" | The type of the payment rule followed by the ID. |
| Payment Type | Yes | "com", "revshare" | The type of payment to a broker. |
| Publisher | Yes | "Undead.com (456)" | The name of the publisher followed by the ID (Microsoft Advertising format). |
| Revenue Type | Yes | "CPA" | The basis on which the advertiser pays the member. |
| Seller | Yes | "That Seller (456)" | The name of the selling member followed by the ID (Microsoft Advertising format). |
| Size | Yes | "728x90" | The size of the creative served. |
| Split | Yes | "Mobile Split A (342)" | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Example | Formula | Description |
|--|--|--|--|
| 25% Video Complete | 10 |  | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | 10 |  | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | 10 |  | The total number of times the video creatives completed 75% of the entire duration. |
| Booked Revenue | 25.767257 | booked_revenue | The total revenue booked through direct advertisers (line item). |
| Clicks | 1 | clicks | The total number of clicks across all impressions. |
| Conversion Rate | 0.000221877080097626 | total_convs / imps | The rate of conversions to impressions. |
| Conversions per Million | 221.877080097625 | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| Cost | 16.833378 | cost | The total amount of media cost for direct publisher and purchased third-party inventory. |
| Cost Per Video Complete | 22.767257 |  | The cost per video completion. |
| CPM | 1.66051685393258 | (cost / imps) x 1000 | The media cost per 1000 impressions. |
| CTR % | 0.000221877080097626 | clicks / imps | The rate of clicks to impressions. |
| Imps | 2340 | imps | The total number of impressions (served and resold). |
| Network Profit | 123.45 | Booked revenue + Reseller revenue - Total Cost | The sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPA | 123.45 | Network profit/Conversions | Network profit per conversion. |
| Network Profit eCPC | 123.45 | Network profit/Clicks | Network profit per click. |
| Network Profit eCPM | 123.45 | (Network profit/Imps) * 1000 | Network profit per thousand impressions. |
| Network Profit Margin | 123.45 | Network profit/(Booked revenue + reseller revenue) | Network profit margin. |
| Post Click Conversions | 15 | post_click_convs | The total number of recorded post-click conversions. |
| Post View Conversions | 15 | post_view_convs | The total number of recorded post-view conversions. |
| PPM | 0.944966292134831 | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| Profit | 0.084102 | Booked revenue - Total cost | Booked revenue minus total cost. |
| Profit eCPA | 123.45 | (Booked Revenue - Total Cost)/Conversion | Profit per conversion. |
| Profit eCPC | 123.45 | (Booked Revenue - Total Cost)/Click | Profit per click. |
| Profit eCPM | 123.45 | ((Booked Revenue - Total Cost)/Imps) * 1,000 | Profit per thousand impressions. |
| Profit Margin | 123.45 | (Booked Revenue - Total Cost)/Booked Revenue | Buyer profit margin. |
| Resold Revenue | 0 | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| Revenue | 25.767257 | booked_revenue + reseller_revenue | The total revenue booked through direct advertisers (line item) and direct publishers (resold impressions). |
| Revenue Per Video Complete | 25.767257 |  | The revenue per video completion. |
| Total Conversions | 1 | total_convs | The total number of post-view and post-click conversions. |
| Total Cost | 123.45 | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPA | 123.45 | (Total Cost/Conversion) | The total cost per conversion. |
| Total Cost eCPC | 123.45 | (Total Cost/Click) | The total cost per click. |
| Total Cost eCPM | 123.45 | (Total Cost/Imps) * 1000 | The total cost per 1,000 imps. |
| Total RPM | 2.60548314606741 | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| Video Completion Rate | 1.12359550561797% | (Video Completions/Total Impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage . |
| Video Completions | 12 |  | The total number of times the video creatives played for the entire duration. |
| Video Errors | 2 |  | The total number of times a video error occurred. |
| Video Skip Rate | 1.12359550561797% |  | The percentage of times the user opted to skip the video. |
| Video Skips | 10 |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Start Rate | 1.12359550561797% |  | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Starts | 11 |  | The total number of times the first segment of the video creative was downloaded and started. |
| Videos Served | 10 |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium** \>  **Analytics** \>  **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    >
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    >
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data,  you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A  popup notification will let you know when the report is ready to view or download.

        > [!TIP]
        >
        > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Device Analytics Report](device-analytics-report.md)
- [Buying Mobile Inventory](buying-mobile-inventory.md)
- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Mobile Ad Call Reference](mobile-ad-call-reference.md)
- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
