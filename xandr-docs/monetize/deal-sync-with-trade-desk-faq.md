---
title: Microsoft Monetize - Deal Sync with The Trade Desk (FAQ)
description: This page deals with FAQs on Deal Synchronization with The Trade Desk.
ms.date: 11/13/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Deal sync with The Trade Desk (FAQ)

Frequently Asked Questions About Deal Synchronization with The Trade Desk:

## How do I know a deal successfully uploaded to The Trade Desk systems?

You can confirm this with The Trade Desk buyer by asking if they can see the deal on the negotiations page of The Trade Desk UI.

Once the deal syncs successfully, the **Pending** label appears on the Microsoft Monetize **Deal** screen. This indicates that the deal is awaiting buyer acceptance in the DSP.

## How do I know if a buyer accepted the deal in The Trade Desk UI?

Ask The Trade Desk buyer to confirm they have accepted the deal in The Trade Desk UI.

Once the buyer accepts the deal, the **Active** label appears on the Microsoft Monetize **Deal** screen.

## What deal information is uploaded to The Trade Desk systems via API?

The following details are shared with The Trade Desk APIs:

|  |  |  |
|--|--|--|
| - Deal Name<br> - Buyer Seat ID<br> - Seller Name<br> - Deal ID | - Deal Type<br> - Deal Auction Type<br> - Start Date<br> - End Date | - Currency<br> - Floor Price/Ask Price<br> - Allowed Media Types<br> - Allowed Creative Sizes |

## Will updates to existing The Trade Desk deals that were created before deal sync was enabled automatically update?

No, deals created prior to the enablement of The Trade Desk deal sync on your account will not automatically update. You will need to work with The Trade Desk buyer to manually update the deal in The Trade Desk UI.

## Why does my deal have an end date in The Trade Desk UI when I created it with no end date?

The Trade Desk's API requires all newly synchronized deals to include an end date and supports a maximum flight duration of two years. If a deal is created without an end date, Microsoft Advertising automatically assigns an end date corresponding to the maximum supported flight duration of two years during synchronization. This doesn't affect the buyer's ability to bid, even after the end date in The Trade Desk has passed, as long as the deal is active and sending bid requests.

## If I created a deal with The Trade Desk and then updated the deal details, will they automatically update in The Trade Desk systems?

Yes, deals automatically sync updates. Changes you make to updatable fields (for example, start date, end date, price) will be automatically uploaded to The Trade Desk systems. Once the changes are uploaded, this will trigger a change to the buyer status to "pending". You will need to ask The Trade Desk buyer to re-accept the deal in The Trade Desk UI.

Updates to the deal name are an exception: they are automatically accepted and don't require buyer approval.

## What are things I cannot change with The Trade Desk deals once they are created?

The following fields cannot be changed in The Trade Desk systems after a deal is uploaded:

- Buyer

- Deal Type

- Seller Member ID

- Seller Member Name

## Can I change a buyer for a deal once it has been uploaded to The Trade Desk systems?

Publishers cannot remove the buyer from a deal once it has been uploaded to The Trade Desk systems. You can check which buyer is designated by pulling the buyer-deal-sync object in the API or Database.
<!-- If your account is enabled for multi-buyer deals, you can add additional buyer seat ids to an existing deal.-->

## Can I create a deal for multiple media types?

The Trade Desk supports deal sync with multiple media types for Standard deals.

Programmatic Guaranteed deals cannot be multi-media type. One media type must be declared in all PG deals with The Trade Desk.

## When I create a PG deal, do the Ask Price and Impression Budget numbers have to be accurate?

Yes, the "Spend" and "Impression Target" must be the same as the contracted numbers agreed with the buyer. These two numbers will be pushed into The Trade Desk systems and buyers won't be able to update them. Any changes to these two values will trigger re-acceptance of the deal.

## What should publishers tell buyers about how to find and accept a synced deal in The Trade Desk UI?

Buyers can refer to the Knowledge Portal in The Trade Desk UI. Publishers can share the following links with buyers:

- [Knowledge Portal](https://desk.thetradedesk.com/knowledge-portal/en/fwd.html)
- [Using Deal Desk](https://desk.thetradedesk.com/knowledge-portal/en/fwd-using-deal-desk.html)
- For deal acceptance, see [Review and accept deals](https://desk.thetradedesk.com/knowledge-portal/en/fwd-review-and-accept-deals.html).

## I created a deal with The Trade Desk member 1088, why did it not sync with The Trade Desk systems?

Deals created with The Trade Desk Microsoft Advertising members will not be supported in deal sync with The Trade Desk as The Trade Desk APIs require The Trade Desk partner ID declared in the deal. Microsoft Advertising is unable to determine which partner IDs to associate with a member ID deal.
