---
title: Bidders - Bid Response
description: Explore this article to understand bid responses, their implementation, fields, types, and detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Bid response

> [!NOTE]
>
> - **Not Supported**: The AppNexusBidding Protocol is no longer supported; this documentation is for legacy purposes only.
> - If you're a new bidder integrating with Xandr, see the **[OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf)**.

A bidder will send a Bid Response after it receives a [Bid Request](bid-request.md) from the Impression Bus. The Bid Response will include the bidder's bid ("price") and chosen creative (`"creative_id"` or `"creative_code"`). This creative will be served if the bid is ultimately accepted by the ad server.

## Implementation

### Specs

#### Bid_response

| Field | Type | Description |
|:---|:---|:---|
| `debug_text` | string | This optional textfield will be displayed within the debug log when calling any TinyTag with &debug=1&bidder=BIDDER_ID&dongle=DONGLE appended to the query string.<br><br>**Note:** DONGLE (a password to protect a bidder's debug output) is only required if one has been set for your bidder.<br><br>**Required:** No |
| `no_bid` | bool | If 'true', this will signal to the Impression Bus that you have returned a valid response but have chosen not to bid. This **no_bid** field is best when you want to `no_bid` the entire response, not just a particular tag.<br>**Required:** No |

#### Bid_response-\>responses\[ \]

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | int | The ID of the member whose creative is chosen by the bidder from the "members" array in the request.<br>**Required:** Yes |
| `auction_id_64` | int | The ID of the auction for which this response is being sent.<br>**Required:** Yes |
| `exclusive` | bool | *Owner Phase:* If 'true', the creative in this response will be served. No other bidders will be allowed to compete for the impression.<br>**Required:** No |
| `no_bid` | bool | If 'true', this will signal to the Impression Bus that you have returned a valid response but have chosen not to bid on this tag.<br>**Required:** No |
| `price` | double | The gross price, expressed as CPM, that the bidder is willing to pay for this impression. If exclusive, this is used only for reporting purposes; if not exclusive, only a bidder that pays more than the reserve price will be able to bid in the auction. This should be a simple decimal number. If the value is a string, we will evaluate the string to a 0, so ensure that the value is a number.<br>**Required:** No |
| `userdata_js` | string | The userdata javascript commands to modify the userdata if this bidder's response is selected.<br><br>**Note:** If the field **no_cookies** on the bid request is set to true, then there is no guarantee that any `userdata_js` commands will be executed successfully (since AppNexus may not be able to store any information about the user).<br><br>**Required:** No |
| `custom_notify_data` | string | This freeform text field can be used to pass information to the [Notify Request](notify-request.md). This will be URL- and/or cookie-encoded by ImpBus automatically, so it can be passed in free-text form.<br>**Required:** No |
| `creative_id` | int | *Owner Phase:* The ID of the creative to use as the new default creative for the impression.<br>*Non-owner phase:* The ID of the creative that is submitted as part of the member's bid for the impression.<br>**Required:** Yes (if no code is supplied). |
| `creative_code` | string | The custom code of the creative passed into the creative service.<br>**Required:** Yes (if no code is supplied). |
| `click_url` | string | The click URL to be associated with the creative. If the creative already has a `click_url` configured, the value in the bid response will be prepended to the existing url. You can also use custom macros for your click tracking.<br>**Required:** No |
| `pixel_url` | string | The pixel URL to be associated with the creative. This pixel will be used for non-secure inventory.<br>**Required:** No |
| `pixel_type` | enum | The type of pixel to be used: 'javascript' or 'image' (defaults to image if not supplied).<br>**Required:** No |
| `deal_id` | int | The ID of the deal you want to use for this auction.<br>**Required:** No |

#### Bid_response-\>responses\[ \]-\>custom_macros\[ \]

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The name of the macro to be replaced in the any of the creative's urls (media, pixel, click, etc) or content. The name may contain any characters except the carat (^), and must be formatted as `${MACRO_NAME}`<br>within the creative's urls or content.<br><br>**Note:** Custom macros are replaced AFTER system macros have been replaced.<br>For more details on custom macros, see [Creative Service](creative-service.md).<br><br>**Required:** No |
| `value` | string | The value used to replace the macro. The value may contain any characters except the carat (^). Do not escape forward slashes.<br><br>**Note:** Even if the value is an integer, it must be placed within double-quotes. |

## Auction ID

- Each bid response should include the auction ID for the tag it is responding to. Multiple responses can be given for the same auction.
- Bid responses in which `no_bid` is set to `true` must include the auction ID.

## Limits on custom data (Macros and notify data)

AppNexus does not impose limits on data passed in the `custom_macros` array or the `custom_notify_data` field, but we recommend limiting total custom data passed to 1000 characters or less. This data has to be encoded and sent to the user's browser for certain types of inventory (external sellers, iFrame placements) as part of a redirect URL, and longer URLs can break under certain browsers and for certain sellers.

## Example

### Single tag response (using creative ID with pixel)

```
{
   "bid_response":{
      "responses":[
         {
            "member_id":3,
            "price":11.170,
            "creative_id":11,
            "pixel_url":"https://ad.doubleclick.net/pixel?id=11706",
            "pixel_type":"image",
            "auction_id_64": 2345245234523
         }
      ]
   }
}
```

#### Single tag, multiple bids (using creative ID with pixel)

```
{
   "bid_response":{
      "responses":[
         {
            "member_id":3,
            "price":11.170,
            "creative_id":11,
            "pixel_url":"https://ad.doubleclick.net/pixel?id=11706",
            "pixel_type":"image",
            "auction_id_64": 2345245234523
         },
         {
            "member_id":3,
            "price":9.200,
            "creative_id":12,
            "pixel_url":"https://ad.doubleclick.net/pixel?id=11706",
            "pixel_type":"image",
            "auction_id_64": 2345245234523
         }
      ]
   }
}
```

#### Multi tag response (using creative code and custom macros)

```
{
   "bid_response":{
      "responses":[
         {
            "member_id":7,
            "price":3.12,
            "creative_code":"23219",
            "custom_macros":[
               {
                  "name":"CAMPAIGN_ID",
                  "value":452346
               },
               {
                  "name":"INT_CODE",
                  "value":"a352-45we-sdr3"
               }
            ],
            "userdata_js":"update_frequency(23219)",
            "auction_id_64": 2345245234523
         },
         {
            "member_id":14,
            "price":1.14,
            "creative_code":"23219",
            "custom_macros":[
               {
                  "name":"CAMPAIGN_ID",
                  "value":452312
               },
               {
                  "name":"INT_CODE",
                  "value":"c231-4sa2-css5"
               }
            ],
            "userdata_js":"update_frequency(23219)",
            "auction_id_64": 2432387423232
         }
      ]
   }
}
```

#### Response to a deal

```
{
   "bid_response":{
      "responses":[
         {
            "member_id":5555,
            "price":0.75,
            "creative_id":11,
            "auction_id_64": 5555508250840350700,
            "deal_id": 555664
         }
      ]
   }
   }
```
