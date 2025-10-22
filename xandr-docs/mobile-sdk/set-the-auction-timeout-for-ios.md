---
title: Set the Auction Timeout for iOS
description: This page covers how the setAuctionTimeout property defines the time period, in milliseconds, to wait for a bidder to respond to a bid request. If the bidder fails to respond, the bid request will fail. 
ms.custom: ios-sdk 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Set the auction timeout for iOS

The setAuctionTimeout property defines the time period, in milliseconds, to wait for a bidder to respond to a bid request. If the bidder fails to respond within the value set for time out period (for example, 500 milliseconds), the bid request would result in failure.

## Property

| Property | Type | Attribute | Description |
|--|--|--|--|
| `setAuctionTimeout` | Integer | readwrite | Set the timeout period in milliseconds |

``` 
@property (nonatomic, readwrite, assign) NSUInteger auctionTimeout;
```

## Example

``` 
[[ANSDKSettings sharedInstance] setAuctionTimeout:500];
```
