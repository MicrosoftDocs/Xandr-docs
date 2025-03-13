---
title: Finance - Reconciling Your Invoice with Reporting
description: In this article, learn how to confirm charges on your invoice using reports, and understand what the cost of media, buyer auction service fee, creative overage fee and other charges are.
ms.date: 10/28/2023
ms.custom: finance
---

# Finance - Reconciling your invoice with reporting

You can log into the UI and use the Buying Billing Report and Selling Billing Report to assess and confirm charges you see on your invoice. This page explains how to run the report and find the desired invoice
fields.

For a detailed explanation of the fields on your invoice, see [Understanding your Invoice](understanding-your-invoice.md).

> [!NOTE]
> For Sellers looking for information on how to reconcile your Seller Statement with reporting, see [Reconciling your Seller Statement with Reporting](reconciling-your-seller-statement-with-reporting.md).

## Run the buyer billing report

In the UI, run the Buying Billing Report to confirm the cost of media, buyer auction service fee, managed ad serving fee, and creative overage fee amounts on your invoice.

On the Member reporting screen, select **Buying Billing Report** under **Type**. Enter the **Range**, **Interval** (how the data will be
grouped), and **Timezone** and then click **Run report**.

> [!NOTE]
> Certain fields, such as some fee information for unmet minimums, and log-level data are not currently available in the reporting.

## Confirm invoice values (buyers)

After running the report, you can confirm the values for each of the fields below.

## Cost of media

This is the amount to be paid to Microsoft Advertising for media purchases. You can find this value in your report in the row that displays RTB impressions that were not cleared direct, where Cleared Direct is zero and Impression Type is RTB. The values in the Imps and Media Cost columns in the report should match the values in the Billable Units and Amount columns on your invoice.

## Buyer auction service fee

This is the fee charged for:

- impressions bought from third parties (where Cleared Direct is "1"), typically Google or Yahoo!
- disclosed Buyer deductions (where Cleared Direct is "0")

It is charged in addition to your media cost. For more information, see [Buyer Auction Service Charge Mechanics](buyer-auction-service-charge-mechanics.md). You can find this value in your report in the Auction Service Fees column. The total at the bottom of the column in the report should match the value in the Amount column on your invoice.

## Viewable marketplace

For a buyer who wants to only pay for impressions that are viewable, Microsoft Advertising offers the **Viewable Marketplace**. For more details, see the "Guaranteed Outcomes" topic within the UI's Help Center. Microsoft Advertising provides the following details on the invoice if you are using the Viewable Marketplace:

- the type of Viewable Marketplace that was purchased

- the number of billable units ("views") bought

- the Cost of Media purchased via the Viewable Marketplace

The Buying Billing Report is to be used to reconcile the invoice. Before running the report, select **Clearing Event Units** (under **Metrics**) and **Clearing Event** (under **Dimensions**). This will ensure that the report contains the relevant information.

## Creative overage fee

This is the amount charged for serving creatives that are over the maximum size specified in your Microsoft Advertising contract. For each oversized creative, the difference between (a) the size of the creative and (b) the maximum creative size outlined in your contract is multiplied by (c) the number of impressions where the creative served, and then by (d) the bandwidth charge in your contract is equal to the creative overage fee we charge each month.

> [!NOTE]
> (b) the **maximum creative size** is in **KB** whereas (d) the **bandwidth charge** is in **GB**. When converting from GB to KB, **divide by 976,563** because Microsoft Advertising uses the **kibibyte** metric for KB.

For example, let's say the maximum creative size in your contract is (b) 40KB, you have a (a) 60KB creative that served (c) 100,000 times, and your bandwidth fee is (d) $2.50 per GB (which converts to 976,563 KB).

Your creative overage fee would be calculated as follows: [ [ (a) 60KB - (b) 40KB ] x 100,000 imps ] x [ (d) $2.50 / 976,563 KB ] =
$5.12

You can find this value in your report in the Creative Overage Fees column. The total at the bottom of the column in the report should match the value in the Amount column on your invoice.

## List of reports to use to reconcile invoice charges

The table below lists charges that can commonly appear on your invoice and which billing report to use to reconcile those charges. For some charges, you may need to consult your contract with Microsoft Advertising.

| Charge Description | Report to Use |
|---|---|
| Completes - Custom/Standard Video | Buyer Billing Report |
| Views - Custom/Standard Display | Buyer Billing Report |
| Booked Revenue | Buying Billing Report |
| Buyer Auction Service Charge | Buying Billing Report |
| Buyer Auction Service Fee | Buying Billing Report |
| Click Tracker Fees | Buying Billing Report |
| Cost of Media | Buying Billing Report |
| Cost of Media Net Fees | Buying Billing Report |
| Creative Hosting (Video) | Buying Billing Report |
| Creative Overage Fee | Buying Billing Report |
| Foreign Exchange Fee | Buying Billing Report |
| Imp Tracker Fees | Buying Billing Report |
| (Managed) Ad Serving Fee | Buying Billing Report (and the Selling Billing Report if you have access to it) |
| Ad Serving (Hosted Video) | Buying Billing Report (and the Selling Billing Report if you have access to it) |
| Ad Serving (Non-Hosted Video) | Buying Billing Report (and the Selling Billing Report if you have access to it) |
| Creative Audit Fee | Completed Creative Audits Report |
| Priority Creative Audit Fee | Completed Creative Audits Report |
| Bidder Service Fee | Consult your contract with Microsoft Advertising. |
| Console Service Fee | Consult your contract with Microsoft Advertising. |
| Finance Charge | Consult your contract with Microsoft Advertising. |
| Log Level Data | Consult your contract with Microsoft Advertising. |
| Onboarding Fee | Consult your contract with Microsoft Advertising. |
| Per Look Fee | Consult your contract with Microsoft Advertising. |
| Seller Rev Share Minimum | Consult your contract with Microsoft Advertising. |
| Service Fee | Consult your contract with Microsoft Advertising. |
| Unmet Min. Service Fee (Buyer auction serv. fee) | Consult your contract with Microsoft Advertising. |
| Unmet Minimum Fee | Consult your contract with Microsoft Advertising. |
| Unmet Minimum Service Fee (Spend) | Consult your contract with Microsoft Advertising. |
| Unmet Minimum Volume | Consult your contract with Microsoft Advertising. |
| User ID Mapping | Consult your contract with Microsoft Advertising. |
| Cost of Data | Data Usage Report |
| Data Sales Tax | Data Usage Report |
| Seller Auction Service Fee | Selling Billing Report |
| Cost of Segment Data | Data Usage Report |

## Related topics

- [Understanding your Invoice](understanding-your-invoice.md)
- [Billing and Settlement FAQ](billing-faq.md)
