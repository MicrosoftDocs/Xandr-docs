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

| Dimension | Filter? | Description |
|---|---|---|
| Insertion Order | Yes | The name and ID of the insertion order under which the impression was purchased. For more information about insertion orders, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| Line Item | Yes | The ID and name of a line item. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Campaign | Yes | The campaign that purchased this impression (doesn't apply to all advertisers) |
| Creative | Yes | The creative that served on this impression. For more information about creatives, see [Working with Creatives](working-with-creatives.md). |
| Seller | Yes | The seller of the impression |
| Publisher | Yes | The publisher who owns the inventory on which the impression occurred |
| Placement | Yes | The placement where the impression occurred |
| Impression Type | Yes | The type of impression served. Below are the 11 impression types and their definitions: <br> - **Blank** - No creative served <br> - **PSA** - A public service announcement served because no other creative was eligible <br> - **Default Error** - A default creative served due to a timeout issue <br> - **Default** - A default creative served because there were no valid bids <br> - **Kept** - Your advertiser's creative served on your publisher's site <br> - **Resold** - Your publisher's impression was sold to a third-party buyer <br> - **RTB** - Your advertiser's creative served on third-party inventory <br> - **PSA Error** - A public service announcement served due to a timeout issue or lack of a default creative <br> - **External Impression** - An impression from an impression tracker <br> - **External Click** - A click from a click tracker <br> - **Insertion** - Your creative served on third-party inventory, where it persists across page-loads and sessions. <br><br> **Note**: This impression type is currently only for Facebook News Feed creatives. |
| Media Type | Yes | The type of creative that served: <br> - Banner <br> - Interstitial <br> - Video <br> - Text <br> - Expandable <br> - Skin <br> - Facebook |
| Supply Type | Yes | The supply (inventory) type on which the impression occurred: <br> - Web <br> - Mobile Web <br> - Mobile App |
| Device Type | Yes | The type of hardware device on which the impression occurred: <br> - Desktops & Laptops <br> - Tablets <br> - Mobile Phones <br> - TV <br> - Game Consoles <br> - Set Top Box <br> - Media Players <br> - Other Devices |
| Split | Yes | Filter for the name and ID of a programmable split. For more information about programmable splits, see [Working with Programmable Splits](working-with-programmable-splits.md). |
| Domain | No | The domain on which the impression occurred |
| Size | Yes | The pixel dimensions of the served creative |
| Deal | Yes | The deal associated with the impression |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Reporting Metric | Description |
|---|---|
| Imps | The total number of impressions served |
| Clicks | The total number of clicks recorded |
| CTR (Click-Through Rate) | The ratio of clicks to impressions, expressed as a percentage |
| Measurable Imps | The total number of impressions that were measured for viewability |
| Viewed Imps | The total number of impressions that were deemed viewable as defined by the Interactive Advertising Bureau (IAB): For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must be viewable to a viewer on their screen. |
| Custom Viewable Imps | The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Microsoft Advertising account representative) |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. <br> Viewability Measurement Rate = Measurable Imps / Imps |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. <br> Viewability Rate = Viewed Imps / Measurable Imps |
| Custom Viewability Rate | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability |
| Average Viewable Duration | The average number of seconds for which the creative was in view by IAB standards <br> Average Viewable Duration = Total Viewable Duration / Viewable Imps |
| Total Viewable Duration | The total number of seconds for which the creative was in view by IAB standards |
| Video Completions | The total number of video creatives played for their entire duration |
| Video Completion Rate | The ratio of video completions to total impressions, expressed as a percentage. <br> Video Completion Rate = Video Completions / Total Impressions |
| Viewable Completion Rate | The ratio of in-view creative/impression completions to total impressions, expressed as a percentage. <br> Viewable Completion Rate = Viewable and Completed Video Impressions / Measurable Video Impressions |

## Run your report

Follow these steps to run the report:

1. Select **Reporting** > **Advertiser Reports** from the dropdown menu (depending on how your account has been configured).

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the  **Chosen** list (right).

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
