---
title: Microsoft Invest - Buyer Engagement Report
description: In this article, learn what a Buyer Engagement Report is and how you can run this report to gain insight into the viewable duration of your display and video creatives.
ms.date: 10/28/2023
---

# Microsoft Invest - Buyer Engagement report

The Buyer Engagement Report gives you insight into the viewable duration of your display and video creatives.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. Here are the ranges available for this report:

- Custom
- Yesterday
- Last 7 Days
- Last 14 Days
- Month To Yesterday
- Last 30 Days

### Intervals

Intervals determine how your data is grouped together into rows in the report response. Here are the intervals available for this report:

- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

## Data retention period

This report can retrieve data from the last five weeks.

## Dimensions

The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.

Some dimensions have *attributes*. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: *Dimension_Name:Attribute_Name*.

| Column | Type | Filter?| Description|
|---|---|---|---|
| `Buyer` | string | Yes | The name and ID of the buying member of the impressions. |
| `Advertiser` | string | Yes | The name and ID of the advertiser associated to the served impressions. |
| `Insertion Order` | string  | Yes | The name and ID of the insertion order under which the impressions were purchased. For more information about insertion orders, see Working with Insertion Orders.|
| `Line Item` | string | Yes | The name and ID of the line item under which the impression was purchased. The buy-side   hierarchy is **Line Item** > **Campaign**. |
| `Split` | string| Yes| The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the split_id (if included) will be null.|
| `Campaign` | string| Yes| The name and ID of the campaign that purchased the impressions.|
| `Creative` | string | Yes |  The name and ID of the creative served for the impression.  For impressions older than 14 months, creatives will be aggregated into one row with 0 as the   creative ID. <br> **Note**: For external click or impression trackers, creative_id will be "External Clicks" or "External Imps".|
| `Seller` | string | Yes | The name and ID of the selling member. |
| `Publisher`| string | Yes | The name and  ID of the  publisher on whose inventory the impressions were occurred. |
| `Placement`| string | Yes | The name and ID of the placement or the open slot on publisher website where the   advertiser's creative with matching specifications was served. |
| `Media Type`| string | Yes | The name and  ID of the media type associated with the creative that served on the impression. |
| `Impression Type`| string | Yes| The name and  ID for the type of impression that served (associated types in parentheses):  <br> - **1** ("Blank"): No creative served  <br> - **2** ("PSA"): A public service announcement served because there were no valid bids and no default creative was available <br> - **3** ("Default Error"): A default creative served due to a timeout issue <br> - **4** ("Default"): A default creative served because there were no valid bids <br> - **5** ("Kept"): Your advertiser's creative served on your  publisher's site <br> - **6** ("Resold"): Your publisher's impression was sold to a third-party buyer <br>  - **7** ("RTB"): Your advertiser's creative served on third-party inventory <br> - **8** ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative  <br> - **9** ("External Impression"): An impression from an impression tracker <br> - **10** ("External Click"): A click from a click tracker <br> - **11** ("Insertion"): Your creative served on third-party inventory, where it persists across page-loads and sessions. This impression type is currently only for Facebook News Feed creatives. |
| `Device Type` | string | Yes | The type of device on which the impression was served. Possible values: <br>     - Desktops & Laptops <br>  - Tablets  <br> - Mobile Phones  <br> - TV  <br>  - Game Consoles  <br> - Set Top Box <br> - Media Players <br> - Other Devices |
| `Domain` | string | No | The ID of the domain   on which the impression was occurred. |
| `Deal`| string | Yes | The name and ID of the deal with which the served impression is associated. <br> - For more information about deals you have negotiated with sellers, see Deal Buyer Access Service. |
| `Size` | string | Yes | The size of the creative that was served.|
| `Supply Type` | string | Yes | The supply (inventory) type on which the impression occurred:  <br> - Web <br> - Mobile Web <br> - Mobile App |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Description|
|---|---|---|---|
| `Imps` | int | Imps | Your line item's total number of impressions.|
| `Clicks`| int | Clicks | Your line item's total number of clicks.|
| `CTR (Click-Through Rate)`| double| Clicks/Imps| The click-through rate – the ratio of clicks to impressions, expressed as a percentage.|
| `Measurable Imps`| int | N/A |The total number of impressions that were measured for viewability.|
| `Viewed Imps` | int | N/A | The total number of impressions that were deemed viewable as defined by the   Interactive Advertising Bureau (IAB): For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must be viewable to a viewer on their screen. |
|`Custom Viewable Imps` | int | N/A| The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Microsoft Advertising account representative).|
|`Viewability Measurement Rate`| double | Measurable Imps / Imps | The percentage of impressions measured for viewability out of the total number of impressions. |
|`Viewability Rate` | double | Viewed Imps / Measurable Imps| The percentage of impressions that were viewable out of the total number of impressions measured for viewability. |
|`Custom Viewability Rate` |double| Custom Viewable Imps / Imps| The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability.|
|`Average Viewable Duration`| double | Total Viewable Duration / Viewable Imps | The average number of seconds for which the creative was in view by IAB standards. |
|`Total Viewable Duration` | int | N/A | The total number of seconds for which the creative was in view by IAB standards.|
|`Video Completions`| double| N/A| The total number of video creatives played for their entire duration|
|`Video Completion Rate`| double| Video Completions / Total Impressions| The ratio of video completions to total impressions, expressed as a percentage. |
|`Viewable Completion Rate`| double| Viewable and Completed Video Impressions/ Measurable Video Impressions| The ratio of in-view creative/impression completions to total impressions, expressed as a percentage.|

## Run your report

Follow these steps to run the report:

1. Select **Reporting** > **Advertiser Reports** from the dropdown menu (depending on how your account has been configured).

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser.
    - **Run in background, notify me when results are ready to view**: A pop-up notification will let you know when the report is ready to view or download.
    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under Name this report (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the Your Reports screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.

1. Select **Run report** to send your report request.

## Related topic

[Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
