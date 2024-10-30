---
title: Network Analytics Report
description: The article presents a network analytics report that provides comprehensive insights into both buy and sell-side data for your network.
ms.date: 10/28/2023
---

# Network analytics report

This report lets you view both buy and sell-side data for your Network. For more granular analytics on a specific advertiser or publisher, use the **Advertiser Analytics** and **Publisher Analytics** reports.

**Time frame**

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
- Cumulative: Data is grouped together in one figure, covering the
  entire selected time range.

**Data retention period**

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data (however, daily, monthly and cumulative intervals are still available)
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match [Dates and Times in Reporting](dates-and-times-in-reporting.md) for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months is aggregated. The data from Billing reports are kept in non-aggregated form indefinitely.

**Real time data**

Real Time Data is a new feature being offered within this report (not all users have access yet). Traditionally, reports have had a 2 hour built-in delay to allow for a fuller reconciliation with conversions, impressions and other metrics associated with transactions. However, in some cases, it is important to have up-to-the-minute information even if it has not been fully reconciled yet. Dimensions which support the real-time option are marked with the clock icon.

:::image type="content" source="media/real-time-data-reporting.png" alt-text="Diagram that explains real time data.":::

- To use this new feature, set the **Real Time Data** field to **Included**. This will cause the data in your report to contain both real-time and the more fully reconciled batch file data. If you want the report to break out the real-time data from batch file data, select the **Real-Time status** checkbox.
- Do not use information in the real-time data portion of your report to bill your clients as that data may change slightly once fully
  reconciled within 2 to 4 hours. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

**Time ranges including dates occurring greater than 45 days ago:** If you create a Network analytics report with the **Range** field set to "Lifetime", "Quarter to Date" or "Custom" (where the end date is greater than 45 days from today), your report (regardless of metrics included) will be added to a special queue for "resource-intensive" reports. As a result, the report may take longer than usual to complete. In addition, these resource-intensive reports may, due to the amount of data being requested, fail before being completed. If your report fails to complete, you will receive a notification. If your report request fails, you can:

- rerun the report at a later time.
- use a report type other than Network Analytics.
- alter the way you structure your reports (if possible) so they do not include dates greater than 45 days ago.

If you are frequently requesting Network analytics reports which include dates longer than 45 day ago, you may need to consider running these reports via the API, caching the data and using [Bulk Reporting Feeds](../digital-platform-api/bulk-reporting-feeds.md) or [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md) (LLD).

**Currency 2.0**

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

> [!IMPORTANT]
>
> - The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.
> - Some dimensions have attributes. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax "`Dimension_Name:Attribute_Name`".
> - For all revenue fields, the currency is defined by the **Buying Currency** field.

