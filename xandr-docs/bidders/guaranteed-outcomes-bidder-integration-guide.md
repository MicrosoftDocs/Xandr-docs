---
title: Guaranteed Outcomes Bidder Integration Guide
description: This article outlines the Guaranteed Outcome feature of Xandr's Exchange.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Guaranteed Outcomes Bidder Integration Guide

This page outlines the specifications that define the method by which Xandr enables a Bidder to bid for, and to be billed for, an outcome (view and/or complete) vs. the typical served impression. In addition, since different buyers have different standards for what constitutes a "viewable impression", the specification is designed to support a variety of standards, including different definitions (e.g., IAB vs. GroupM) and different measurement technology vendors (e.g. DoubleVerify). In the future, the specification may also be used to support additional transaction events, for example, an in demo impression.

For more information see [Guaranteed Outcomes](./guaranteed-outcomes.md).

## Implementation

At a high level, our approach to the implementation follows what has been described in the OpenRTB specification as a "billing notice", from OpenRTB Specification 2.4, Section 7.2.

> "Winning the auction, however, does not guarantee that the ad will be successfully delivered to the client or that it ? will meet viewability expectations. Furthermore, policies vary among exchanges as to the criteria for billing. Most consider an ad billable upon some form of delivery or rendering vs. the auction win alone. This aligns better with the buyer’s obvious goal of ensuring that the impressions they pay for are actually displayed.To abstract the concept, let us refer to “billing notice” as the firing of some notification URL at the time when the clearing price of the impression will be booked as spend. This is irrespective of whether the actual OpenRTB win notice URL is delegated to the client for firing or some other tracking URL is used."

The billing notification concept has been further developed in the OpenRTB Specification 2.5. Highlighting relevant content from section 4.2.3.

> BEST PRACTICE: The essential function of the win notice is to inform a bidder that they won an auction. It does not necessarily imply ad delivery, creative viewability, or billability. Exchanges are highly encouraged to publish to their bidders, their event triggers, billing policies, and any other meaning they attach to the win notice.
>
> BEST PRACTICE: Firing of the billing notice should be server-side and as “close” as possible to where the exchange books revenue in order to minimize discrepancies between exchange and bidder.

## Protocol summary

A summary of the components required to enable bidding for and purchasing outcomes is as follows:

### Bid request

Xandr will indicate in the bid request that it will accept outcome based bids, which outcomes (views and/or completes), and the rate that the exchange will use to generate an eCPM value for ranking.

### Bid response

Bidder will indicate that the bid is an outcome based bid, specify which outcome (payment_type), specify the outcome based bid price (vCPM for views, CPCV for completes), and provide a billing notify url.

### Win notify

Xandr will indicate that the winning bid was for an outcome, specify which outcome, and quote the winning, outcome-based price that the Bidder will be charged if the ad achieves the desired outcome post-serve. Note that at this point the Bidder is notified of winning the auction and that an impression was served—but they aren’t charged until the outcome is verified.

### Billing notify

After the creative is served and Xandr receives a positive signal that the desired outcome occurred, Xandr calls the billing notify url to indicate that the outcome occured and the Bidder is charged the winning outcome-based price.

## Specification

### Bid request

### Impression AppNexus object

Xandr supports the following fields in the `appnexus` extension object of the `imp` object:

| Field | Type | Description |
|:---|:---|:---|
| `allowed_payment_types` | array of objects | Specifies the allowable payments types for this impression. If this field is not present, then the only allowed payment type is `'impression'`. |

### Allowed payment type object

