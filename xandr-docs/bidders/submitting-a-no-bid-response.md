---
title: Submitting a No-Bid Response
description: Learn when to submit a "no-bid" response. This page also talks about the two types of no-bids, Global no-bids and Tag-based no-bids.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Submitting a No-Bid response

> [!NOTE]
>
> - **Not Supported**: The AppNexus Bidding Protocol is no longer supported; this documentation is for legacy purposes only.
>
> - If you're a new bidder integrating with AppNexus, please see the **[OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf)**

If your bidder receives a bid request for which no member wants to bid, you may submit a "no-bid" response. There are two types of no-bids:

- Global no-bids, in which a bidder chooses not to bid on any part of the bid request.
- Tag-based no-bids, in which you may bid on one or more tags in a multi-tag bid request, but not on others.

> [!NOTE]
> For multi-tag auctions, you do **not** need to submit no-bids for auctions that you're not bidding on. If your bidder is configured such that it must submit no-bids in these cases, use the [tag-based no-bid](#tag-based-no-bids) format listed below.

## Global No-Bids

When you would like to no-bid on a global basis, you must submit include `{ "no_bid": true }` in the bid response. The bid response below is sufficient for this type of no-bid.

``` 
{
     "bid_response":{
         "no_bid":true 
    }
}
```

## Tag-Based No-Bids

If you receive an bid request in which there are multiple tags. You may elect to bid for none of them, in which case you would use the global no-bid above, or you could bid for one more. If you want to be explicit in your bid response, you can choose to submit no-bids for those tags that you don't want to bid on.
This is not necessary - you can submit responses only for those tags that you want to bid on (you must return the auction id for each bid). If you do no-bid on a specific tag, you must include the auction ID. The example below no-bids on two of the three auctions, and submits a bid for auction `3452454642231`.

``` 
{
   "bid_response":{
      "responses":[
        {
           "auction_id_64":2432387423232,
           "no_bid":true,
        },
        {
            "member_id":3,
            "exclusive":false,
            "price":1.170,
            "creative_id":11,
            "pixel_url":"https://ad.doubleclick.net/pixel?id=11706",
            "pixel_type":"image",
            "auction_id_64": 3452454642231
        },
        {
           "auction_id_64":786958659876
           "no_bid":true,
        }
      ]
   }
}
```

## Related topics

- [Submit a Bid Response](submit-a-bid-response.md)
- [Bid Response](bid-response.md)
- [Bid Response - FAQ](bid-response---faq.md)
