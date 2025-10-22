---
title: Bidders - Deal Sync with DV360 - FAQ
description: Explore Deal Sync with DV360 FAQs. Beta product for selected sellers testing. Contact account representative to participate.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Deal sync with DV360 - FAQ

> [!NOTE]
> This product is currently in Beta stage and has been enabled for selected sellers who have chosen to participate in the beta testing. If you would like to test out this product, reach out to your Xandr account representative.

## How do I know a deal successfully uploaded to DV360 systems?

You can confirm this with the DV360 buyer by asking if they can see the deal in the negotiations page of the DV360 UI.

## How do I know if a buyer accepted the deal in the DV360 UI?

Ask the DV360 buyer to confirm they have accepted the deal in the DV360 UI. We are working to display the DV360 buyer acceptance status in and plan to release the feature in future iterations of this product.

## What deal information is uploaded to DV360 systems via API?

The following details are shared with DV360 APIs:

| Name| Type | Information |
|--|--|--|
| Deal Name| Deal Type | Currency |
| Buyer Seat ID | Deal Auction Type | Floor Price/Ask Price |
| Seller Name | Start Date | Allowed Media Types (PG Deals ONLY) |
| Deal ID |  End Date | Allowed Creative Sizes (PG Deals ONLY) |

## What will happen to existing DV360 deals that were created before enablement of deal sync?

In the Alpha phase of testing, changes to existing deals created prior to enablement of DV360 deal sync will not automatically be uploaded to DV360 APIs. You will need to work with the buyer to manually update the deal objects in the DV360 UI, per the existing workflow.

## Will updates to existing DV360 deals that were created before deal sync was enabled automatically update?

No, deals created prior to the enablement of DV360 deal sync on your account will not automatically update. You will need to work with the DV360 buyer to manually update the deal in the DV360 UI.

## If I created a deal with DV360 post enablement of Deal sync and then updated the deal details, will they automatically update in DV360 systems?

Yes, deals created post DV360 deal sync enablement will have automatic deal updates. Changes you make to updatable fields (ex. start date, end date, price) will be automatically uploaded to DV360 systems. Once the changes are uploaded, this will trigger a change to the buyer status to "pending". You will need to ask the DV360 buyer to re-accept the deal in the DV360 UI.

## What are the things I cannot change with DV360 deals once they are created?

The following fields cannot be changed in DV360 systems after a deal is uploaded:

- Deal ID
- Deal Type
- Auction Type
- Currency
- Allowed media type

## Can I change a buyer for a deal once it has been uploaded to DV360 systems?

Publisher cannot remove buyers from a deal once it has been uploaded to DV360 systems. However, if your account is enabled for multi buyer deals, you can add buyer `seat ID`s to an existing deal.

## Can I create a deal for multiple media types?

While multi format deals are supported in Monetize UI, DV360 does encourage publishers to declare only one media type in a deal. This will allow buyers to get more granular details about how to target a deal.

Programmatic Guaranteed (PG) Deals cannot be multi-media type. One media type must be declared in all PG deals with DV360.

## If a DV360 buyer manually creates a deal first in DV360 UI using the deal ID, and then the deal with the same deal ID gets uploaded to DV360 via the deal sync process, how will DV360 systems handle it?

There are a few ways DV360 systems will react:

1. If the deal details of the deal created via API match the manually created deal, then the deal created via API is automatically matched with the manually created deal and will be accepted.
1. If the deal details of the deal created via API does not match the manually created deal, the buyer will be asked to re-accept the deal. Prior to re-acceptance, the deal created manually will continue to deliver based on old terms. Accepting the new deal will override the manually created deal.
1. If the deal type of the deal created via API upload differs from the manually created deal, the API call will fail. For example, if the manually created deal is a non-reserved deal, the API call will fail if you create a reserved deal via API.

Once a deal is uploaded to DV360 systems via the deal sync process, buyers will not be able to use that same deal ID to manually create a deal in the DV360 UI.

## When I create a PG deal, do the Ask Price and Impression Budget numbers have to be accurate?

Yes, the "Ask Price" and "Impression Target" must be the same as the contracted numbers agreed with the buyer. These two numbers will be pushed into DV360 systems and buyers won't be able to update them. Any changes to these two values will trigger re-acceptance of the deal. The buyer will continue to bid based on previously accepted deal parameters until the buyer re-accepts the deal.

## What should publishers tell buyers about how to accept a synced deal in the DV360 UI?

Publishers can share the [DV360 Buyer UI Deal Acceptance Workflows](dv360-buyer-ui-deal-acceptance-workflows.md) document with their buyers, which explains in more detail how to accept a deal in the DV360 UI as well as how to target creatives and line items to an accepted deal.

## What are some ways for DV360 buyers to find the deal in the DV360 UI so they can accept it?

Buyers can find the deal through a few identifying factors in the Negotiations screen of the DV360 UI:

- Filter for deals "pending action" to find deals that require the   buyer's acceptance.
- Search for deals using the seller name, which will be the publisher's Xandr Member name.
- Search for deals using the deal name, which will be the name submitted in Xandr systems.

## Can a publisher pick and choose which DV360 buyers to automatically sync deals with?

That feature isn't supported. Deal sync with DV360 is designed to automate deal sync for ALL DV360 buyers as the design of the final state of this product is to enable all sellers in the Xandr marketplace.

## I created a deal with DV360 member 1212, why did it not sync with DV360 systems?

Deals created with DV360 Xandr members are not supported in deal sync with DV360 as DV360 APIs require the DV360 partner ID declared in the deal. Xandr is unable to determine which partner IDs to associate with a member id deal.

## My buyer is seeing that creative format and creative requirements are undeclared but required in, should they be concerned?

Creative format and requirements are not required fields for non-PG deals so we currently do not upload these details for non-PG deals. The warning is benign and does not mean that the buyer cannot set up line items on these deals. It just means that they can use any type of creative to target those deals. Other buyers have seen this warning before and have successfully set up line items and creatives to bid on these deals.

## My buyer sees that a deal is displaying Pacing as "ASAP", is there any way to change that?

The buyer should not be concerned that Pacing is set to ASAP. Pacing is controlled on the sell side, and this field is purely for transparency purposes. Therefore pacing will largely be determined based on the publisher's settings in Xandr systems rather than the line items set up in DV360.

## Do I need to declare sizes in the deal when I am setting up a PG Deal using size-less placements?

Yes, publishers should still include all potential sizes that could be passed in bid requests for that specific PG deal. DV360 does not support the concept of "any size" for image creatives. DV360 uses size restrictions specified during deal negotiation to enforce the buyer to select at least one creative that satisfies each required creative dimension, thereby guaranteeing that we'll have at least one eligible creative to serve the requested ad size. If the allowed sizes for a PG deal changes, the publisher can go in and update the allowed creative sizes in the PG deal and Xandr will automatically upload those updates to DV360 systems.
