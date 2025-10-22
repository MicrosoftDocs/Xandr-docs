---
title: Submit a Bid Response
description: Learn how for every Bid Request, the Imp Bus allows you to submit a Bid Response, which in turn must include the auction_id_64 in the Bid Request, and the member_id of the member for each response.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Submit a Bid Response

For each Bid Request, the Imp Bus allows you to submit a Bid Response (see [Bid Response](incoming-bid-response-from-bidders.md) for more details). Each response must include the auction_id_64 included in the Bid Request, and the member_id of the member for each response. The segment changes will only take effect if the bid is selected by the publisher. Examples of bid responses for OpenRTB and Xandr's bidding protocol are shown here:

**OpenRTB**

``` 
{
  "id": "1234567890",
  "seatbid": [
    {
      "bid": [
        {
          "id": "1",
          "impid": "102",
          "price": 9.43,
          "adid": "314",
          "nurl": "https://adserver.com/winnotice?impid=102&price=${AUCTION_PRICE}",
          "ext": {
            "appnexus": {
              "crcode": "234234",
              "custom_macros": [
                {
                  "name": "INT_CODE",
                  "value": "a352-45we-sdr3"
                }
              ]
            }
          }
        }
      ],
      "seat": "512"
    }
  ],
  "bidid": "abc1123",
  "cur": "USD"
}
```

**Bidding protocol**

``` 
{
   "bid_response":{
      "responses":[
         {
            "member_id":9,
            "price":12.21,
            "creative_id":18,
            "segment_actions": [{"action": "add", "id":1234, "expires_min": 60},{"action": "remove", "code":"wxyz","member_id":9}],
            "auction_id_64": 2345245234523
        }
      ]
   }
}
```

To tell the impression bus that you're not interested in bidding on that particular auction, you must submit a bid response with no_bid set to true. See [Bid Response](incoming-bid-response-from-bidders.md) for more details.

Next step: [Synchronizing User IDs](synchronize-your-user-ids.md)
