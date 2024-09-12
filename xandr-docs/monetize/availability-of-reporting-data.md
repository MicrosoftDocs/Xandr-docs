---
title: Microsoft Monetize - Availability of Reporting Data
description: Learn how and when Reporting Data is accessible to you. Also go through what are the pointers for scheduled reports and how many saved reports you can view in the UI.
ms.date: 10/28/2023
---


# Microsoft Monetize - Availability of reporting data

This page describes how, when, and for how long reporting data is or becomes available to you.

> [!IMPORTANT]
> If you are noticing any latency in the availability of your reporting data, first check if there are any known outages at [Xandr Status](https://status.xandr.com/).

## Data processing

Reporting data is typically available in the UI and API within 3 to 4 hours for hourly aggregated reports, and within 6 hours after midnight UTC for daily reports. All data for a given hour is aggregated across the entire platform at once, so timing for most reports isn't specific to certain objects or fields. However, a few reports follow different schedules.

## Events (clicks, conversions, video completions)

Since clicks, conversions, video completions, and other events occur after the initial impressions that caused them, they can appear in later hours of a report's data. As a result, you may see hours in your reports that only contain events. The impressions associated with these events will have occurred in earlier hours of the report. Event data is never more than a few hours delayed.

## Data retention

The data retention period for each report is stated on that report's page in the documentation. For a list of reports, see [Reporting Guide](reporting-guide.md).

## Scheduled reports

A few facts to keep in mind about scheduled reports:

- Scheduled reports expire after 6 months. You must create a new scheduled report after 6 months.
- Scheduled reports and saved report templates cannot have a **Lifetime** or **Custom** date range.
- Scheduled reports are run in the order in which they were originally created. For example, if you create two daily reports, the daily report created first will run first each day.
- Daily reports are run and sent each day as soon as the data for the entire day (in the specified timezone) is available.
- Weekly reports are run and sent on the Monday of each week for the previous 7 days.
- Monthly reports are run and sent on the first day of each month.

## Saved reports

You can save and view up to 200 reports in the UI. To retrieve a full list of saved reports, use the API [Saved Report Service](../digital-platform-api/saved-report-service.md).

## Related topics

- [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md)
- [Dates and Times in Reporting](dates-and-times-in-reporting.md)