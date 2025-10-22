---
title: Finance - Buyer Auction Service Charge Mechanics
description: In this article, understand how Buyer Auction Service Charge (BASC) is calculated.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: finance
ms.author: shsrinivasan
---

# Finance - Buyer auction service charge mechanics

When purchasing inventory with Microsoft Advertising, the buyer may be charged the Buyer Auction Service Charge (BASC) specified in its contract. BASC is quoted as a percentage of Media Cost. Microsoft Advertising can apply this charge in one of two ways, either as a fee or a deduction. Which of the two is being used will be specified in the contract.

## Fee

In this case, the BASC is charged separately from Media Cost. Note that these fees will NOT affect or be deducted from Media Cost budgets. As a result, the total amount Microsoft Advertising will invoice for at the end of a campaign (or line item) will exceed the media budget by the BASC.

`Buyer Payment = Media Cost + (Media Cost * Buyer Auction Service Charge %)`

## Deduction (or Bid reduction)

In this case, the BASC is applied as a component of Media Cost. As a result, Microsoft Advertising deducts its BASC from the Media Cost paid by the buyer and passes the remainder on to the seller. During the auction, Microsoft Advertising reduces bids by the amount of each buyer's BASC before comparing bids to determine the winning price paid to the seller.

`Buyer Payment = Media Cost`

`Media Cost = Winning Price / (1 - Buyer Auction Service Charge %)`

## Example

Assume the buyer has a 10% BASC and is bidding a flat $1.20 CPM, and that the next highest net bid is $0.80 CPM.

- If you are participating in a second price auction, the winning price for the impression is $0.81 CPM. The following table illustrates the bids and media cost that result from the Fee and Deduction options:

| BASC % | BASC Type | Initial Bid | Net Bid compared in Auction | Winning Price | Media Cost | Fees | Total Buyer Payment |
|---|---|---|---|---|---|---|---|
| 10% | Fee | $1.20 CPM | $1.20 CPM | $0.81 CPM | $0.81 CPM | $0.08 CPM | $0.89 CPM |
| 10% | Deduction | $1.20 CPM | $1.08 CPM | $0.81 CPM | $0.90 CPM | None | $0.90 CPM |

- If you are participating in a first price auction (i.e., no bid reduction to next highest bid), the winning price for the impression is $1.20 CPM. The following table illustrates the bids and media cost that result from the Fee and Deduction options:

| BASC % | BASC Type | Initial Bid | Net Bid compared in Auction | Winning Price | Media Cost | Fees | Total Buyer Payment |
|---|---|---|---|---|---|---|---|
| 10% | Fee | $1.20 CPM | $1.20 CPM | $1.20 CPM | $1.20 CPM | $0.12 CPM | $1.32 CPM |
| 10% | Deduction | $1.20 CPM | $1.08 CPM | $1.08 CPM | $1.20 CPM | None | $1.20 CPM |

## Inventory discrepancy and bid calculation

When buying ads through the Auction Service, Microsoft Advertising may reduce the bid amount submitted by Company due to discrepancy offsets based on historical counting differences with the inventory provider.
