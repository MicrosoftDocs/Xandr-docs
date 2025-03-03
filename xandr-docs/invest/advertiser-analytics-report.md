---
title: Microsoft Invest - Advertiser Analytics Report
description: In this article, learn about the Advertiser Analytics report that lets you view buy-side data for a specific advertiser.
ms.date: 10/28/2023
---

# Microsoft Invest - Advertiser Analytics report

The Advertiser Analytics report lets you view buy-side data for a specific advertiser. The data available via this report is even more granular than what you can get from the [Member Analytics Report](network-analytics-report.md).

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

> [!NOTE]
> For impressions older than 100 days, the day will be returned rather than the hour.

For more information about how quickly report data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Data retention period

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data (however, daily, monthly and cumulative intervals are still available)
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match statistics shown elsewhere in Microsoft Invest for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months is aggregated. The data from Billing reports are kept in non-aggregated form indefinitely.

## Real time data

Real Time Data is offered within this report (not all users have access). Traditionally, reports have had a 2 hour built-in delay to allow for a fuller reconciliation with conversions, impressions and other metrics associated with transactions. However, in some cases, it is important to have up-to-the-minute information even if it has not been fully reconciled yet. Dimensions which support the real-time option are marked with the clock icon.

:::image type="content" source="./media/real-time-data-reporting.png" alt-text="Diagram of a real time data.":::

- To use this new feature, set the **Real Time Data** field to **Included**. This will cause the data in your report to contain both real-time and the more fully reconciled batch file data. If you want the report to break out the real-time data from batch file data, select the **Real-Time status** checkbox.
- Do not use information in the real-time data portion of your report to bill your clients as that data may change slightly once fully
  reconciled within 2 to 4 hours. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, select the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

> [!IMPORTANT]
> The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.
>
> Some dimensions have *attributes*. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: *Dimension_Name:Attribute_Name*
>
> For all revenue fields, the currency is defined by the **Buying Currency** field (When Currency 2.0 is disabled).

