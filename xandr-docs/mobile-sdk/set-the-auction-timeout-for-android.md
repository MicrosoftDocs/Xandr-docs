---
title: Set the Auction Timeout for Android
description: The setAuctionTimeout property defines the time period, in milliseconds, to wait for a bidder to respond to a bid request, failing which the bid request would result in failure. 
ms.custom: android-sdk  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Set the auction timeout for Android

The setAuctionTimeout property defines the time period, in milliseconds, to wait for a bidder to respond to a bid request. If the bidder fails to respond within the value set for the time out period (for example, 500 milliseconds), the bid request would result in failure.

## Property

| Property | Type | Attribute | Description |
|--|--|--|--|
| `setAuctionTimeout` | integer | -- | Set the timeout period in milliseconds |

``` 
public static void setAuctionTimeout(long auctionTimeout)
```

## Example

``` 
SDKSettings.setAuctionTimeout(500)
```
