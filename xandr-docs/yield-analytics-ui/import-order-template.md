---
title: Import Order Template
description: In this article, explore information about template fields, important notes for template usage, and instructions on importing an order template.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Import order template

Create an XLS file with following fields for an import order template:

## Template fields

The fields on the template are:

| Field | Required? | Notes |
|:---|:---|:---|
| Order ID | Y | Order Management System (OMS) ID, or a sequential number. |
| Order Name | Y | The order name should follow your standard naming structure. |
| Advertiser  | Y | Advertiser names should match those entered into your ad server.|
| Industry | N |  |
| Salesperson | N |  |
| Agency | N |  |
| Order Line ID | Y |  |
| Order Line Name  | Y |  |
| External Target ID | Y |  |
| Target Expression | Y | Complete targeting expression. Example: ad size in ('728x90') and area in ('Hotel') and site in ('Great Bookings'). |
| Start Date | Y | Order start date -- mm/dd/yy (11/27/13). |
| End Date | Y | Order end date -- mm/dd/yy (11/27/13). |
| Pricing Type | Y | How is the deal priced. Example: flat rate, by volume, or performance -- CPD; CPA; CPC; CPM. |
| Contract Type | Y | What type of deal is this -- Bulk; House; Sponsorship; Time-Based Bulk; Weight-Based Bulk; Advertising Exchange; Unknown; Standard; PSA; Text Link. |
| Impressions  | Y | How many impressions are included in this proposal? -- standard numerical entry, without any formatting (100001). |
| Sold | Y | Contracted CPM value -- standard currency input with two decimal places (10.01). |

## Notes on using template

- The External Target ID or **Target Expression** should be filled out. The ID is used to lookup targeting: If both fields are completed, the targeting expression is used.
- Only order lines that have all of the required details completed are imported, all others will be excluded. (This also applies to invalid targeting expressions.)
- All orders created via **Evaluate Orders** (Deal Planner) will appear in the **Orders** table with a Proposed status.
- If two users edit the same proposal simultaneously, the most recent changes are used.
- Proposals created in Yield Analytics are kept in the database for seven days, unless they are replaced with a matching order during nightly processing.
  - The amount of time that proposals stay in the system can be configured. For details, see your Client Services Manager.
- The column headers in the template are there for ease of completion, but they aren't required for the import process to work.

## Related topics

- [Evaluate Orders Overview](evaluate-orders-overview.md)
- [Evaluate the Yield of an Order](evaluate-the-yield-of-an-order.md)
- [Orders Overview](orders-overview.md)
