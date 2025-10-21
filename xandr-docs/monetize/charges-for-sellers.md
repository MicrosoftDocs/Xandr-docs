---
title: Microsoft Monetize - Charges for Sellers
description: Explore seller charges, encompassing Seller Auction Service Charge, Managed Ad Serving Fee, Seller Revenue Share Minimum Fee, and other fees.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Charges for sellers

## Seller auction service charge (SASC)

Also known as Seller Revenue Share in some contracts, SASC is the charge for selling inventory to third-party buyers. It is quoted as a percentage of the buyer's media cost, and deducted prior to the calculation of seller revenue.

## Managed Ad serving fee

The charge for serving managed, kept, mediated, or direct impressions and for serving default creatives, PSAs, and blanks.

## Seller revenue share minimum fee

For contracts which contain a clause that requires a Seller Revenue Share Minimum fee (included on your Buyer invoice for Seller activity during the invoiced period), we review Microsoft Advertising's earnings from the Seller’s resold traffic and apply a minimum CPM (the exact value applied is defined in the contract). For example, assuming the Seller Auction Service fee = **10%** and the Seller Revenue Share Minimum fee CPM = **$0.01 CPM**, the following calculations could be made:

| Month | Resold Impressions | Gross Resold Revenue | Seller Auction Service fee (see formulas below) | Seller Rev Share minimum (see formulas below) | Seller Rev Share Minimum Fee Assessed (explanation) |
|--|--|--|--|--|--|
| Month 1 | 1,000,000,000 | $200,000 | $20,000<br>($200,000 * 10%) | $10,000 (1B/1000*0.01) | $0 (since minimum commitment was met)<br>($10,000 < $20,000) |
| Month 2 | 3,000,000,000 | $200,000 | $20,000<br>($200,000 * 10%) | $30,000<br>(3B/1000*.01) | $10,000 (since minimum commitment was not met)<br>($30,000 - $20,000) |

In this example, the Seller would receive an additional line item on their invoice labelled “Seller Rev Share Minimum” for $10,000 ($30,000 - $20,000).

The Seller Revenue Share Minimum fee will appear on invoices as the DIFFERENCE between the Seller Revenue Share Minimum fee and the Seller Auction Service Fee.

> [!WARNING]
> Gross Resold Revenue does not appear in the UI. Resold Revenue is net earnings to the network after Microsoft Advertising Seller and Buyer Auction Service Charges have been applied.
