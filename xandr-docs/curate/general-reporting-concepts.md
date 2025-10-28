---
title: Microsoft Curate - Overview of Reporting Concepts
description: This page explains concepts around reporting system like how the system handles data, creates report requests, types of data, and delivery mechanisms.
ms.date: 10/28/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---


# Microsoft Curate - Overview of reporting concepts

This section of the Reporting Guide explains the concepts underlying our reporting system, such as:

- How our system handles dates and times in reporting data
- How to create more efficient report requests
- The types of data (dimensions and metrics) and the operations you can perform on them (filtering and grouping)
- The various delivery mechanisms for your data

## In this section

- **[Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)**: Learn how a report is run, so you can design your report requests efficiently.
- **[Transactional Reporting Options](transactional-reporting-options.md)**: Learn about the different ways to retrieve data from our systems.
- **[Dates and Times in Reporting](dates-and-times-in-reporting.md)**: How our systems handle dates and times.
- **[Report Throttling](report-throttling.md)**: A description of how our system limits the number of report requests per member and per user.
- **[Impression Counting](impression-counting.md)**: A list of media types and look-back windows.

## Report Center 

The **Report Center** is where you can view your saved and recent reports.

## Saved reports 

The **Saved reports** table includes the following columns. You can sort the table by selecting a column header.

| Column | Description |
|-------|-----|
| Name  | The name of the saved report. Select the name to run the report and open the results page. If the report fails to load, an error message appears on the **Report Center** page. |
| Report Interval | The time range used in the saved report. |
| Date Created | The date when the report was originally created. |
| Created By | The user who created the report.<br>**Note**:<br>Reports can’t currently be shared with other team members. |
| Report Type | The report type associated with the saved report.|
| Schedule |You can schedule the report to run at regular intervals by adjusting this setting. The schedule updates automatically after you make your selection.|
| Expiry |Saved and scheduled reports expire after six months. After the expiration date, you can’t save edits or apply scheduling. To reuse the report configuration, run the report and save the results as a new copy.|
| Edit |Select this button to open the report builder. The report builder lets you modify report dimensions, metrics, and filters.|
| Delete |Select this button to delete the saved report.<br>**Note**:<br>Deleted reports can’t be restored.|

You can filter the list to show only scheduled reports. Select the filter options from the **Report Center** header.
You can search for saved reports by name using the search bar in the upper-right corner of the screen.
Select the **New report** button to go to the report type selection screen.

## Recent reports

The **Recent reports** tab displays reports that were run in the last 72 hours, allowing you to revisit them.

The Recent reports table includes the following columns. You can sort the table by selecting a column header.

| Column | Description |
|-------|-----|
|Name|The name of the saved report. Select the name to run the report and open the results page. If an error occurs while loading the report, a notification appears on the **Report Center** page.|
|Report Interval |The time range used in the saved report.|
|Date Created |The date when the report was originally created.|
|Created By|The user who created the report.<br>**Note**:<br> Recent reports are visible only to the user who created them.|
|Report Type|The report type associated with the saved report.|
|Status|The current status of the report. The status can be **Ready** (the report is available to view) or **Waiting** (the results are still being generated).|
|Download|Select this icon to download the report in one of the following formats: XLSX, CSV, Excel/TSV, or JSON.|

### Report type screen

After selecting **New report**, you can choose a report type. A summary description is provided for each type to help you understand its scope. You can search for a report type by name or description. Select **Create new report** to open the corresponding report builder screen.

### Report Builder Screen

The **Report Builder** screen lets you select dimensions (data categories), metrics (quantitative values), and filters (data scope). You can search for dimensions and metrics using their respective search bars. Select the checkbox next to an item’s name to include it in the report.
The [Curator Analytics Report](curator-analytics-report.md) groups dimensions and metrics by category, making it easier to find and bulk-select related fields.
You can select the data date range from the leftmost option below the report name. For convenience, several predefined time ranges are available. Next to the date range selector is the **Date** grouping option, that lets you view data as cumulative totals or broken down by hour, day, or month.

You can apply filters by selecting the button next to the **Date grouping** option. This opens a side panel where you can choose a dimension to filter. After selecting a dimension, a list of filterable values appears. Select values by clicking their rows. You can include or exclude the selected values in your filter.

There are two ways to apply filters:

- Manual selection: Select individual values from the list.
- Bulk add by ID: Paste a comma-separated list of object IDs into the text box, then confirm by selecting one of the available options below it.
  
IDs can also be extracted automatically from within parentheses. This is especially useful when copying and pasting object IDs from other parts of the user interface, such as line item targeting.

Select the Settings (gear) icon to open Advanced options, which include the following:

- Currency – Specifies the currency used to display monetary metrics.

- Timezone – Defaults to the member’s setting but can be changed as needed.
<br>**Note**:<br> Time zone support is available only for report types that include hourly data.

- Include IDs as a separate column – When selected, the name and ID appear in separate columns for applicable dimensions. When cleared, the dimension is displayed in a single column, with the ID shown in parentheses after the name.

### Running a report 

From the **Report Builder** screen, you can run a report in the following ways:

- Select Run report – Runs the report and opens the results on the **Report Results** screen.

- Right-click options for running a report:

  - Run in background and email results – Runs the report in the background and automatically emails the results to the specified email address.
  - Run in background and download results – Runs the report in the background and automatically prompts your browser to download the report when it’s ready.

### Report Results Screen

The **Report Results** screen displays the report data in a table, with totals shown at the bottom. You can resize and sort columns using the column headers.

The report time period, date grouping, filters, and advanced settings can be modified in the same way as in the **Report Builder** screen. Changes take effect when you select **Run report**.

You can update dimensions and metrics by selecting **Edit** on the right side of the page, which opens a side panel for modifying selections.

To refresh the data, select the **Reload data** button to pull the latest available data that matches the report configuration. Use the **Download** button (downward arrow icon) to export the report in supported formats.

To save the report, select **Run & save report** from the button next to **Run report**. You can then add scheduling information if needed.

To rename the report, select the **pencil icon** next to the report title at the top of the results page.
