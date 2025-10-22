---
title : Completed Creatives Audits Report
description : This page discusses about Completed Creative Audits Report and how it allows bidders to see why your creative was audited, and how many creatives were audited over a period of time.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Completed creatives audits report

The **Completed Creative Audits Report** allows bidders to see why your
creative was audited, and how many creatives were audited over a period
of time.

> [!NOTE]
> The API documentation for the **Completed Creatives Audits Report** is located [here](completed-creative-audits-report.md).

## Basic

| Field                      | Description/Options                                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Interval** (drop-down menu)  | - Hourly <br> - Daily <br> - Monthly <br> - Cumulative                                                                                 |
| **Range** (drop-down menu)     | - Custom <br> - Current Hour <br> - Today <br> - Yesterday <br> - Last 48 Hours <br> - Last 7 Days <br> - Month to Date <br> - Month to Yesterday <br> - Last Month       |
| **Time Zone** (drop-down menu) | Select the appropriate time zone.                                                                               |
| **Type** (drop-down menu)      | - [Platform Buyer Report](platform-buyer-report.md) (default) <br> -  [Bidder Billing Report](bidder-billing-report.md) <br> - [Bidder Bid Error Report](bidder-bid-error-report.md) <br> - Completed Creatives Audits Report |

## Metrics

Select the **metrics** you want to be displayed in the report. Click
the **Edit** button on the right to
select/deselect.

| Metric           | Definition                                                |
|------------------|-----------------------------------------------------------|
| **Audits Completed** | The number of audits completed in the grouping specified. |
| **Audit Fees**       | The total fees for audits in the grouping specified.      |

## Filters

Select the **filters** you want to be used to generate the report. Click
the **Edit** button on the right to select/deselect.

| Filter       | Definition                                                                                                                                                                                                                                                   |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Audit Reason** | Select to filter by the the type of audit submission. This will be either "Initial" or "Reaudit". <br>- Initial = First submission of the creative to Audit. <br> - Reaudit = Any re-submissions of a creative for audit after the initial audit that occurred on upload. |
| **Audit Type**   | Select to filter by the priority of the audit. Allowed values: <br> - `1`: Standard <br> - `2`: Priority                                                                                                                                                                       |
| **Buyer Member** | Select to filter by the ID of the member whose creative was audited.                                                                                                                                                                                         |
| **Creative**     | Select to filter by ID of the creative that was audited.                                                                                                                                                                                                     |

## Dimensions

Select the **dimensions** you want to be used to generate the report.
Click the **check box** on the left to select/deselect.

| Dimension     | Definition                                                                                                                                                                                                                         |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Audit Reason**  | The type of audit submission. This will be either "Initial" or "Reaudit". <br> - Initial = First submission of the creative to Audit <br> - Reaudit = Any re-submissions of a creative for audit after the initial audit that occurred on upload |
| **Audit Type**    | The priority of the audit. Allowed values: <br> - `1`: Standard <br> - `2`: Priority                                                                                                                                                                 |
| **Creative**     | ID of the creative that was audited.                                                                                                                                                                                               |
| **Date of Audit** | Day on which audits were completed.                                                                                                                                                                                                |
| **Member**        | ID of the member whose creative was audited.                                                                                                                                                                                       |

## Delivery

This section determines how the report will be delivered to you as well
as any reports you would like to save.

Options on how to run the report (select one):

| Run now, show results in screen                                                                                                                       | Run in background, notify me when results are ready to view                                                                                                                                                            | Export, send results via email                                                                                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| This will display the report in the **View Report** tab of the report screen. Recommended delivery format for reports with less dimensions and/or metrics | Report will run in the background and a pop-up will notify you when the report is complete. Access complete report from **Your Reports** tab. Recommended delivery format for reports with less dimensions and/or metrics. | Report will be sent to the email included in the text box. Use the drop down option to select the format of the file to be sent via email. Recommended delivery format for larger reports with lots of dimensions and/or metrics. |

Options to save the report (Select both or one of the options):

| Add to scheduled reports                                                                                                                        | Save as report template                                                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| If there is a report that you want every day, week, or month: <br> - Configure what you want that report to look like. <br> - Click **Add to scheduled reports**. | This allows you to configure different types of templates of reports that you plan on running frequently, or slightly modifying. Enter the name of the report in the **Report Name** text box. | 

## Run report

After your selections are made, **Run Report** to run the report.
The **View Report** screen will
automatically be accessed, where the report results are displayed.

## Related topics 

- [Reporting Screen](reporting-screen.md)
- [Platform Buyer Report](platform-buyer-report.md)
- [Bidder Billing Report](bidder-billing-report.md)
- [Bidder Bid Error Report](bidder-bid-error-report.md)
- [Your Reports](your-reports.md)
