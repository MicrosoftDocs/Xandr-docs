---
title: Microsoft Monetize - General Reporting Concepts
description: Explore reporting concepts, system's date/time handling, efficient report requests, data types/operations, and diverse data delivery methods.
ms.date: 10/28/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - General reporting concepts

This section of the Reporting Guide explains the concepts underlying our reporting system, such as:

- How our system handles dates and times in reporting data
- How to create more efficient report requests
- The types of data (dimensions and metrics) and the operations you can perform on them (filtering and grouping)
- The various delivery mechanisms for your data

In This Section

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
| Created By | The user who created the report.<br>[!Note:]<br>Reports can’t currently be shared with other team members. |
| Report Type | The report type associated with the saved report.|
| Schedule |You can schedule the report to run at regular intervals by adjusting this setting. The schedule updates automatically after you make your selection.|
| Expiry |Saved and scheduled reports expire after six months. After the expiration date, you can’t save edits or apply scheduling. To reuse the report configuration, run the report and save the results as a new copy.|
| Edit |Select this button to open the report builder. The report builder lets you modify report dimensions, metrics, and filters.|
| Delete |Select this button to delete the saved report.[!Note:] Deleted reports can’t be restored.|