Xandr supports the following fields in the `allowed_payment_type` object of the impression `ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `payment_type` | integer | Specifies the ID of a payment type that is acceptable for this impression. See [Currently supported payment types](#currently-supported-payment-types) below. |
| `conversion_rate` | double | Optional. Specifies the rate that Xandr will use to convert an outcome-based bid to an impression-based eCPM price for ranking in the auction. A Bidder may use this for internal bid ranking and/or budgeting/pacing. |

#### Currently supported payment types

| ID | Description | Bid Type |
|:---|:---|:---|
| 1 | Impression | CPM |
| 2 | Views - Standard Display | vCPM |
| 6 | Views - Custom Display - 100pv1s | vCPM |
| 8 | Views - Standard Video | vCPM |
| 9 | Views - Custom Video - 100pv50pd | vCPM |
| 10 | Complete – Standard Video | CPCV |

### Bid response

### Bid object

| Field | Type | Description |
|:---|:---|:---|
| `price` | float | (Required) The bid price expressed in CPM.<br>If the `bid_payment_type` is omitted or set to 'Impression', then price is used in the auction and to populate the `${AUCTION_PRICE}` macro.<br>If the `bid_payment_type` is something other than Impression, then price must still be set; however, the `payment_type_price` field will be used in the auction and to populate the `${AUCTION_PRICE}` macro. |
| `nurl` | string | The win notify URL. The Xandr server will call this URL when it receives a client-side notification from the device, which indicates that Xandr won the auction.  This occurs at the same time that Xandr records the impression and is when the Bidder should record a served impression as well.<br><br>**Note**: The win notify does not signify a transaction, just that the impression served. The billing notify will signal a transaction.<br>Win notify URLs sent as HTTPS are not supported and will be treated as HTTP requests.<br><br>The following macros are supported in the notify URL:<br>`${AUCTION_ID}` - Xandr `auction_id_64`<br>`${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response<br>`${AUCTION_IMP_ID}` - ID of the impression from the `impid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_SEAT_ID}` - ID of the winning seat from the `seat` field in the `seatbid` object<br>`${AUCTION_AD_ID}` - ID of the buyer's creative, from the `adid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_PRICE}` - Clearing price of the impression in the currency specified in the `cur` field in the bid response. If `bid_payment_type` is present and something other than Impression, then the `AUCTION_PRICE` will reflect price to be paid only if the billing notify is called.<br>`${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response<br>`${CREATIVE_CODE}` - The `code` field set on the `creative` object via the API when registering a creative<br>`${AN_PAYMENT_TYPE}` - The `payment_type` of bid specified in the `bid_payment_type` field of the bid response |
| `burl` | string | The billing notify URL. The Xandr server will call this URL when it determines that the impression is billable. This event occurs at the same time that Xandr records the buyer cost for the impression. At this point,  the Bidder incurs cost and should record a transaction.<br>Billing notify URL is only relevant for bids that have specified a `bid_payment_type` other than Impression.<br><br>Billing notify URLs sent as HTTPS are not supported and will be treated as HTTP requests.<br><br>The following macros are supported in the billing notify URL:<br>`${AUCTION_ID}` - Xandr `auction_id_64`<br>`${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response<br>`${AUCTION_IMP_ID}` - ID of the impression from the `impid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_SEAT_ID}` - ID of the winning seat from the `seat` field in the `seatbid` object<br>`${AUCTION_AD_ID}` - ID of the buyer's creative from the `adid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_PRICE}` - Clearing price for the `payment_type` specified in the `bid_payment_type` field of the bid response, in the currency specified in the `cur` field in the bid response.<br>`${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response<br>`${CREATIVE_CODE}` - The `code` field set on the `creative` object via the API when registering a creative<br>`${AN_PAYMENT_TYPE}` - The `payment_type` of bid specified in the `bid_payment_type` field of the bid response |

### Bid response AppNexus object

Xandr supports the following fields in the `appnexus` extension object of the bid object:

| Field | Type | Description |
|:---|:---|:---|
| `bid_payment_type` | object | Required to submit Guaranteed Outcomes bid.  Specifies the payment type for which the Bidder is bidding.  If omitted, then Xandr will consider the bid to be for a standard Impression. |

### Bid payment type object

Xandr supports the following fields in the `bid_payment_type` object of the bid response `ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `payment_type` | integer | Specifies the payment type for which the Bidder is bidding and will be billed. If the payment type is not `'impression'`, then a billing notify url must be set on the bid object. See [Currently supported values for bid payment type object](#currently-supported-values-for-bid-payment-type-object) below.|
| `price` | double | Specifies the bid price for the payment type, expressed on an outcome basis (see Bid Type in the [Currently supported values for bid payment type object](#currently-supported-values-for-bid-payment-type-object)) below.<br>For example, if the `payment_type` is set to 2 ('Views - Standard Display'), `price` is interpreted as a vCPM value. It is also the maximum charge, which is only accrued if the creative is served and measured viewable, according to the IAB definition and the Xandr viewability measurement script. <br><br>**Note**: Only USD bids are supported for payment types other than Impression. |

#### Currently supported values for bid payment type object

| ID | Description | Bid Type |
|:---|:---|:---|
| 1 | Impression | CPM |
| 2 | Views - Standard Display | vCPM |
| 6 | Views - Custom Display - 100pv1s | vCPM |
| 8 | Views - Standard Video | vCPM |
| 9 | Views - Custom Video - 100pv50pd | vCPM |
| 10 | Complete – Standard Video | CPCV |
