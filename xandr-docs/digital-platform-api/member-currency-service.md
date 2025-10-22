---
title: Member Currency Service
description: Member Currency service is read-only and shows you the list of currencies used by a member's publisher.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member Currency service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This is a read-only service that shows you the list of currencies used by a member's publishers. For more details about a currency, see [Currency Service](./currency-service.md).

## REST API

| HTTP Methods | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/member-currency?member_id=MEMBER_ID` | View all available currencies |

## JSON fields

| Fields | Type | Description |
|:---|:---|:---|
| `currencies` | array | An array of currency symbols that represent all the currencies used by this member's active (not deleted) publishers. |

## Example

### View all currencies for a member

```
curl -b cookies -c cookies 'https://api.appnexus.com/member-currency?member_id=958'
{
    "response": {
        "status": "OK",
        "currencies": [
            "USD",
            "EUR",
            "NOK",
            "CAD",
            "GBP",
            "AUD",
            "PHP",
            "CNY",
            "INR",
            "JPY",
            "TWD",
            "CHF",
            "TRY",
            "SEK"
        ]
    }
}
```
