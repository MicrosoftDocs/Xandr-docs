---
title: Bid Response - FAQ
description: In this article, explore answers to frequently asked questions about the process of responding to bids, bid preparation, and submission.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bid response - FAQ

## Multiple bid responses

### How do I submit multiple bid responses for a single auction?

The [Bid Response](incoming-bid-response-from-bidders.md) includes a `seatbid` array object. Each object within the array is a response. For each element in the `seatbid` array you must specify the `seat` (member ID) for which are you responding, along with the other [required fields](incoming-bid-response-from-bidders.md) for the bid response. For example if the bid request had auction ID 12345, and your bidder has two members - 1234 and 4567 - you could submit the following multiple bid responses:

```
{
    "id": "4876290993254515176",
    "seatbid": [{
        "bid": [{
            "id": "1",
            "impid": "8278013996604217356",
            "price": 1,
            "adid": "12345",
            "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}",
            "ext": {
                "appnexus": {
                    "custom_macros": [{
                        "name": "custom_macro_1",
                        "value": "m1.js"
                    }]
                }
            }
        }],
        "seat": "1234"
    },
    {
        "bid": [{
            "id": "1",
            "impid": "8278013996604217356",
            "price": 1,
            "adid": "12345",
            "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}",
            "ext": {
                "appnexus": {
                    "custom_macros": [{
                        "name": "custom_macro_2",
                        "value": "m2.js"
                    }]
                }
            }
        }],
        "seat": "4567"
    }],
    "bidid": "1",
    "cur": "USD"
}
```

### Which bid is chosen when I submit multiple responses?

There are a number of factors, such as bid biases, channel conflict rules, and member exclusion that a seller can utilize. For example, a seller may not be willing to see X brand on Y site, or that seller may say that X brand can run only if the buyer pays $1 cpm more. A seller may also have a complex set of conditional rules that say, for example, X brand can only run if it's one of the first five impressions per day for a user from the US. Xandr will determine which response has the highest cpm after all ineligible creatives have been eliminated and all biases have been applied. This is the response that will be used.

### How many bids can I submit per bid request?

You may return up to 15 responses per bid request. In a single auction request these will all be for the same auction. In a multi-auction request these may be distributed between one or more auctions.

## Serving creatives

### Can I customize my creative per impression?

When you upload a creative (see [Creative Service](creative-service.md) and [Creative - FAQ](creative---faq.md)), you can specify Xandr macros as well as custom macros in the content of the creative. Macros are in the form `${MACRO_NAME}`.

The complete list of Xandr macros is available on the [Xandr Macros](xandr-macros.md) page. These macros are automatically populated with the appropriate data when the creative is served. For example, `${PRICE_PAID}` is the cpm that it cost to actually win that impression.

> [!WARNING]
> Macros specified when uploading to the Creative Service must be either Xandr macros or custom macros, NOT OpenRTB macros. OpenRTB macros can be used only in the bid response.

If you have determined, for example, that this user is part of your user group ABC, you can include a custom macro in the creative's content. In the response object, in the [Bid Response](incoming-bid-response-from-bidders.md), you can specify the values of any custom macros. The following excerpt will replace the custom macro `${MY_USER_GROUP}` with ABC and `${SOMETHING_ELSE}` with 123. **Custom macros are applied after Xandr macros**, so if you have a custom macros of the same name as a Xandr macro, the Xandr value for that macro will take precedence and your value will be ignored.

```
"custom_macros":[
               {
                  "name":"MY_USER_GROUP",
                  "value":"ABC"
               },
               {
                  "name":"SOMETHING_ELSE",
                  "value": "123"
               }
]
```

It is recommended that you include a a catch-all parameter in the content of each creative in case it is determined that you need to serve extra custom parameters. If you change your creative's content, the creative will need to be reaudited. However, you can shoe-horn additional parameters into a catch-all custom macro without incurring an additional audit fee.

### How do I know if I win an auction?

There are several ways you can determine whether you've won an auction:

- **[bid.nurl](incoming-bid-response-from-bidders.md)**

  The nurl is a string containing the win notify URL. The Xandr server pings this URL when it receives a client side notification from the device, which indicates that Xandr won the auction.
- **[Notify request](notify-request.md)**

  If you have set up your bidder to receive notify requests by adding a valid path in the [Bidder Service](bidder-service.md), you will be sent a notify request every time you win an auction.
- **Creative delivery count**

  If you do not provide a notify URL or use the notify request, you can tell when you've won an auction by counting the delivery of your creatives. This method will likely result in a higher discrepancy than the preceding.

## Custom macros

### Why aren't custom macros populating?

The JSON format of the bid response is very particular in this area. Check that you are following the exact format of the object. Specifically, all macros must be replaced with string values. If the JSON for the bid response does not have quote marks around the replacement value, that value will not be interpreted as a string and will thus not be replaced by the impression bus.

Also, nested macros are not supported. If you have nested macros, the innermost macro will not populate.

## Related topics

- [Incoming Bid Response from Bidders](incoming-bid-response-from-bidders.md)
- [Bidder Service](bidder-service.md)
- [Creative Service](creative-service.md)
