---
title: Microsoft Monetize - Multi-Buyer Seller Deal Metrics
description: Explore metrics in the article, revealing insights for sellers on multi-buyer deal performance and rejection reasons.
ms.date: 10/28/2023
---


# Microsoft Monetize - Multi-buyer seller deal metrics

The Multi-Buyer Seller Deal Metrics report provides key information relevant to sellers about multi-buyer deal metrics, performance, and rejection reasons.

> [!NOTE]
> As of May 3, 2021, Imps Matched and Bid Requests will be randomly sampled at a rate of 10 percent. The sampled values will be multiplied by 10 to give a reasonable estimate in all screens where these two metrics are reported. No other deal metrics will be affected.

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

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Buyer Member | Yes | ID and name of the member whose advertiser purchased the impression. |
| Buyer Seat Name | No | Display name for the buyer seat code |
| Buyer Seat Code | No | Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression |
| Deal | Yes | Deal associated with the impression |
| Ask Price | No | Ask price for the deal |
| Bidder ID | Yes | ID of the bidder (DSP) for the impression |
| Bidder Name | No | Name of the bidder (DSP) for the impression |
| Start Date | No | Date and time when the deal starts being available to the buyer |
| End Date | No | Date and time when the deal stops being available to the buyer |
| Deal Buyer Type | Yes | Select to filter by the type of buyer the impression served through. Possible values are Entire Deal, Bidder, Buyer Member and Buyer Seat.<br> - **Entire Deal**: Deal metrics for the entire deal, across all buyers.<br> - **Bidder**: Deal metrics for all buyers within the given DSP on the deal.<br> - **Buyer Member**: Deal metrics for a single legacy Microsoft Advertising buyer member ID. When looking at a bidder-level deal, you will only see impressions matched and bid requests in the Bidder and the Entire Deal rows, not in the Buyer Member or the Buyer Seat.<br> - **Buyer Seat**: Deal metrics for a single seat ID (DSP's proprietary buyer ID). When looking at a bidder-level deal, you will only see impressions matched and bid requests in the Bidder and the Entire Deal rows, not the Buyer Member or the Buyer Seat.<br>**Note**: This dimension is mandatory on the Multi-Buyer Deal Metrics Report. To not see data broken out by deal buyer type, filter by Entire Deal. |
| Deal Type Name | No | Whether the deal is an open deal, private deal, or programmatic guaranteed deal |
| Deal Auction Type Name | No | Type of auction (standard-, first- or fixed-price) |
| Priority | No | For a private auction only, the priority the seller assigned to the deal |
| Package ID | No | ID of the Package that the deal was created from. This value will be 0 if the deal was not created from a package. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Imps (matched) | The total number of impressions that matched the deal's targeting settings. |
| Imps (won) | The total number of impressions won. |
| Seller Revenue | The seller revenue on the deal. |
| Seller Revenue eCPM | The seller revenue on the deal, represented in eCPM. |
| Bid Rate | The percentage of impressions bid on compared to the number of bid requests sent to the buyer. |
| Gross Win Rate | The percentage of impressions won compared to the number of impressions matched. |
| Ineligible Bid Rate | The percentage of rejected bids compared to the total number of bids - calculated as Reject Count / Bids. |
| Net Win Rate | The percentage of impressions won compared to the number of bids made by the buyer - calcuated as Imps (won) / Bids. |
| Average Biased Bid | The average biased bid for the deal. This is the bid price used for ranking purposes in the auction. |
| Average Floor Price | The average floor price for bids against this deal. If an Ask Price is set on the deal, this value will be constant. If the deal uses Market Price, then this value will be the average floor price calculated from the floors applied to this deal across all auctions. |
| Average Net Bid | The average net bid on the deal. This is the bid price that is net of all fees and used in determining seller revenue (prior to any bid price reduction that may take place). |
| Bid Requests | The number of bid requests sent to the buyer. This number may be less than Imps (matched) due to buyer filters or seller settings. |
| Total Bids | The total number of bids submitted by the buyer for this deal. |
| Reject Below Floor Count | The number of bids rejected because they are below the reserve price set on the auction. |
| Reject Below Floor Ym Count | The number of bids rejected because they are below the yield management floor applicable for the auction. |
| Reject Bidder Error Count | The number of bids rejected due to bidder errors. |
| Reject Bidder Error Deal Not Available Count | The number of bids rejected because the deal is no longer available. |
| Reject Blocked By Ad Profile Adserver Count | The number of bids blocked by the seller's Ad Profile due to adserver exclusions. |
| Reject Blocked By Ad Profile Audit Status Count | The number of bids blocked by the Ad Profile due to their audit status. This typically happens when the buyer is bidding with an unaudited creative and the seller has blocked unaudited creatives in ad quality. |
| Reject Blocked By Ad Profile Brand Count | The number of bids blocked by the Ad Profile due to brand exclusions. |
| Reject Blocked By Ad Profile Category Count | The number of bids blocked by the seller's Ad Profile due to category exclusions. |
| Reject Blocked By Ad Profile Count | The total number of bids rejected by settings on the seller's Ad Profile. |
| Reject Blocked By Ad Profile Creative Count | The number of bids rejected because the creative is blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Language Count | The number of bids rejected because the language of the ad is blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Member Count | The number of bids rejected because the member is blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Tech Attribute Count | The number of bids rejected because a technical attribute or attributes of the creative is blocked by the Ad Profile. |
| Reject Blocked By Deal Adserver Count | The number of bids blocked due to adserver constraints on the Deal. |
| Reject Blocked By Deal Below Floor Count | The number of bids rejected because they are below the deal's floor price. |
| Reject Blocked By Deal Brand Count | The number of bids rejected because their brands are not allowed on the deal. |
| Reject Blocked By Deal Category Count | The number of bids rejected because they do not meet the deal's category requirements. |
| Reject Blocked By Deal Count | The total number of bids rejected due to settings on the deal. |
| Reject Blocked By Deal Creative Count | The number of bids rejected because the creative is blocked by the deal. |
| Reject Blocked By Deal Language Count | The number of bids rejected due to allowed language constraints on the deal. |
| Reject Blocked By Deal Media Subtype Count | The number of bids rejected due to not matching the deal's allowed media subtypes. |
| Reject Blocked By Deal Payment Type Count | The number of bids rejected due to not matching the deal's allowed payment types. |
| Reject Blocked By Deal Size Count | The number of bids rejected due to not meeting the deal's size requirements. |
| Reject Blocked By Deal Tech Attribute Count | The number of bids rejected due to technical attribute limits on the deal. |
| Reject Blocked By Dynamic Adserver Count | The number of bids rejected due to adserver constraints dynamically passed in by the seller at the time of the impression request. |
| Reject Blocked By Dynamic Brand Count | The number of bids rejected because the brand is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Category Count | The number of bids rejected because the category is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Language Count | The number of bids rejected because the language is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Tech Attribute Count | The number of bids rejected because a technical attribute is blocked dynamically by the bid request passed in by the seller. |
| Reject Count | The total number of rejected bids. |
| Reject Invalid Creative Count | The number of bids rejected due to invalid creatives that the buyer bid with. |
| Reject Invalid Creative Not Ssl Count | The number of bids rejected due to the creative not being SSL approved for a secure auction. |
| Reject Other Advertiser Exclusion Count | The total number of bids rejected due to advertiser exclusions not listed above. |
| Reject Other Count | The total number of bids rejected for reasons other than data security not listed above. |
| Reject Other Data Protection Count | The total number of bids rejected for data security reasons not listed above. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   1. Or, from the Publishers top menu, click on **Prebid Server Premium** \>  **Analytics** \> **Prebid Server Analytics**.
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
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md). (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Network Reporting](network-reporting.md)
- [Publisher Reporting](publisher-reporting.md)
