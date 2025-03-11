---
title: Microsoft Invest - Offline Attribution Report
description: In this page, learn what is Offline Attribution report and how it helps you track your line item's offline sales performance.
ms.date: 10/28/2023
---

# Microsoft Invest - Offline attribution report

The Offline Attribution report lets you track your line item's offline sales performance. This report is only available for Microsoft Invest clients that have **Offline Attribution** enabled on their line items.

## Time frame

NCS data uses the time zone(s) where offline sales take place, so you don't need to make a time zone selection when generating this report.

### Time ranges

Time ranges define the time period of the data extracted for the report. Here are the ranges available for this report:

- Custom
- Last 7 Available Days
- Last 14 Available Days
- Last 30 Available Days
- Last 365 Days

> [!NOTE]
> When making a **Range** selection, note that NCS reports requested between Sunday and Tuesday won't include NCS data from the current week.

### Intervals

Intervals determine how your data is grouped into rows in the report response.

> [!NOTE]
> The **Interval** selection for this report must be **Daily**.

## Data retention period

This report can retrieve data from the last 100 days.

## Dimensions

The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.

Some dimensions have *attributes*. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: *Dimension_Name:Attribute_Name*.

| Dimension | Filter? | Description |
|--|--|--|
| Insertion Order | Yes | The name and ID of the insertion order under which the impression was purchased. For more information about insertion orders, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| Line Item | Yes | The ID and name of a line item. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Split | Yes | The name and ID of a programmable split. For more information about programmable splits, see [Working with Programmable Splits](working-with-programmable-splits.md). |
| Flight<br> - Start Date<br> - End Date | No | The line item flight under which the impression was purchased. You can optionally choose to show flight start and end dates in your report. For more information about programmable splits, see [Working with Programmable Splits](working-with-programmable-splits.md). |
| Day | No | The day on which NCS generated the report. The date displayed for this dimension will match the date displayed for the Analysis End Date. |
| Analysis Start Date | No | The first day of the purchase interval being reported for each cohort. |
| Analysis End Date | No | The last day of the purchase interval being reported for each cohort. |
| Frequency Type | No | The reporting frequency selected for this line item or split. |
| Lookback | No | The lookback window selected for this line item or split. |
| Product | No | The product selection name used to describe the product or products being reported. |
| Analysis Rejection Reason | No | The error that identifies which of the requirements for measurement weren't met. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Metric | Description |
|--|--|
| Imps | The total number of impressions served. |
| Clicks | The total number of clicks recorded. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs: budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Booked Revenue | The revenue received from the advertiser. |
| All Outlet Adjusted Penetration (%) | The penetration percentage for the product, category, or brand during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US.<br>**Note:** *Penetration* measures brand or category popularity. It is calculated by dividing the number of people who've purchased a specific brand or category of goods at least once in a given time period by the size of the relevant market's total population. |
| All Outlet Adjusted Number Of Trips | The number of trips to the store by households that have been during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US. |
| All Outlet Adjusted Total Spend | The number of dollars spent by households on the product, category, or brand during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US. |
| Media Cost | The cost to the buying member for this inventory. |
| Imps (viewed) | Impressions that are considered viewable as defined by the Interactive Advertising Bureau (IAB): For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must render on a screen. |
| 100% Complete | For a video creative, the number of times the video creative was viewed to completion. |

## Run your report

Follow these steps to run the report:

1. Select **Reporting \> Advertiser Reports** from the dropdown menu (depending on how your account has been configured).
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
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Select **Run report** to send your report request.

## Related topics

- [enabling sales impact with nielsen catalina solutions](enabling-sales-impact-with-nielsen-catalina-solutions.md)
- [activate nielsen sales impact for a line item](activate-nielsen-sales-impact-for-a-line-item.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
