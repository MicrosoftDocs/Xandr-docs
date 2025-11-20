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

## Log-Level Data 
Monthly fee for access to detailed impression-level data 

## Member breakout fee 
Fee for creating additional member seats 

## Impression Tracker fee 
Charge applied when using third-party tracking tags to measure ad impressions served on the platform. These tags help verify that ads were shown and collect accurate reporting data 

## Click Tracker fee 
A charge for using third-party tags that record when someone clicks on the ad. These trackers help verify clicks and provide accurate reporting for your campaigns. 

## Prebid Server Premium (PSP) Fee 
The charge for using Microsoft Advertising’s Prebid Server Premium. This fee shows up as “Seller Auction Service Fee” on the invoice.

## Broker Auction Service Charge (BrASC) 
BrASC is a charge for enabling the curator to use Curate's suite of packaging and audience tools and access supply. When taken as a percentage, it is calculated based on the buyer’s media cost after buy-side charges are applied. 

## Margin Auction Service Charge (MASC) 
MASC is an alternative charge which can be applied when a curator takes a margin on curated deals. MASC is applied as a percentage of the curator’s gross margin. For example, if margin is $0.18 and MASC is 30%, the fee is $0.06 

## Creative Audit 
The charge for each creative audit performed by Microsoft Advertising, both initial audits and re-audits. The creative audit fee is waived with standard turnaround time. Priority audit is charged a fee with expedited turnaround time. You can view the creative audit amount for a specific invoice period using the Completed Creative Audits Report in the UI. 

## Creative overage fee 
This fee only applies to hosted banner creatives. This includes creatives uploaded with HTML-5 zip files, as they are treated as hosted banners and charged for creative overage. 

The amount charged for serving creatives that are over the maximum size specified in your contract. For each oversized creative, the difference between (a) the size of the creative and (b) the maximum creative size outlined in your contract is multiplied by (c) the number of impressions where the creative served, and then by (d) the bandwidth charge in your contract is equal to the creative overage fee we charge each month. You can reconcile the creative overage fee on your invoice in the UI with the Buying Billing Report. 

> [!NOTE]
>  - (b) the maximum creative size is in KB where as (d) the bandwidth charge is in GB. When converting from GB to KB, divide by 976,563 because Microsoft Advertising uses the kibibyte metric for KB. 
> - For example, let's say the maximum creative size in your contract is (b) 40KB, you have a (a) 60KB creative that served (c) 100,000 times, and your bandwidth fee is (d) $2.50 per GB (which converts to 976,563 KB). 
> - Your creative overage fee is calculated as follows: [[(a)60KB - (b)40KB ] x 100,000 imps] x [(d) $2.50 / 976,563 KB] = $5.12 

 
## Fee vs Deduction 
Curator charges can be applied in two distinct ways: as a fee or as a deduction. The contract will specify which of the two will be used 

## Fee 
A fee is a charge that appears as a line item on the Curator’s invoice. It does not affect or will be deducted from the media cost. Only BrASC can be charged as a fee. 

## Deduction 
A BrASC deduction is applied as a component of media cost. A MASC deduction is taken as a component of the curator’s margin. It is disconnected from the buyer's net media cost. It is taken as a percentage of the curator's margin and is deducted from the curator's margin. The buyer's net media cost, less any BrASC deduction and less any curator margin, equals the curator's net media cost which is passed to the seller. 