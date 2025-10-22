---
title: Programmatic Guaranteed Deals for Bidders
description: In this article, learn about the bidding process to buy guaranteed deal inventory, along with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Programmatic guaranteed deals for bidders

Xandr offers the ability to bid on guaranteed deals with many of our platform sellers. This page walks you through the bidding process.

Programmatic guaranteed deals allow sellers on Microsoft Monetize to make delivery commitments to buyers on a specific deal ID. When buyers accept the deal, they are compelled to bid when Xandr sends the deal ID in a request to their DSP.

## Buying guaranteed deal inventory

Follow the steps to buy the guaranteed deal inventory:

1. **Configure your system to handle deals**

    Ensure that your system is configured to read the deal IDs in the bid request and format a proper deal-specific bid response. For more information, see the [Example Request/Response Chain](deals-for-bidders.md#example-requestresponse-chain). Please make sure to review [Deal Auction Mechanics](deal-auction-mechanics.md) to understand how Xandr conducts auction in different situations.

    > [!NOTE]
    > The `private_auction` flag is independent of programmatic guaranteed deals.

1. **Reach out to your Xandr representative**

    Once you've configured your system to handle deal ID requests and responses appropriately, reach out to your Xandr representative to enable you for guaranteed deals on Xandr. Enabling you for the deals may involve:  

    - Validating how you make decisions and respond to deal requests – bidders are expected to respond to the guaranteed deals at near 100%.

        > [!NOTE]
        > The sizes accepted by the guaranteed deal are specified in the "deals" field.

    - Making your buyer member visible to sellers in our system.
    - Having a dedicated workflow for buying guaranteed deals.

1. **Tell your buyers to start negotiating deals**

    Your buyers will negotiate the deals with sellers directly. Xandr isn't involved in the process. Here's the process that your buyers should follow:  

    - Buyer negotiates a guaranteed deal with a seller offline.
    - Buyer gives their DSP seat ID (or Xandr member ID if still on legacy integration) to the seller. Please check with your Xandr representative if you are unsure which ID to provide.
    - Seller sets up a guaranteed deal with the buyer within UI.
    - Seller gives the deal ID to the buyer.
    - Buyer enters the deal ID into your bidder system for targeting.

1. **Validate your buyers' deals**

    Once a buyer has set up a deal with a Xandr seller, you must ensure that your bidder profiles are not blocking any of the parameters that apply to the deal inventory. For example, if a profile is filtering out the seller, creative size, or other parameter that applies to the deal inventory, you'll not receive those bid requests. For details about updating or creating bidder profiles, see the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md).

    We recommend using the [Deal Buyer Access Service](deal-buyer-access-service.md) to validate that the deal exists in Xandr's system. This will help you avoid targeting a deal that is inactive or not, what you expected.

### Example of a configured programmatic guaranteed deal in the API

Programmatic guaranteed deals are categorized as type ID 4 in the [Deal Service](../digital-platform-api/deal-service.md).

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access?id=888636&member_id=2378'
{
    "response": {
        "status": "OK",
        "count": 1,
        "deal": 
        "deals": {
            "id": 888636,
            "code": null,
            "name": "Programmatic guaranteed deal for buyer 1085 with floor of $2.50",
            "description": null,
            "active": false,
            "start_date": "2020-08-16 00:00:00",
            "end_date": "2013-12-31 23:59:59",
            "floor_price": 8.89,
            "currency": "USD",
            "use_deal_floor": true,
            "last_modified": "2013-12-04 20:39:57",
            "seller": {
                "id": 2378,
                "name": "Seller 2378"
            },
            "buyer_seats": [
                {
                    "guaranteed_deals_support": "Enabled",
                    "name": "AppNexus Black (buyer)",
                    "code": "2382",
                    "bidder_id": 2,
                 },
]
            "type": {
                "id": 4,
                "name": "Programmatic Guaranteed"
            },
            "brands": [
                {
                    "id": 1
                }
            ],
            "ask_price": 10
        }
    }
}
```

## Example request or response chain

This example is for the Xandr integration of the Xandr Bidding Protocol.

Guaranteed deals are noted in the bid request deal.ext.appnexus.gtd = 1 for any guaranteed bid request. (If the field is missing or 0, the bid request isn't guaranteed.)  

### Bid request

```
{
    "id": "1255856238299639049",
    "imp": [
        {
            "id": "5314315908322445999",
            "banner": {
                "w": 300,
                "h": 250,
                "id": "1",
                "pos": 1,
                "api": [
                    1,
                    2,
                    3,
                    5,
                    6,
                    7
                ],
                "format": [
                    {
                        "w": 300,
                        "h": 250
                    },
                    {
                        "w": 1,
                        "h": 2
                    },
                    {
                        "w": 1,
                        "h": 1
                    }
                ]
            },
            "instl": 0,
            "tagid": "29036382",
            "secure": 1,
            "pmp": {
                "private_auction": 1,
                "deals": [
                    {
                        "id": "1662126",
                        "bidfloor": 6,
                        "bidfloorcur": "USD",
                        "at": 3,
                        "wseat": [
                            "5222642"
                        ],
                        "ext": {
                            "appnexus": {
                                "gtd": 1,
                                "sc": 1
                            }
                        }
                    }
                ]
            },
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 5.69,
                    "predicted_view_rate": 0.662587,
                    "member_ad_profile_id": 1420812,
                    "predicted_video_completion_rate": 0,
                    "predicted_view_rate_over_total": 0.622841,
                    "allowed_payment_types": [
                        {
                            "payment_type": 1,
                            "imp_count_method": 2
                        }
                    ],
                    "tag_code": "49509_header_ad",
                    "tag_id": 29036382
                }
            }
        }
    ],
    "site": {
        "id": "6723846",
        "domain": "iheart.com",
        "cat": [
            "IAB1",
            "IAB9-1",
            "IAB9-26",
            "IAB1-6",
            "IAB9-16",
            "IAB9-17"
        ],
        "page": "https://www.iheart.com/upgrade/?upsellfrom=54",
        "publisher": {
            "id": "2260937",
            "ext": {
                "appnexus": {
                    "publisher_code": "939109bd-fe28-4a72-9ab3-66c079f9592f"
                }
            }
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.0 Mobile/15E148 Safari/604.1",
        "geo": {
            "country": "USA",
            "city": "Harrison",
            "zip": "07029",
            "utcoffset": -240,
            "ext": {
                "appnexus": {
                    "timezone": "America/New_York"
                }
            }
        },
        "dnt": 0,
        "devicetype": 4,
        "make": "Apple",
        "model": "iPhone",
        "os": "Apple iOS",
        "language": "en",
        "carrier": "T-Mobile",
        "connectiontype": 3
    },
    "user": {
        "id": "0",
        "gender": "O",
        "ext": {}
    },
    "at": 1,
    "tmax": 150,
    "cur": [
        "USD"
    ],
    "badv": [
        "ig.com",
        "pmi.com",
        "trovit.com",
        "aliexpress.com"
    ],
    "regs": {
        "coppa": 0,
        "ext": {
            "gdpr": 0
        }
    },
    "source": {
        "fd": 1,
        "tid": "1f413c8f-0b66-4f7e-b009-e7adb42ea086"
    },
    "ext": {
        "appnexus": {
            "seller_member_id": 11470
        },
        "schain": {
            "complete": 1,
            "nodes": [
                {
                    "asi": "ogury.com",
                    "sid": "939109bd-fe28-4a72-9ab3-66c079f9592f",
                    "rid": "495963a3-e4f3-4433-886d-8094cc231ddf",
                    "hp": 1
                },
                {
                    "asi": "appnexus.com",
                    "sid": "11470",
                    "rid": "1f413c8f-0b66-4f7e-b009-e7adb42ea086",
                    "hp": 1
                }
            ],
            "ver": "1.0"
        }
    }
}
```

### Bid response

```
{
    "id": "1255856238299639049",
    "seatbid": [
        {
            "bid": [
                {
                    "id": "0",
                    "impid": "5314315908322445999",
                    "price": 6.1799999999999997,
                    "adid": "445790616",
                    "nurl": "https://adx.g.doubleclick.net/pagead/adview?ai=...&pr=10:${AUCTION_PRICE}",
                    "adm": "...",
                    "adomain": [
                        "pepsi.com"
                    ],
                    "dealid": "1662126",
                    "w": 300,
                    "h": 250,
                    "api": 3
                }
            ],
            "seat": "5222642"
        }
    ],
    "cur": "USD"
}
```

## Notify request error codes

Deal-specific error codes, see [Bid Error Codes](bid-error-codes.md) for more info.

| Error | ID | Description |
|---|---|---|
| NEC_DEAL_BELOW_FLOOR | 310 | Your bid was not considered in the auction because it is below the deal's ask price. |
| NEC_DEAL_BRAND_BANNED | 311 | The brand associated with your creative isn't a valid brand for this deal. |
| NEC_DEAL_NO_MEMBER | 309 | The deal you specified in your response isn't available to your member. |
| NEC_DEAL_NOT_AVAILABLE | 308 | The deal you specified in your response isn't currently active. |

## Related topics

- [Deal Auction Mechanics](deal-auction-mechanics.md)
- [Deal Buyer Access Service](deal-buyer-access-service.md)
- [Legacy Bidder Profile Service](legacy-bidder-profile-service.md).
