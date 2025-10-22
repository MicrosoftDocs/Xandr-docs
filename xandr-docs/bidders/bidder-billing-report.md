---
title: Bidder Billing Report
description: Explore this article to understand the Bidder Billing report, including its metrics, filters, delivery, dimensions, and how to run a report.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder Billing report

The **Bidder Billing Report** is where bidders can pull billing/financial data, and drill down into very specific dimensions.

The API documentation for the **Bidder Billing Report** is located [here](bidder-billing-report-api.md).

## Basic

| Field | Description/Options |
|:---|:---|
| **Type** (drop-down menu) | - [Platform Buyer Report](platform-buyer-report.md) (default)<br> - Bidder Billing Report<br> - [Bidder Bid Error Report](bidder-bid-error-report.md)<br> - [Completed Creatives Audits Report](completed-creatives-audits-report.md) |
| **Range** (drop-down menu) | - Custom<br> - Current Hour<br> - Today<br> - Yesterday<br> - Last 48 Hours<br> - Last 7 Days<br> - Month to Date<br> - Month to Yesterday<br> - Last Month |
| **Interval** (drop-down menu) | - Hourly<br> - Daily<br> - Monthly<br> - Cumulative |
| **Time Zone** (drop-down menu) | Select the appropriate time zone. |

## Metrics

Select the **metrics** you want to be displayed in the report. Click the **Edit** button on the right to select/deselect.

| Metric | Definition |
|:---|:---|
| **Imps** | The total number of impressions bought. |
| **Buyer eCPM** | The buyer's cost per impression expressed in eCPM. |
| **Buyer Media Cost** | The amount the buyer pays for the cost of media. |

## Filters

Select the **filters** you want to be used to generate the report. Click the **Edit** button on the right to select/deselect.

| Filter | Definition |
|:---|:---|
| **Buyer Member** | Select to filter by the internal ID of the buyer member. |
| **Deal** | Select to filter by specific Deals set up between the Bidder and Seller. |
| **Seller Member** | Select to filter by internal ID of the seller member. |
| **Publisher** | Select to filter by internal ID of the publisher, which is one level more detailed than seller member. |
| **Buying Currency** | Select to filter by the buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| **Impression Type** | Select to filter by the type of impression served. Possible values:<br> - 1 = blank<br> - 2 = PSA<br> - 3 = default error<br> - 4 = default<br> - 5 = kept<br> - 6 = resold<br> - 7 = RTB<br> - 8 = PSA resulting from a default error<br> - 9 = external impression<br> - 10 = external click |
| **Country** | Select to filter by the country or region the impression originated from. |

## Dimensions

**Include IDs as separate column** (checkbox to the left).

Select the **dimensions** you want to be used to generate the report. Click the **check box** on the left to select/deselect.
Select **Include IDs** as separate column if you would like the object ID listed as a separate column in the report.

| Metric | Description |
|:---|:---|
| **Buyer Member** | The internal ID of the buyer member. |
| **Buyer Seat Code** | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| **Buyer Seat Name** | The display name for the buyer seat code. |
| **Deal** | Deal name and ID of the deal the impression is attributed to. Further details about deals can be found in the [Deal Buyer Access Service](deal-buyer-access-service.md). |
| **Seller Member** | Internal ID and name of the seller member. |
| **Publisher** | Internal ID of the publisher, which is one level more detailed than seller member. |
| **Buying Currency** | Buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| **Impression Type** | Type of impression served. Possible values:<br> - 1 = blank<br> - 2 = PSA<br> - 3 = default error<br> - 4 = default<br> - 5 = kept<br> - 6 = resold<br> - 7 = RTB<br> - 8 = PSA resulting from a default error<br> - 9 = external impression<br> - 10 = external click |
| **Country** | The country the impression originated from. |

## Delivery

This section determines how the report will be delivered to you as well as any reports you would like to save.

Options on how to run the report (select one):

| Run now, show results in screen | Run in background, notify me when results are ready to view | Export, send results via email |
|---|---|---|
| This will display the report in the **View Report** tab of the report screen. Recommended delivery format for reports with less dimensions and/or metrics. | Report will run in the background and a pop-up will notify you when the report is complete. Access complete report from **Your Reports** tab. Recommended delivery format for reports with less dimensions and/or metrics. | Report will be sent to the email included in the text box. Use the **drop down option** to select the format of the file to be sent via email. Recommended delivery format for larger reports with lots of dimensions and/or metrics. |

Options to save the report (Select both or one of the options):

| Add to scheduled reports | Save as report template |
|:---|:---|
| If there is a report that you want every day, week, or month:<br> - Configure what you want that report to look like.<br> - Click **Add to scheduled reports**. | This allows you to configure different types of templates of reports that you plan on running frequently, or slightly modifying.<br>Enter the name of the report in the **Report Name** text box. |

## Run report

After your selections are made, click **Run Report** to run the report. The **View Report** screen will automatically be accessed, where the report results are displayed.

## Related topics

- [Reporting Screen](reporting-screen.md)
- [Platform Buyer Report](platform-buyer-report.md)
- [Bidder Bid Error Report](bidder-bid-error-report.md)
- [Completed Creatives Audits Report](completed-creatives-audits-report.md)
- [Your Reports](your-reports.md)
