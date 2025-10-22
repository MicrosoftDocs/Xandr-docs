---
title: Bidder Bid Error Report
description: Explore this article to understand the Bidder Bid Error report, including its metrics, filters, delivery, dimensions, and how to run a report.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder Bid Error report

The **Bidder Bid Error Report** allows bidders to see the volume and types of bid errors that their bidders are generating when they bid.

> [!NOTE]
> The errors listed in the Bidder Bid Error Report are considered **pre-auction** errors, meaning these are bids reject prior to the start of the auction for a specific impression.

This is meant to be a helpful troubleshooting tool. Here are a few suggestions:

- Group your results by the **actual error**, to see what your most common errors are.
- If you are troubleshooting a specific area, add dimensions like **Seller Member**, **Ad Profile**, or **Creative** to understand exactly which options and which creatives are generating that error.
- Group the results by **Deal** – to troubleshoot errors for a specific deal.

> [!NOTE]
> The API documentation for the **Bidder Bid Error Report** is located [here](bidder-bid-error-report-api.md).

## Basic

| Field | Description/Options |
|:---|:---|
| **Type** (drop-down menu) | - [Platform Buyer Report](platform-buyer-report.md) (default)<br> - [Bidder Billing Report](bidder-billing-report.md)<br> - Bidder Bid Error Report<br> - [Completed Creatives Audits Report](completed-creatives-audits-report.md) |
| **Range** (drop-down menu) | - Custom<br> - Current Hour<br> - Today<br> - Yesterday<br> - Last 48 Hours<br> - Last 7 Days<br> - Month to Date<br> - Month to Yesterday<br> - Last Month |
| **Interval** (drop-down menu) | - Hourly<br> - Daily<br> - Monthly<br> - Cumulative |
| **Time Zone** (drop-down menu) | Select the appropriate time zone. |

## Metrics

Select the **metrics** you want to be displayed in the report. Click the **Edit** button on the right to select/deselect.

| Metric | Definition |
|:---|:---|
| **Error Count** | The amount of errors logged on the Xandr platform over the timeframe selected (a randomly selected set of 1% of the errors multiplied by 100 to account for the sampling). |

## Filters

Select the **filters** you want to be used to generate the report. Click the **Edit** button on the right to select/deselect.

| Filter | Definition |
|:---|:---|
| **Buyer Member** | Select to filter by the Buyer Member who is impacted by the error. |
| **Deal** | Select to filter by the ID of the deal impacted by the error (if Deal ID = 0 no deal was involved). |
| **Creative Category** | Select to filter by the classification assigned to both brands and creatives impacted by the error. |
| **Seller Member** | Select to filter by the Seller Member who is impacted by the error. |
| **Publisher** | Select to filter by the ID of the publisher, which is one level more granular than Seller Member. |
| **Brand** | Select to filter by the brand registered in the Xandr system and associated with the creative that is impacted by the error. |
| **Creative Size** | Select to filter by the size of the creative impacted by the error. |
| **Error** | Select to filter by the specific error that occurred and was logged and the error message that describes the error. More details on specific bid errors can be found [here](bid-error-codes.md). |
| **Language** | Select to filter by the name and ID of the language. |
| **Technical Attribute** | Select to filter by the feature of the creative such as whether it is an image, flash, video, is expandable, etc. impacted by the error. |

## Dimensions

**Include IDs as separate column** (checkbox to the left).

Select the dimensions you want to be used to generate the report. Click the **check box** on the left to select/deselect. Select **Include IDs** as separate column if you would like the object ID listed as a separate column in the report.

| Dimensions | Definitions |
|:---|:---|
| **Buyer Member** | The Buyer Member who is impacted by the error. |
| **Buyer Seat Code** | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| **Buyer Seat Name** | The display name for the buyer seat code. |
| **Deal** | The ID of the deal impacted by the error (if Deal ID = 0 no deal was involved). |
| **Creative** | The Creative ID associated with the Buyer Member that is impacted by the error. |
| **Creative Category** | A classification assigned to both brands and creatives impacted by the error. |
| **Seller Member** | ID and name of Seller Member who is impacted by the error. |
| **Publisher** | The ID of the publisher, which is one level more granular than Seller Member. |
| **Brand** | Brand registered in the Xandr system and associated with the creative that is impacted by the error. |
| **Ad Profile** | The Ad Profile ID & name of the Seller Member impacted by the error. |
| **Creative Size** | Size of the creative impacted by the error. |
| **Error** | Specific error that occurred and was logged and the error message that describes the error. More details on specific bid errors can be found [here](bid-error-codes.md). |
| **Language** | Name and ID of the language. |
| **Technical Attribute** | The feature of the creative such as whether it is an image, flash, video, is expandable, etc. impacted by the error. |

### Delivery

This section determines how the report will be delivered to you as well as any reports you would like to save.

Options on how to run the report (select one):

| Run now, show results in screen | Run in background, notify me when results are ready to view | Export, send results via email |
|---|---|---|
| This will display the report in the **View Report** tab of the report screen. Recommended delivery format for reports with less dimensions and/or metrics. | Report will run in the background and a pop-up will notify you when the report is complete. Access complete report from **Your Reports** tab. Recommended delivery format for reports with less dimensions and/or metrics. | Report will be sent to the email included in the text box. Use the drop down option to select the format of the file to be sent via email. Recommended delivery format for larger reports with lots of dimensions and/or metrics. |

Options to save the report (Select both or one of the options):

| Add to scheduled reports | Save as report template |
|:---|:---|
| If there is a report that you want every day, week, or month:<br> - Configure what you want that report to look like.<br> - Click **Add to scheduled reports**. | This allows you to configure different types of templates of reports that you plan on running frequently, or slightly modifying.<br>Enter the name of the report in the **Report Name** text box. |

## Run report

After your selections are made, click **Run Report** to run the report. The **View Report** screen will automatically be accessed, where the report results are displayed.

## Related topics

- [Bid Error Codes](bid-error-codes.md)
- [Reporting Screen](reporting-screen.md)
- [Platform Buyer Report](platform-buyer-report.md)
- [Bidder Billing Report](bidder-billing-report.md)
- [Completed Creatives Audits Report](completed-creatives-audits-report.md)
- [Your Reports](your-reports.md)
