---
title: Loss Reason Codes
description: In this article, explore the bid loss codes and its corresponding description enabled for `lurl`.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Loss reason codes

If your bidder has been enabled for `lurl`, the `${AUCTION_LOSS}` macro returns a code for the bid loss reason. The following are the loss codes you might see and their corresponding description.

| `lurl` Loss Code | `lurl` Loss Description |
|:---|:---|
| 1 | Internal Error |
| 3 | Invalid Bid Response |
| 4 | Invalid Deal ID |
| 5 | Invalid Auction ID |
| 6 | Invalid (i.e., malformed) Advertiser Domain |
| 7 | Missing Markup |
| 8 | Missing Creative ID |
| 9 | Missing Bid Price |
| 100 | Bid was Below Auction Floor |
| 101 | Bid was Below Deal Floor |
| 102 | Lost to Higher Bid |
| 104 | Buyer Seat Blocked |
| 200 | Creative Filtered - General; reason unknown |
| 201 | Creative Filtered - Pending Processing by Exchange (e.g., approval, transcoding, etc.) |
| 202 | Creative Filtered - Disapproved by Exchange |
| 203 | Creative Filtered - Size Not Allowed |
| 204 | Creative Filtered - Incorrect Creative Format |
| 205 | Creative Filtered - Advertiser Exclusions |
| 207 | Creative Filtered - Not Secure |
| 208 | Creative Filtered - Language Exclusions |
| 209 | Creative Filtered - Category Exclusions |
| 210 | Creative Filtered - Creative Attribute Exclusions |
| 213 | Creative Filtered - Not Allowed in PMP Deal |

For more information on the macros supported for `lurl`, see [Incoming Bid Response from Bidders](incoming-bid-response-from-bidders.md).