| Column | Filter? | Description |
|:-------|:--------|:------------|
| Seller | Yes | The seller of the impression. |
| Seller Type | Yes | Microsoft Advertising buckets sellers into different types for billing purposes. For more information, see [Seller Types](#seller-types). |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement | Yes | The placement through which this impression occurred. <br><br>**Note:** For impressions older than 100 days, placements are aggregated into one row with `-1` as the ID and a generic name. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Line Item: Type | No | The line item type (e.g., Standard, Augmented). |
| Line Item: Status | No | The line item status (e.g., inactive, active). |
| Line Item: Start Date | No | The start date of the line item. |
| Line Item: End Date | No | The end date of the line item. |
| Line Item: Imps Budget (daily) | No | The daily impression budget of the line item. |
| Line Item: Imps Budget (lifetime) | No | The lifetime impression budget of the line item. |
| Line Item: Revenue Budget (daily) Adv Currency | No | The daily revenue budget of the line item. This dimension is available only when Currency 2.0 is disabled. |
| Line Item: Revenue Budget (lifetime) Adv Currency | No | The lifetime revenue budget of the line item. This dimension is available only when Currency 2.0 is disabled. |
| Line Item: Comments | No | Any comments that have been entered for the line item. |
| Line Item: Type (reporting label) | Yes | A custom reporting label field used to list the line item type (e.g., Retargeting LI). This is not the same as the **Type** attribute described above. You may only select one reporting label per report. |
| Line Item: Sales Rep (reporting label) | Yes | A custom reporting label field containing the sales representative. You may only select one reporting label per report. |
| Line Item: Trafficker (reporting label) | Yes | A custom reporting label field containing the trafficker. You may only select one reporting label per report. |
| Flight | No | The line item flight under which the impression was purchased. |
| Flight: Start Date | No | The start date of the flight under which the impression was purchased. |
| Flight: End Date | No | The end date of the flight under which the impression was purchased. |
| Flight: Imp Budget (daily) | No | The daily budget in impressions for the flight. |
| Flight: Imp Budget (lifetime) | No | The lifetime budget in impressions for the flight. |
| Flight: Revenue Budget (daily) Advertiser Currency | No | The daily budget in revenue for the flight. This dimension is available only when Currency 2.0 is disabled. |
| Flight: Revenue Budget (lifetime) Advertiser Currency | No | The lifetime budget in revenue for the flight. This dimension is available only when Currency 2.0 is disabled. |
| Campaign | Yes | The campaign that purchased this impression. (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the **Split** column (if included) will be null. |
| Creative | Yes | The creative that served on this impression. For more information about creatives, see [Working with Creatives](working-with-creatives.md). <br><br>**Note:** For impressions older than 100 days, creatives will be aggregated into one row with `0` as the ID and a generic name. |
| Media Type | Yes | The media type associated with the creative that served on this impression. |
| Country | Yes | The country/region in which the impression took place. |
| Size | Yes | The size of the creative, e.g., 320x50. There may be situations where the size listed in the report does not match the size of the placement. This happens when Promo Sizes come into the equation. When a creative serves into a placement fulfilling a size in the Promo Sizes Array, the size reported is the `size` of the creative, which could be different from the promo size or the placement's size. |
| Bid Type | Yes | See [Bid Types](#bid-types) below for definitions of the different types of bids. |
| Advertiser Currency | Yes | The default currency of the advertiser who purchased this impression. This is set when an advertiser is created. For more information, see [Create an Advertiser](create-an-advertiser.md). <br><br> **Tip:** To display the cost/revenue in the local currency, select **Adv. Currency** as a dimension. <br/> This dimension is available only when Currency 2.0 is disabled. |
| Conversion Pixel | Yes | The conversion pixel that was fired, if any. To view pixel-specific metrics in separate columns of your report, do both of the following: <br/> - Filter by a set of pixels (up to a maximum of 20 pixels) in the Conversion Pixel filter. <br/> - Select the Conversion Pixel dimension. <br/> For more information about conversion pixels, see [Working with Conversion Pixels](working-with-conversion-pixels.md). |
| Revenue Type | Yes | The basis on which the advertiser has agreed to pay you for the impression. For more information, see [Revenue Types](#revenue-types). |
| Payment Type | Yes | How the buyer is paying for the impression. See [Payment Types](#payment-types) for definitions of the different payment types. |
| Campaign Priority | No | The bidding priority of the campaign that purchased this impression. (Does not apply to all advertisers.) |
| Billing Period | No | The insertion order's billing period. |
| Billing Period: Start Date | No | The start date of the insertion order's billing period. |
| Billing Period: End Date | No | The end date of the insertion order's billing period. |
| Billing Period: Booked Imps Budget (daily) | No | The daily impression budget of the insertion order's billing period. |
| Billing Period: Booked Imps Budget (lifetime) | No | The lifetime impression budget of the insertion order's billing period. |
| Billing Period: Revenue Budget (daily) Buying Currency | No | The daily revenue budget of the insertion order's billing period. This dimension is available only when Currency 2.0 is disabled. |
| Billing Period: Revenue Budget (lifetime) Buying Currency | No | The lifetime revenue budget of the insertion order's billing period. This dimension is available only when Currency 2.0 is disabled. |
| Billing Period: External Code | No | The custom code for the billing period. |
| Venue | No | The venue on which this impression occurred. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Campaign: Test/Control (reporting label) | Yes | The name of the control group the user who viewed this impression belonged to, if any. |
| Insertion Order | Yes | The insertion order under which this impression was purchased. |
| Insertion Order: Type | No | The insertion order type (e.g., Legacy IO, Seamless IO). For more information, see [Create an Insertion Order](create-an-insertion-order.md). |
| Insertion Order: State | No | The state of the insertion order (e.g., active, inactive). |
| Insertion Order: Start Date | No | The start date of the insertion order (for legacy insertion orders). |
| Insertion Order: End Date | No | The end date of the insertion order (for legacy insertion orders). |
| Insertion Order: Imps Budget (daily) | No | The daily impression budget of the insertion order. |
| Insertion Order: Imps Budget (lifetime) | No | The lifetime impression budget of the insertion order. |
| Insertion Order: Revenue Budget (daily) | No | The daily budget in revenue for the insertion order. |
| Insertion Order: Revenue Budget (lifetime) | No | The lifetime budget in revenue for the insertion order. |
| Insertion Order: Billing Code | No | The billing code associated with the insertion order (if there is one). |
| Insertion Order: Type (reporting label) | Yes | A custom reporting label field used to list the insertion order type (e.g., Branding IO). This is not the same as the **Type** attribute described above. You may only select one reporting label per report. |
| Insertion Order: Sales Rep (reporting label) | Yes | A customer reporting label field used to list the sales representative associated with the insertion order. You may only select one reporting label per report. |
| Insertion Order: Trafficker (reporting label) | Yes | A customer reporting label field used to list the trafficker associated with the insertion order. You may only select one reporting label per report. |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the monetary metrics to be displayed in the buying currency. This dimension is available only when Currency 2.0 is disabled. |
| Selling Currency | No | The transaction currency used by the seller to sell this impression. Including this dimension will cause most monetary metrics to be displayed in the selling currency. This dimension is available only when Currency 2.0 is disabled. |
| Publisher Currency | No | This is the currency in which the publisher sells their inventory. This dimension is available only when Currency 2.0 is disabled. |
| Adjustments | No | Changes to Member reported revenue based on factors such as revenue, conversions, clicks, or impressions reported by their advertisers or agencies' ad servers. |
| Clearing Event | Yes | The clearing event associated with the impression (e.g., Impressions, Views - Standard Display). |
| Creative Code | No | Optional code associated with the creative that ran. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

### Seller types

| Name | Definition |
|:-----|:-----------|
| platform | When you purchase platform inventory, you will be charged your contracted auction service fee. |
| partner | When you purchase inventory from one of our external supply partners, you will be charged your contracted auction service fee. |
| unknown | The seller type is not identifiable. You shouldn't see this turn up in your reports. If you do, contact your [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com). |

### Bid types

> [!NOTE]
> The term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price".

| Name | Definition |
|:-----|:-----------|
| Manual | Base CPM bid. Only applies when you are bidding with a CPM goal whether it's Base, EAP, or ECP. |
| Learn | Learn bid. Only applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized. |
| Optimized | Optimized bid. Only applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized. |
| Unknown | The node was in an unknown optimization phase. |
| Optimized give up | The bid was "Optimized" but was below the venue's "give up" price. |
| Learn give up | The bid was "Learn" but was below the venue's "give up" price. |
| Manual give up | The bid was "Manual" but was below the venue's "give up" price |

### Revenue types

| Name             | Description                                                             |
|:-----------------|:------------------------------------------------------------------------|
| No Payment       |                                                                         |
| Flat CPM         | A flat payment per 1000 impressions.                                    |
| Cost plus CPM    | Cost (what you spend on inventory) plus an extra CPM.                   |
| Cost plus margin | Cost (what you spend on inventory) plus a percentage of what you spend. |
| CPC              | A flat payment per click.                                               |
| CPA              | A flat payment per conversion.                                          |
| Revshare         | A payment on a revshare basis (CPC or CPA).                             |
| Estimated CPM    | The estimated payment per 1000 impressions.                             |
| CPVM             | A flat payment per 1000 viewable impressions.                           |

### Payment types

| Name           | Description                                         |
|:---------------|:----------------------------------------------------|
| No Payment     |                                                     |
| CPM            | Payment per 1000 impressions.                       |
| CPC            | Payment per click.                                  |
| CPA            | Payment per action.                                 |
| Owner CPM      | Publisher is paid on a CPM basis.                   |
| Owner revshare | Publisher is paid on a Revshare basis (CPC or CPA). |
| CPVM           | Payment per 1000 viewable impressions.              |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|:-------|:------------|
| Imps | The total number of impressions. |
| Imps (master creative) | The number of page-level roadblocks that served the master creative. <br><br>**Note:** Alpha-Beta Notice:<br> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Clicks | The total number of clicks. |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Total Conversions | The total number of post-view and post-click conversions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Conversions per Million | The number of conversions per million impressions. |
| Click-to-Conv Rate | The ratio of clicks to conversions. |
| Total Revenue | The total revenue; the sum of booked and resold revenue. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post View Conversions | The number of post-view conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post View Revenue | The amount of revenue derived from post-view conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post Click Convs | The number of post-click conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Revenue | The amount of revenue derived from post-click conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPM | The total revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPC | The total revenue, expressed as eCPC. For definitons of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPA | The revenue per conversion or acquisition, expressed as eCPA. For the definition of eCPA, see the see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Media Cost | The total amount of media cost across both managed publishers and RTB inventory. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPM | The cost per thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPC | The cost per click. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPA | The cost per acquisition (conversion). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit | Booked revenue minus total cost. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit eCPM | The profit per thousand impressions. Here profit is defined as the booked revenue minus total cost. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit Margin | The profit, expressed as a percentage of revenue. Here profit is defined as the booked revenue minus total cost. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post View Conversion Rate | The ratio of post-view conversions to impressions. |
| Post Click Conversion Rate | The ratio of post-click conversions to impressions. |
| Commissions | The total commissions that come out of your booked revenue. Commissions are $0. |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps). |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Video Views | If you use the CPM bid strategy on the Microsoft Advertising Platform, online video views count each instance a potential customer plays your video for two continuous seconds with more than 50% of the screen in view. If you use the CPCV bid strategy for CTV, video views count each time a potential customer plays your video for 15 continuous seconds or clicks on the video, whichever occurs first. <br> **NOTE:** When you select CPCV as the bidding strategy, you pay for either a video view or a click, whichever occurs first. Video views exclude click interactions with the ad, which are captured under the Clicks metric. |
| Video Completion Rate | On the Microsoft Advertising Platform, video completion rate represents the ratio of completed video views to the total number of video impressions. <br> **NOTE:** Discrepancies in video views impressions may occur due to technical issues on the publisher's side, which can affect the reported percentages. |
| Clearing Event Booked Revenue Per Event | The total booked revenue per clearing event. |
| Clearing Events Booked Revenue CPM | The booked revenue in CPM per event. |
| Booked Revenue vCPM | The booked revenue, expressed as a viewable CPM. |
| vCPM | The CPM for viewable impressions. |
| Media Cost vCPM | The media cost expressed in terms of viewable CPM. |
| Clearing Event Buyer Media Cost Per Event | The media cost per clearing event. |
| Clearing Event Buyer Media Cost eCPM | The total media cost per 1000 events (for the associated clearing event). |
| Clearing Event Units | The total number of events purchased (for the associated Clearing Event). When buying a Clearing Event other than impression (e.g., viewable impressions), the number of billed events will be less than the number of impressions. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Profit eCPC | Profit per click. <br><br> **Note:** This new field defines "profit" as booked revenue minus total cost. |
| Profit eCPA | Profit per conversion. <br><br> **Note:** This new field defines "profit" as booked revenue minus total cost. |
| Post-View Cross Device Conversions | The number of post-view Cross Device conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post-Click Cross Device Conversions | The number of post-click Cross Device conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Video Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Starts | The total number of times the first segment of the video creative was downloaded and started. |
| 25% Video Complete | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | The total number of times the video creatives completed 75% of the entire duration. |
| Video Completions | The total number of times the video creatives played for the entire duration. |
| Videos Served | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Video Errors | The total number of times a video error occurred. |
| Revenue Per Video Complete | The revenue per video completion. |
| Cost Per Video Complete | The cost per video completion. |
| Video Completion Rate | The ratio of video completions to impressions, expressed as a percentage (video completions/total impressions). |
| Video Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Skip Rate | The percentage of times the user opted to skip the video. |

### Custom viewable definition metrics

| Column | Description |
|:-------|:------------|
| Custom Viewable Imps | The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Microsoft Advertising account representative). |
| Custom Viewability Rate | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been
    configured).
    1. Or, from the Publishers top menu, select **Prebid Server Premium &gt; Analytics &gt; Prebid Server Analytics**
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in
    the order you prefer.

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

## Related topic

[Member Reporting](network-reporting.md)
