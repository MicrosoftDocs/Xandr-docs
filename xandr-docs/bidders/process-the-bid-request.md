---
title: Process the Bid Request
description: In this article, learn how the bid requests are processed along with some sample bid requests.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Process the bid request

When you simulate traffic to a TinyTag for which your bidder is eligible to bid, a Bid Request will be sent to your bidder. This request includes a significant amount of information about the impression. Sample bid requests for OpenRTB and Xandr's bidding protocol are shown below. For a more detailed description of the various fields, see [Bid Request](outgoing-bid-request-to-bidders.md).

The Bid Request is sent with header information, such as the IP address and debug information. The JSON for the request itself includes details about the members for which the auction should be evaluated by the bidder; the tag(s) for the auction, including details about each tag; and information about the auction, including the user ID, the region from which the impression originated, and other information.

Once your bidder has received this first bid request, you can trust that the initial sandbox setup is working properly.

## Sample bid requests

### OpenRTB

```
{
  "id": "1234534625254",
  "at": 2,
  "tmax": 120,
  "imp": [
    {
      "id": "1",
      "banner": {
        "w": 320,
        "h": 50,
        "pos": 1,
        "battr": [
          13
        ]
      }
    }
  ],
  "badv": [
    "company1.com",
    "company2.com"
  ],
  "app": {
    "id": "234563",
    "bundle": "com.rovio.angrybirds",
    "cat": [
      "IAB2-1",
      "IAB2-2"
    ],
    "publisher": {
      "id": "pub12345"
    }
  },
  "device": {
    "ip": "64.124.253.1",
    "ua": "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.6; en-US; rv:1.9.2.16) Gecko/20110319 Firefox/3.6.16",
    "os": "OS X"
  },
  "user": {
    "id": "45asdf987656789adfad4678rew656789"
  }
}
```

### Bidding protocol

```
Host: 64.208.137.73
Connection: keep-alive
X-Inventory-Class: 4
X-Venue: 352
X-DMA: 501
X-Exclusive: 0
X-Debug: 1
{
   "bid_request":{
      "members":[
         {
            "id":5
         }
      ],
      "allow_exclusive":false,
      "debug_requested":false,
      "tags":[
         {
            "id":13,
            "sizes":["728x90"],
            "position":"unknown",
            "auction_id_64":8984480746668973511,
            "reserve_price":1.250,
            "tag_format":"javascript",
            "ad_profile_id":382,
            "default_creative_id":29,
            "tag_data":"page_id=242",
            "querystring":"age=12&gender=male"
         },
         {
            "id":17,
            "sizes":["300x250"],
            "position":"unknown",
            "auction_id_64":8984480746668973512,
            "reserve_price":1.500,
            "tag_format":"javascript",
            "ad_profile_id":389,
            "default_creative_id":32,
            "tag_data":"page_id=242",
            "querystring":"age=12&gender=male"
         }
      ],
      "bid_info":{
         "user_id_64":2987961585469200312,
         "selling_member_id":3,
         "no_cookies":false,
         "ip_address":"96.246.152.18",
         "user_agent":"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US;rv:1.9.0.3) Gecko/2008092414 Firefox/3.0.3",
         "country":"US",
         "region":"NY",
         "city": "New York",
         "postal_code": 10014,
         "dma":501,
         "time_zone":"America/New_York",
         "url":"https://www.yahoo.com/",
         "domain":"yahoo.com",
         "within_iframe":false,
         "total_clicks":0
      }
   }
}
```

## Next step

[Submitting your Bid Response](submit-a-bid-response.md)