| Column | Filter? | Description |
|--|--|--|
| Adjustments | No | Changes to Network reported revenue based on factors such as revenue, conversions, clicks, or impressions reported by their advertisers or agencies' ad servers. |
| Buyer | Yes | The buyer of this impression.<br>**Note**: The name might be "Default"; or "Default Error", which means that there was no buyer for the impression, and a default creative was served. |
| Seller | Yes | The seller of this impression. |
| Seller Type | Yes | Microsoft Advertising buckets sellers into different types for billing purposes. For more information about the different seller types, see "Seller Types" below. |
| Advertiser | Yes | The advertiser whose creative served on this impression. |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred.<br>For impressions older than 100 days, the ID will be 0. |
| Placement | Yes | The name and ID of the placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Insertion Order | Yes | The insertion order under which this impression was purchased. |
| Insertion Order: Type | No | The insertion order type (e.g., Legacy IO, Seamless IO). |
| Insertion Order: State | No | The state of the insertion order (e.g., active, inactive). |
| Insertion Order: Start Date | No | The start date of the insertion order (for legacy insertion orders). |
| Insertion Order: End Date | No | The end date of the insertion order (for legacy insertion orders). |
| Insertion Order: Imps Budget (daily) | No | The daily impression budget of the insertion order. |
| Insertion Order: Imps Budget (lifetime) | No | The lifetime impression budget of the insertion order. |
| Insertion Order: Revenue Budget (daily) | No | The daily budget in revenue for the insertion order. |
| Insertion Order: Revenue Budget (lifetime) | No | The lifetime budget in revenue for the insertion order. |
| Insertion Order (lifetime) Pacing | No | The lifetime pacing budget for the insertion order.<br>**Note**: This dimension is applicable to legacy insertion orders, but not for seamless insertion orders. |
| Insertion Order: Billing Code | No | The billing code associated with the insertion order (if there is one). |
| Insertion Order: Comments | No | The comments associated with the insertion order (if there are any). |
| IO: Type (reporting label) | Yes | A custom reporting label field used to list the insertion order type (e.g., Branding IO). This is not the same as the **Type** attribute described above. You may only select one reporting label per report. |
| IO: Sales Rep (reporting label) | Yes | A customer reporting label field used to list the sales representative associated with the insertion order. You may only select one reporting label per report. |
| IO: Trafficker (reporting label) | Yes | A customer reporting label field used to list the trafficker associated with the insertion order. You may only select one reporting label per report. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Line Item: Type | No | The line item type (e.g., Standard, Augmented). |
| Line Item: State | No | The state of the line item (e.g., active, inactive). |
| Line Item: Start Date | No | The start date of the line item. |
| Line Item: End Date | No | The start date of the line item. |
| Line Item: Imps Budget (daily) | No | The daily impression budget of the line item. |
| Line Item: Imps Budget (lifetime) | No | The lifetime impression budget of the line item. |
| Line Item: Revenue Budget (daily) Adv Currency | No | The daily revenue budget of the line item. This dimension is available only when Currency 2.0 is disabled. |
| Line Item (lifetime) Pacing | No | The lifetime pacing budget for the line item.<br>**Note**: This dimension is applicable to standard line items, but not for seamless line items. |
| Line Item: Revenue Budget (lifetime) Adv Currency | No | The lifetime revenue budget of the line item. This dimension is available only when Currency 2.0 is disabled. |
| Line Item: Comments | No | Any comments that have been entered for this line item. |
| LI: Type (reporting label) | Yes | A custom reporting label field used to list the line item type (e.g., Retargeting LI). This is not the same as the **Type** attribute described above. You may only select one reporting label per report. |
| LI: Sales Rep (reporting label) | Yes | A custom reporting label field containing the sales representative. You may only select one reporting label per report. |
| LI: Trafficker (reporting label) | Yes | A custom reporting label field containing the trafficker. You may only select one reporting label per report. |
| Flight | Yes | The line item flight under which the impression was purchased. |
| Flight: Start Date | No | The start date of the line item flight under which the impression was purchased. |
| Flight: End Date | No | The end date of the line item flight under which the impression was purchased. |
| Flight: Imps Budget (daily) | No | The daily budget in impressions for the flight. |
| Flight: Imps Budget (lifetime) | No | The lifetime budget in impressions for the flight. |
| Flight: Revenue Budget (daily) Advertiser Currency | No | The daily budget in revenue for the flight. This dimension is available only when Currency 2.0 is disabled. |
| Flight: Revenue Budget (lifetime) Advertiser Currency | No | The liftime budget in revenue for the flight. This dimension is available only when Currency 2.0 is disabled. |
| Campaign | Yes | The campaign which purchased this impression. (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Media Type | Yes | The media type associated with the creative that served on this impression. |
| Brand | Yes | The brand associated with the creative. Microsoft Advertising keeps a list of advertiser brands in our systems that can be applied to a creative when it's uploaded. For impression type "Resold", no information is available in the **Brand** field for this report. |
| Country | Yes | The country in which the impression took place. For impression requests for which we received no indication that the ad was rendered (i.e., non-transacted), country information **is not** provided. |
| Size | Yes | The size of the creative (e.g., 320x50). |
| Bid Type | Yes | See "Bid Types" below for definitions of the different types of bids. |
| Advertiser Currency | Yes | The default currency of the advertiser in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Publisher Currency | Yes | The default currency of the publisher in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Impression Type | Yes | See **Impression Types** below for definitions of the different types of impressions. |
| Payment Rule | Yes | The payment rule in effect for this impression's auction, if any. |
| Revenue Type | Yes | The basis on which the advertiser has agreed to pay you for the impression. For more information, see **Revenue Types**. |
| Payment Type | Yes | How the buyer is paying for the impression. See **Payment Types** for definitions of the different payment types. |
| Campaign Priority | Yes | The bidding priority of the campaign that purchased this impression. (Does not apply to all advertisers.) |
| Billing Period | Yes | The insertion order's billing period. |
| Billing Period: Start Date | No | The start date of the insertion order's billing period. |
| Billing Period: End Date | No | The end date of the insertion order's billing period. |
| Billing Period: Booked Imps Budget (daily) | No | The daily impression budget of the insertion order's billing period. |
| Billing Period: Booked Imps Budget (lifetime) | No | The lifetime impression budget of the insertion order's billing period. |
| Billing Period: Billing Period: Revenue Budget (daily) Buying Currency | No | The daily revenue budget of the insertion order's billing period. This dimension is available only when Currency 2.0 is disabled. |
| Billing Period: Billing Period: Revenue Budget (lifetime) Buying Currency | No | The lifetime revenue budget of the insertion order's billing period. This dimension is available only when Currency 2.0 is disabled. |
| Billing Period: External Code | No | The custom code for the billing period. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Deal Code | Yes | The custom code for the deal. For deals with external supply partners, this is typically the string used to identify the deal.|
| Adv: Salesperson (reporting label) | Yes | The salesperson associated with this advertiser's account. This is a reporting label. |
| Adv: Account Manager (reporting label) | Yes | The account manager associated with this advertiser's account. This is a reporting label. |
| Advertiser Type (advertiser) | Yes | The type of the advertiser who purchased this impression. This is a reporting label. |
| Salesperson (publisher) | Yes | The salesperson associated with this publisher's account. This is a publisher reporting label. |
| Pub: Account Manager (reporting label) | Yes | The account manager associated with this publisher's account. This is a publisher reporting label. |
| Campaign: Test/Control (reporting label) | Yes | The name of the control group the user who viewed this impression belonged to, if any. |
| Buying Currency | Yes | The transaction currency that the buyer used to purchase the impression. Including this dimension will cause most monetary metrics to be displayed in the buying currency. This dimension is available only when Currency 2.0 is disabled. |
| Selling Currency | Yes | The transaction currency used by the seller to sell this impression. Including this dimension will cause most monetary metrics to be displayed in the selling currency. This dimension is available only when Currency 2.0 is disabled. |
| Creative | Yes | The creative served for the impression.<br>**Note**: For impressions older than 100 days, creatives will be aggregated into one row with 0 as the `creative_id`. For external click or impression trackers, creative_id will be External Clicks or "External Imps". |
| Creative Code | No | The optional code applied to the creative used. |
| External Code | No | The name and ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). |
| Deal Type | Yes | The type of deal. Options are **Open Auction**, **Private Auction**, **First Look**, or **Programmatic Guaranteed**. |
| Filtered Request Reason | Yes | The reason why the impression request was filtered out by Microsoft Advertising inventory quality controls and the auction was not held. Possible reasons are:<br> - Invalid Domain<br> - Invalid IP<br> - Suspected Domain Detection Tampering<br> - Unknown<br><br>**Valid Impression** is also a possible **Filtered Request Reason**, but in that case, an auction was held and it was not filtered. |
| Clearing Event | Yes | The underlying auction event that was transacted (e.g., impression, viewable impression, completed video). |
| Buyer Seat Code | No | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression |
| Buyer Seat Name | No | The display name for the buyer seat code |
| Code 1 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| Code 2 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| Code 3 | No | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Include Adjustments in Reported Data | Check to include adjustments in the report should be included in the report. |
| Imps | The total number of impressions. |
| Imps (master creative) | The number of page-level roadblocks that served the master creative.<br>**Note**: Alpha-Beta Notice:<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Imps (blank) | The total number of impressions in which a blank creative served. |
| Imps (default bidder) | The total number of impressions in which a default creative served because there were no valid bids.|
| Imps (default error) | The total number of impressions in which a default creative served due to timeout issue. |
| Imps (kept) | The total number of impressions in which one of your managed advertisers served a creative. |
| Imps (PSA) | The total number of impressions in which a public service announcement served because no other creative was eligible. |
| Imps (PSA error) | The total number of impressions in which a public service announcement served due to timeout issue. |
| Imps (resold) | The total number of impressions sold to a third-party buyer. |
| Imps (RTB) | The total number of impressions in which your creative served on third-party inventory. |
| Impression Requests | The total number of ad calls (impression requests).<br>**Warning**: This metric is typically inaccurate for video inventory due to occasional delays in receiving video events, which can lead to inflated request totals based on the assumption that the video has expired. For a better video request metric, you should use Ad Requests in the [Seller Fill and Delivery Network Report](seller-fill-and-delivery-network-report.md) or [Network Video Analytics Report](network-video-analytics-report.md). |
| Clicks | The total number of clicks across all impressions. For Invest DSP, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| Total Conversions | The total number of post-view and post-click conversions. |
| Post View Conversions | The number of post-view conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post-View Conversions: Cross Device | The number of post-view cross-device conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post View Conversions: IP | The number of post-view IP conversions. For more information about how we attribute post-view (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Conversions | The number of post-click conversions. For more information about how we attribute post-click (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Conversions: Cross Device | The number of post-click cross-device conversions. For more information about how we attribute post-click (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Conversions: IP | The number of post-click IP conversions. For more information about how we attribute post-click (and other) conversions, see [Conversion Attribution](conversion-attribution.md). |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Booked Revenue | The total booked revenue (does not include resold revenue). |
| Revenue | The total revenue; the sum of booked and resold revenue. |
| RPM Including fees | **Deprecated**. Revenue minus fees per thousand impressions. |
| Booked Revnue eCPC | Booked revenue per click. |
| Booked Revnue eCPA | Booked revenue per acquisition. |
| Cost | The total media cost across direct publishers and RTB inventory. |
| Profit | Booked revenue minus total cost. |
| Profit (net commissions/gross serving fees) | **Deprecated**. The profit after subtracting serving fees and commissions (does not include data costs). |
| PPM Including Fees | **Deprecated**. Profit per thousand impressions (includes commissions and serving fees). |
| Buyer Media Cost eCPM | The effective cost per thousand impressions (eCPM) based on media cost. |
| Buyer Media Cost eCPC | The effective cost per click (eCPC) based on media cost. |
| Buyer Media Cost eCPA | The effective cost per acquisition (eCPA) based on media cost. |
| vCPM | Media Cost per thousand viewable impressions. |
| Commissions | Commissions for standard line items, $0 for ALIs. |
| Serving Fees | Serving fees for standard line items, $0 for ALIs. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Total Network RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. For more information about these impression types, see **Impression Types** below. |
| Total RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. For more information about these impression types, see **Impression Types** below. |
| CPM | The total media cost per 1000 impressions. |
| CPM Including Fees | **Deprecated**. The cost per 1000 impressions including serving fees (does not include commissions or data costs). |
| PPM | **Deprecated**. The total profit per 1000 impressions. |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| CPVM | The cost per 1000 viewable impressions.<br>**Note**: Alpha-Beta Notice:<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Imps (master creative) | The number of page-level roadblocks that served the master creative.<br>**Note**: Alpha-Beta Notice:<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Feature Costs | Costs incurred when using a platform feature such as cross-device. |
| Segment Data Costs | All costs related to using segments in the data marketplace. Applicable when specific segments are applied in line items and associated pricing is displayed in the platform. |
| Filtered Requests | The total number of bid requests for which Microsoft Advertising did not hold an auction due to inventory quality concerns. See **Filtered Request Reason** (under **Dimensions**) for a list of the possible reasons. |
| Avg. Bid Reduction | The average bid reduction you gained on the line item. This value represents the difference (as a percentage) between your bid and the actual media cost you paid for the impression you won (e.g., due to bid reduction). This value is only valid for RTB bidding (i.e., not Managed). Currently, this value is not accurately calculated for line items which have the **Pay Per** field set to "View" and **Buying Strategy** set to "RTB". |
| Clearing Event Units | The total number of events purchased (for the associated Clearing Event). When buying a Clearing Event other than impression (e.g., viewable impressions), the number of billed events will be less than the number of impressions. |
| Clearing Event Buyer Media Cost eCPM | The total media cost per 1000 events (for the associated Clearing Event). |
| Pub: Salesperson (reporting label) | The sales person providing for reporting on the publisher. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, feature cost, data segment cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Profit eCPM | Profit per thousand impressions.<br>**Note**: This new field defines "profit" as booked revenue minus total cost. |
| Profit eCPC | Profit per click.<br>**Note**: This new field defines "profit" as booked revenue minus total cost. |
| Profit eCPA | Profit per conversion.<br>**Note**: This new field defines "profit" as booked revenue minus total cost. |
| Profit Margin | Profit divided by Booked Revenue. |
| Network Profit | The sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPM | Network profit per thousand impressions. |
| Network Profit eCPC | Network profit per click. |
| Network Profit eCPA | Network profit per conversion. |
| Network Profit Margin | Network profit margin. |
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
| Segment Data Costs Buying Currency | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the buyer used to purchase the inventory. |
| Segment Data Costs Selling Currency | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the seller used to sell the inventory. |

**Seller types**

| Name | Definition |
|---|---|
| direct | When you purchased inventory from a seller with whom you have a managed relationship. |  
| real time | When you purchase inventory from a seller on the open exchange. |  
| unknown | The seller type is not identifiable. You shouldn't see this turn up in your reports. If you do, please contact [Microsoft Advertising support](https://help.xandr.com/) |  

**Revenue types**

| Name | Description |
|---|---|
| No Payment |  |
| Flat CPM | A flat payment per 1000 impressions. |
| Cost plus CPM | Cost (what you spend on inventory) plus an extra CPM. |
| Cost plus margin | Cost (what you spend on inventory) plus a percentage of what you spend. |
| CPC | A flat payment per click. |
| CPA | A flat payment per conversion. |
| Revshare | A payment on a revshare basis (CPC or CPA). |
| Estimated CPM | The estimated payment per 1000 impressions. |
| CPVM | A flat payment per 1000 viewable impressions. |

**Payment types**

| Name | Description |
|---|---|
| No Payment |  |
| CPM | Payment per 1000 impressions. |
| CPC | Payment per click. |
| CPA | Payment per action. |
| Owner CPM | Publisher is paid on a CPM basis. |
| Owner revshare | Publisher is paid on a Revshare basis (CPC or CPA). |
| CPVM | Payment per 1000 viewable impressions. |

**Impression types**

| Value | Name | Definition |
|---|---|---|
| 1 | Blank | No creative served. |
| 2 | PSA | A public service announcement served because no other creative was eligible. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 4 | Default | A default creative served because no line item bid or no other creative was eligible. |
| 5 | Kept | One of your managed advertisers served a creative. |
| 6 | Resold | The impression was sold to a third-party buyer. |
| 7 | RTB | Your creative served on third-party inventory. |
| 8 | PSA Error | A public service announcement served due to a timeout issue. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |
| 11 | Insertion | Your creative served on third-party inventory where it persists across page-loads and sessions. |

**Bid types**

> [!NOTE]
> The term "give up" is appended to the bid types below if the valuation of the line item for that impression falls below the venue's "give up price".

| Name | Definition |  
|---|---|
| Manual | Base CPM bid. Only applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP. |  
| Learn | Learn bid. Only applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized. |  
| Optimized | Optimized bid. Only applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized. |  
| Unknown | The node was in an unknown optimization phase. |  
| Optimized give up | The bid was "Optimized", but was below the venue's "give up" price. |  
| Learn give up | The bid was "Learn", but was below the venue's "give up" price. |  
| Manual give up | The bid was "Manual", but was below the venue's "give up" price. |  

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium** \>  **Analytics** \>  **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using
    > only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under  **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Working with Line Items](working-with-line-items.md)
- [Reporting Labels](reporting-labels.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Bidding Priority](bidding-priority.md)
- [Give Up Price](bidding-priority.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Analytics Reporting](analytics-reporting.md)
