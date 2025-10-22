---
title: Create a New Report
description: Access Reports tab, input metrics, set panel options (dimension, primary metric, group by, trend lines, sort), and use filters for thorough analysis.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Create a new report

Use the **Reports** tab to create custom reports. As you enter metrics, the report automatically updates based on the selected criteria.

**Dimension** and **Primary Metric** are the only two required fields to run a report.

1. On the **Reports** page, in the **Configuration** panel, specify the report's basic configuration.
   1. In the **Dimension** field, select the primary data you want to analyze (e.g., Product or Advertiser). This determines the available primary metrics.
   1. If you have selected a numeric dimension (e.g., a date), select the date interval or numeric increment for the dimension (e.g.,Daily).
   1. In the **Primary Metric** field, select the main component that you want to report on. This determines the available secondary metrics.
   1. In the **Secondary Metric** area, select the secondary component against which you're comparing the dimension. You can't select the same option for the primary and secondary metric.
   1. In the **Group By** field, select an option by which to segment primary or secondary metric values. For numeric options, select a date or an increment for the numeric display range on the X-axis. In the bar chart view, primary metric groups appear as different colored stacked segments on each bar. Secondary metric groups appear as multiple colored dot anchors for each group.
   1. In the **Trend Lines** field, select the trend line that you want to show and select **Update**.
   1. In the **Sort** field, select a sort option (**Primary Metric** or **Dimension**, ascending or descending) to determine the order in which data appears on the chart or graph.
1. In the **Dimension Filters** panel, select dimension filters by selecting the text next to the filter name, selecting a value, and selecting **Update**.
1. In the **Dimension Filters** panel, set the **Include Zero Values** field to **Yes** or **No** to include or exclude **zero** values.
1. In the **Metric Filters** panel, in the **Time Period** field, specify the date range that you want to analyze.
1. In the **Metric Filters** panel, specify any additional components that restrict the set of analyzed primary and secondary metric values. This is accomplished by selecting a filter, selecting its value, and selecting **Update**, or by adjusting the slide bar.

## Related topics

- [Anatomy of the Reports Tab](anatomy-of-the-reports-tab.md)
- [Compare Two Data Sets](compare-two-data-sets.md)
- [Save and Share a Report](save-and-share-a-report.md)
- [Open and Edit an Existing Report](open-and-edit-an-existing-report.md)
- [Schedule a Report to be Sent](schedule-a-report-to-be-sent.md)
- [Modify a Report's Schedule](modify-a-report-s-schedule.md)
- [Export a Report](export-a-report.md)
- [Reporting Options for Dimension, Primary, and Secondary Metrics](reporting-options-for-dimension-primary-and-secondary-metrics.md)
