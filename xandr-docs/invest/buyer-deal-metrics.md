---
title: Microsoft Invest - Buyer Deal Metrics Report
description: Discover the definition of a Buyer Deal Metrics Report and how to generate it to access details such as deal metrics, performance, and reasons for rejection.
ms.date: 10/28/2023
---

# Microsoft Invest - Buyer Deal Metrics report

> [!NOTE]
> As of May 3, 2021, Imps Matched and Bid Requests will be randomly sampled at a rate of 10 percent. The sampled values will be multiplied by 10 to give a reasonable estimate in all screens where these two metrics are reported. No other deal metrics will be affected.

The Buyer Deal Metrics report provides key information about deal metrics, performance, and rejection reasons that is relevant to buyers.

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

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Seller | Yes | The seller that sold the deal. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Ask Price | No | The ask price for the deal. |
| LI Id | Yes | The ID of the line item. |
| Start Date | No | The day and time when the deal starts being available to the buyer. |
| End Date | No | The day and time when the deal stops being available to the buyer. |
| Deal Type Name | No | Whether the deal is a public deal or a private deal. |
| Deal Auction Type Name | No | Whether the auction was a second price auction or a fixed price auction. |
| Package ID | No | The ID of the package, if the deal is associated with a package. |
| Priority | No | For a private auction only, the priority the seller assigned to the deal. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps (matched) | The total number of impressions matched. |
| Imps (won) | The total number of impressions won. |
| Buyer Media Cost | The total cost to the buyer. |
| Buyer Cost eCPM | The total cost to the buyer in eCPM. |
| Bid Rate | The rate of bidding on the deal. |
| Gross Win Rate | The gross win rate for the deal. |
| Ineligible Bid Rate | The rate of bids that were ineligible for the deal. |
| Net Win Rate | The net win rate for bids on the deal. |
| Bid Requests | The number of bid requests. |
| Bids | The total number of times you bid on the deal. |
| Reject Below Floor Count | The number of bids rejected because they are below the reserve price set on the auction. |
| Reject Below Floor Ym Count | The number of bids rejected because they are below the yield management floor set for the deal. |
| Reject Bidder Error Count | The number of bids rejected due to bidder errors. |
| Reject Bidder Error Deal Not Available Count | The number of bids rejected because the deal was no longer available. |
| Reject Blocked By Ad Profile Adserver Count | The number of bids rejected because an ad server associated to the creative that the buyer bid with is blocked. |
| Reject Blocked By Ad Profile Audit Status Count | The number of bids blocked by the Ad Profile due to their audit status. This typically happens when the buyer is bidding with an unaudited creative and the seller has blocked unaudited creatives in ad quality. |
| Reject Blocked By Ad Profile Brand Count | The number of bids blocked by the Ad Profile due to brand exclusions. |
| Reject Blocked By Ad Profile Category Count | The number of bids rejected because the ad profile does not allow the category of the creative. |
| Reject Blocked By Ad Profile Count | The sum of all bids rejected by the ad profile. |
| Reject Blocked By Ad Profile Creative Count | The number of bids rejected because the creative ad server was blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Language Count | The number of bids rejected because the language of the ad was blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Member Count | The number of bids rejected because the member was blocked by the Ad Profile. |
| Reject Blocked By Ad Profile Tech Attribute Count | The number of bids rejected because a technical attribute or attributes of the creative were blocked by the Ad Profile. |
| Reject Blocked By Deal Adserver Count | The number of bids blocked due to adserver constraints on the deal. |
| Reject Blocked By Deal Below Floor Count | The number of bids rejected because they are below the deal's floor price. |
| Reject Blocked By Deal Brand Count | The number of bids rejected because their brands were not allowed on the deal. |
| Reject Blocked By Deal Category Count | The number of bids rejected because they did not meet the deal's category requirements. |
| Reject Blocked By Deal Count | The sum of all bids rejected due to constraints of the deal. |
| Reject Blocked By Deal Creative Count | The number of bids rejected because the creative is blocked by the deal. |
| Reject Blocked By Deal Language Count | The number of bids rejected due to allowed language constraints on the deal. |
| Reject Blocked By Deal Media Subtype Count | The number of bids rejected due to not matching the deal's allowed media subtypes. |
| Reject Blocked By Deal Payment Type Count | The number of bids rejected due to not matching the deal's allowed payment types. |
| Reject Blocked By Deal Size Count | The number of bids rejected due to not meeting the deal's size requirements. |
| Reject Blocked By Deal Tech Attribute Count | The number of bids rejected because a technical attribute was blocked by the deal. |
| Reject Blocked By Dynamic Adserver Count | The number of bids rejected due to adserver constraints dynamically passed in by the seller at the time of the impression request. |
| Reject Blocked By Dynamic Brand Count | The number of bids rejected because the brand is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Category Count | The number of bids rejected because the category is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Language Count | The number of bids rejected because the language is blocked dynamically by the bid request passed in by the seller. |
| Reject Blocked By Dynamic Tech Attribute Count | The number of bids rejected because their techincal attributes are blocked dynamically by the bid request passed in by the seller. |
| Reject Count | The total number of rejected bids. |
| Reject Invalid Creative Count | The number of bids rejected due to invalid creatives that the buyer bid with. |
| Reject Blocked By Deal Brand Count | The number of bids rejected because the brand is not allowed on the deal. |
| Reject Invalid Creative Not SSL Count | The number of bids rejected due to the creative not being SSL approved for a secure auction. |
| Reject Other Advertiser Exclusion Count | The total number of bids rejected due to advertiser exclusions not listed above. |
| Reject Other Count | The total number of bids rejected for reasons other than data security not listed above. |
| Reject Other Data Protection Count | The total number of bids rejected for data security reasons not listed above. |
| Submitted Bids | The number of bids which were eligible in the final auction. For deals with Microsoft Advertising sellers, this value is equal to the number of bids minus the number of rejected bids. For deals with SSPs, this value is equal to the number of bids submitted to the SSP for the final auction. |

## Run your report

Follow these steps to run your report. Refer to **Dimensions** and **Metrics** section above for more information about the definitions of the data fields.

1. Select **Reporting** from the **Network**, **Advertiser**, or **Publisher** menu (depending on how your account has been configured).

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.
    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to
    view or download.
    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name
    this template using the text entry field under Name this report (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the Your Reports screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.

1. Select **Run report** to send your report request.

## Related topics

- [Advertiser Reporting](advertiser-reporting.md)
- [Member Reporting](network-reporting.md)
