---
title: Segment Usage by Buyers
description: Explore this article to understand how clients can get detailed auction information from their bidder or view available segments using traffic campaigns. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Segment usage by buyers

The way a given client utilizes shared segments, whether contextual, behavioral, or otherwise, is highly dependent upon the way the client is integrated with Xandr. Clients who have implemented their own bidder will see the details of impressions (in accordance with applicable privacy regulations and user opt-out preferences). For more details, see [Xandr's Bidders](#xandrs-bidders). Clients using traffic campaigns will see the segments available for targeting but do not have visibility into the details for each auction.  For more details, see [Xandr's UI clients](#xandrs-ui-clients).

## Xandr's Bidders

Bidders receive full details of auctions on the bid request (in accordance with applicable privacy regulations and user opt-out preferences). These details can include:

- Auction ID
- Xandr User ID
- Referrer URL
- IP Address
- Segment information for all owned segments
- Segment information for segments which have been shared by a data provider

Use of this information is entirely reliant upon targeting logic built into the bidder's architecture.

Below is a sample bid request containing the information mentioned above. Note the fields `"auction_id_64"`, `"user_id_64"`, `"segments"`, `"url"`, and `"ip_address"`:

```
{
   "bid_request":{
      "members":[
         {
            "id":6
         },
         {
            "id":12
         }
      ],
      "allow_exclusive":false,
      "debug_requested":false,
      "tags":[
         {
            "id":13,
            "sizes":["728x90"],
            "position":"unknown",
            "inventory_source_id": 476,
            "auction_id_64":8984480746668973511,
            "tag_format":"iframe",
            "reserve_price":1.000,
            "ad_profile_id":382
         }
      ],
      "bid_info":{
         "user_id_64":2987961585469200312,
         "no_flash":false,
         "no_cookies":false,
         "ip_address":"96.246.152.18",
         "inventory_audits": [
             {
                 "auditor_member_id": null,
                 "intended_audience": "young_adult",
                 "inventory_attributes": [2,3,6,7],
                 "content_categories": [39]
             }
         ],
         "user_agent":"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US;rv:1.9.0.3) Gecko/2008092414 Firefox/3.0.3",
         "accepted_languages": "en-US,en;q=0.8",
         "country":"US",
         "region":"NY",
         "city": "New York",
         "postal_code": 10014,
         "dma":501,
         "time_zone":"America/New_York",
         "url":"https://www.foodandwine.com/recipes/",
         "domain":"foodandwine.com",
         "selling_member_id":3,
         "within_iframe":false,
         "total_clicks":0,
         "segments":[
            {
               "id":103,
               "member_id":6,
               "code":"PotentialCarBuyer",
               "last_seen_min":21108407
            }
         ]
      }
   }
}
```

## Xandr's UI clients

Shared segments are accessible to Xandr's UI clients in a number of ways. For more information, see [Segment Targeting](../monetize/segment-targeting.md).
