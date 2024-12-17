---
title: Microsoft Monetize - Billing and Settlement FAQ
description: This page deals with FAQs on Billing and Settlement.
ms.date: 10/28/2023
---


# Microsoft Monetize - Billing and settlement FAQ

## Finance charges

### How is the finance charge calculated?

On the date your payment is due, the finance fee percentage (specified in your Microsoft Advertising contract) is multiplied by any outstanding past due balances on the account.

> [!NOTE]
> It can take several business days for your payment to be applied. When paying by wire transfer or ACH, your bank may require a several business days to send a bank receipt. In addition, the Client Finance team may require up to 2 business days to apply your payment. It is therefore recommended that you submit payments a few days before the due date so as not to incur finance charges.

### Is the finance charge cumulative?

No. The finance charge is calculated using the amount currently past due (excluding any previously assessed finance charges).

## Credits

### I have over-paid on my account. What will happen?

If you have over-paid, Microsoft Advertising can:

- send a refund via ACH/Wire payment or
- apply this credit to an outstanding invoice of your choosing

To notify us that you have overpaid and specify whether you prefer a refund or a credit, login to our [Customer Support Portal ](https://help.xandr.com/s/login/) and navigate to the **Client Finance** section to submit a ticket. Microsoft Advertising will then ensure that your credit is applied as desired and processed as quickly as possible.

### When are credits processed? When will I receive a separate credit memo as opposed to an itemized credit on my invoice?

If you have signed a new contract with Microsoft Advertising and have completed the cutover, the cadence at which you receive credit memos will change slightly. Microsoft issues all billing documents during the billing run at the beginning of each month. This includes credit memos and invoices that have been credited and rebilled. You will receive a separate credit memo at this time. Please refer to [Understanding your credit note](../understanding-your-invoice.md#credit-note) for more information.

### How can I check my credit status?

To view the credit status of your member and parent account, click **Billing** under your member name (top right). The **Credit Status** tab will contain your outstanding balance and credit. The credit you have remaining is associated with your parent account. Your account may have more than one member associated with it. The credit limit is shared across all members under the parent account.

## Invoices

### How do I run a report that reconciles with my invoice?

You can run the Buying Billing Report in the UI to confirm the amounts on your invoice and provide more granular detail. For step-by-step instructions, see [Reconciling Your Invoice with Reporting](reconciling-your-invoice-with-reporting.md).

> [!NOTE]
> If you are an external buyer who does not use our UI, you can view data from the past 33 days in our [bidder UI](https://bidder.xandr.com/login). This data will help you analyze and compare the detailed charges you see on your invoice. If you require data older than 33 days, please contact your Microsoft Advertising representative and specify what you need.

### How is the creative overage fee calculated?

See the [relevant section of Reconciling your Invoice](reconciling-your-invoice-with-reporting.md).

### Why am I being charged a minimum when my overall spend is above my monthly minimum commitment?

You minimum monthly commitment may be met via service fees, deductions or revenue share. Cost of media purchased (a component of total spend) does not contribute to meeting your monthly minimum. Please consult your contract for details.

### How do I determine the amount that Microsoft Advertising will pay me for the inventory I sold?

In the Selling Billing Report, the **Resold Revenue** metric indicates how much Microsoft Advertising will pay you for inventory you sold to third parties.

### I would like my invoice broken out by advertiser and campaign. Is this possible?

You have the option to receive advertiser-specific and/or insertion order-specific invoices (see [Understanding Your Invoice](understanding-your-invoice.md) for more details on the information that appears in these types of invoices). To enable this option, contact your Microsoft Advertising representative. To include your advertiser's address information in the **Bill To** region of your advertiser-specific invoices, provide the information when you create an advertiser in the UI. Invoices are not currently broken out by campaign, but you can configure the Buying Billing Report to obtain this information.

### Why is there a discrepancy between what Google Ad Manager bills me for cost of media and Microsoft Advertising's reporting?

The media cost you are billed for by Google Ad Manager should not be significantly different from the Cost of Media associated with the Google Ad Manager seller in your Buying Billing Report. However, minor discrepancies (up to 10%) are to be expected. If discrepancies are larger than 10%, there may be several causes. For additional information potential causes of discrepancy and solutions, contact your Microsoft Advertising representative.

> [!NOTE]
> Microsoft Advertising does not charge you for your spend on Google Ad Manager inventory, since Google Ad Manager bills you directly for this media cost. Microsoft Advertising does charge you a **Buyer Auction Service Fee** for each impression purchased through the auction service. For more details, see [understanding-your-invoice](understanding-your-invoice.md), which describes what appears on your invoice, defines each of the fees, and addresses several FAQs related to client invoices.

### I want to be billed off of my own numbers and invoices that I send to Microsoft Advertising. Why won’t Microsoft Advertising do this?

Part of the Microsoft Advertising platform's role is to track, consolidate, and manage data associated with transactions between our buyers and sellers. We rely on this data as the single source of truth to bill and pay our clients.

## Customer account information updates

### How do I add or remove recipients from the invoice and statement distribution lists?

To request changes, login to the [Customer Support Portal](https://help.xandr.com/s/login/) and navigate to the **Client Finance** section. The distribution lists will be updated for the following month's invoice cycle.

### Can I update the billing name that appears on the invoice and have it resent?

Yes. To request an entity name change, use the [Business Support page](https://help.xandr.com/s/login/)( be sure to select "My Account Questions" as the **Request Type**) to enter your new billing name and/or address and provide a reason for the change.

## Reporting

### Is there a report in the UI that will help me to reconcile the amounts in my invoice?

Yes. You can use the Buying Billing Report to assess and confirm charges you see on your invoice. For step-by-step instructions, see [Reconciling Your Invoice with Reporting](reconciling-your-invoice-with-reporting.md).

### Why doesn't the cost of media on my invoice match the cost of media I see in reporting?

The cost of media on your invoice only includes RTB impressions that were not cleared direct. As a result, if you are using direct clearing, costs associated with that buying activity will appear elsewhere on your invoice (i.e., not under cost of media). To more accurately reconcile the cost of media shown in your reports with your invoices, locate the row in the report where **Cleared Direct** is "0" and **Impression Type** is "RTB". The values in the **Imps** and **Media Cost** columns should match the values in the **Billable Units** and **Amount** columns on your invoice. For more information on running the report, see [Reconciling Your Invoice with Reporting](reconciling-your-invoice-with-reporting.md).

Cost of media may be rounded off (by a few cents) due to aggregation.

## Miscellaneous

### Where can I find historical billing documents (e.g., Invoices, Seller Statements)?

Depending on which product you use, you can located historical billing documents as follows:

- **For Invest:** In the upper right, **Services Network** \> **Billing**, then look under the **Invoices/Statements** column.
- **For Monetize:** In the upper left, **Network** \> **Billing**, then look under the **Invoices/Statements** column.

### Why am I getting an invoice for data from both the data provider and Microsoft Advertising?

You can purchase data through Microsoft Advertising or directly from your data provider. If you purchased data through Microsoft Advertising you will see that activity in our **Data Usage Report** in the UI. Otherwise, you will be billed by the Data Provider. For more information on Data Clearing, see [Data Marketplace Overview](data-marketplace-overview.md).

### How can I set up netting if we buy and sell through Microsoft Advertising?

Netting is offered to clients who buy and sell with Microsoft Advertising. Clients can then either:

- apply the amounts due in invoices to their platform revenue and be paid the difference (e..g, for clients with sell-side revenue that exceeds their buy-side invoices) or
- apply their revenue to their invoices and then pay what is left on the invoice (e.g., for clients with buy-side costs that exceed their sell-side revenue)

If you would like to enable monthly netting on your account, please submit a request through our  our [Customer Support Portal](https://help.xandr.com/s/login/). To learn more about netting, see [Understanding Your Seller Statement](understanding-your-seller-statement.md).

### Why was I suspended and when will I get paid?

Reasons for account suspension should be discussed with your Account Manager. Client Finance can help you determine the amount you will be paid. It generally requires one month to analyze the account and net out anything that is still owed to Microsoft Advertising (not including finance fees). Once that occurs, Microsoft Advertising will pay any outstanding liability owed to you. Be sure to create a case in our [Customer Support Portal](https://help.xandr.com/s/login/) with your inquiry.
