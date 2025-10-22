---
title: Deals for Bidders
description: Explore bidding deals, learn the process with platform sellers, and seize opportunities to bid effectively on this page.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Deals for Bidders

Xandr offers the ability to bid on deals with our platform sellers. This page walks you through the bidding process.

> [!TIP]
> A deal auction can be open or private, depending on how the seller defined the deal. For information about how these different types of auctions work, see [Deal Auction Mechanics](deal-auction-mechanics.md).
> [!NOTE]
> The member cannot be changed after a deal has been created.

## Buying deal inventory

### Step 1. Configure your system to handle deals

Ensure that your system is configured to read deal IDs in the bid request and format a proper deal-specific bid response. For more information, see the [Example Request/Response Chain](deals-for-bidders.md#example-requestresponse-chain). Please also make sure to review [Deal Auction Mechanics](deal-auction-mechanics.md) to understand how Xandr conducts auction in different situations.

### Step 2. Reach out to your Xandr representative

Once you've configured your system to handle deal ID requests and responses appropriately, reach out to your Xandr representative to enable you for deals on Xandr. Enabling you for deals may involve:

- Validating how you decision and respond to deal requests
- Making you visible to sellers in our system

### Step 3. Tell your buyers to start negotiating deals

Your buyers will negotiate deals with sellers directly. Xandr is not involved in the process. Here's the process that your buyers should follow:

1. Buyer negotiates a deal with a seller off-line.
1. Buyer gives their Xandr member ID to the seller. If they don't know their member ID, you should help them identify it.
1. Seller sets up a deal with the buyer within the UI
1. Seller gives the deal ID to the buyer.
1. Buyer enters the deal ID into your bidder system for targeting.  

### Step 4. Validate your buyers' deals

Once a buyer has set up a deal with a Xandr seller, you must ensure that your bidder profiles are not blocking any of the parameters that apply to the deal inventory. For example, if a profile is filtering out the seller, creative size, or other parameter that applies to the deal inventory, you will not receive those bid requests. For details about updating or creating bidder profiles, see the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md).

> [!NOTE]
> We recommend using the [Deal Buyer Access Service](deal-buyer-access-service.md) to validate that the deal exists in Xandr's system. This will help you avoid targeting a deal that is inactive or not what you expected.

Example:

```
$ curl -b cookies -c cookies  'https://api.adnxs.com/deal-buyer-access?id=63'
{
     "response" : {
         "status" :  "OK" ,
         "count" : 1,
         "deal" : 
         "deals" : {
             "id" : 63,
             "code" :  null ,
             "name" :  "Private deal for buyer 1085 with floor of $2.50" ,
             "description" :  null ,
             "active" :  false ,
             "start_date" :  "2013-12-01 00:00:00" ,
             "end_date" :  "2013-12-31 23:59:59" ,
             "floor_price" : 2.5,
             "currency" :  "USD" ,
             "use_deal_floor" :  true ,
             "last_modified" :  "2013-12-04 20:39:57" ,
             "seller" : {
                 "id" : 100006,
                 "name" :  "Seller 456"
             },
             "buyer" : {
                 "id" : 100007,
                 "bidder_id" : 2,
                 "name" :  "Buyer 456"
             },
             "type" : {
                 "id" : 2,
                 "name" :  "Private Auction"
             },
             "brands" : [
                 {
                     "id" : 1
                 }
 
             ],
             "ask_price" : 2.75,
             "suggested_min_bid_price" : 3
         }
     }
}
```

### Example request/response chain

> [!NOTE]
> This example is for the Xandr integration of the AppNexus Bidding Protocol.

### Bid request

```
{
    "bid_request": {
        "timestamp": "2014-04-18 17:00:57",
        "bidder_timeout_ms": 2000,
        "members": [
            {
                "id": 1417
            },
            {
                "id": 1625
            }
        ],
        "test": true,
        "member_ad_profile_id": 555216,
        "excluded_attributes": [
            2033
        ],
        "tags": [
            {
                "auction_id_64": 5555508250840350700,
                "size": "300x250",
                "sizes": [
                    "300x250"
                ],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "iframe",
                "site_id": 555526,
                "creative_formats_map": "111111111011",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url",
                    "unknown",
                    "unknown"
                ],
                "ad_profile_id": 555180,
                "visibility_profile_id": 5553,
                "venue_id": 407258,
                "pop_max_width": 300,
                "pop_max_height": 250,
                "pop_is_prepop": false,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 0.913,
                "estimated_average_price": 0.456,
                "id": 5555354,
                "deals": [
                    {
                        "id": 555664,
                        "member_id": 1625,
                        "floor_cpm": 0.5,
                                                "sizes": [
                                                        "300x250", 
                                                        "300x600"
                                                ]
                    }
                ]
            }
        ],
        "bid_info": {
            "user_id_64": 5555037017052493000,
            "no_cookies": false,
            "payment_rule_id": 555018,
            "selling_member_id": 55578,
            "no_flash": false,
            "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36",
            "browser": 8,
            "operating_system": 11,
            "operating_system_extended": 81,
            "operating_system_family": 4,
            "carrier": 1,
            "device_type": 1,
            "language": 1,
            "accepted_languages": "en-US",
            "session_freq": 1,
            "pub_session_freq": 1,
            "ip_address": "555.1.12.54",
            "country": "US",
            "within_iframe": false,
            "device_ids": {
                "sha1udid": "d55555c2314f3789198685914c01425034b5d502",
                "md5udid": "caf55557c5b39fb4ad68dabc9808bda1"
            },
            "publisher_id": 555547,
            "userdata_json": "{}",
            "segments": [
                {
                    "id": 1,
                    "member_id": 0,
                    "code": "cookie_birthday",
                    "provider": "Xandr",
                    "last_seen_min": 23274134
                }
            ]
        }
    }
}
```

### Bid response

```
{
   "bid_response":{
      "responses":[
         {
            "member_id":1625,
            "price":0.75,
            "creative_id":11,
            "auction_id_64": 5555508250840350700,
            "deal_id": 555664
         }
      ]
   }
}
```

### Notify request error codes

Deal-specific error codes, see [Bid Error Codes](bid-error-codes.md).

| Error | ID | **Description |
|--|--|--|
| `NEC_DEAL_NOT_AVAILABLE` | 308 | The deal you specified in your response is not currently active. |
| `NEC_DEAL_NO_MEMBER` | 309 | The deal you specified in your response is not available to your member. |
| `NEC_DEAL_BELOW_FLOOR` | 310 | Your bid was not considered in the auction because it is below the deal's ask price. |
| `NEC_DEAL_BRAND_BANNED` | 311 | The brand associated with your creative is not a valid brand for this deal. |

## Related topics

- [Deal Auction Mechanics](deal-auction-mechanics.md)
- [Deal Buyer Access Service](deal-buyer-access-service.md)
- [Legacy Bidder Profile Service](legacy-bidder-profile-service.md)
