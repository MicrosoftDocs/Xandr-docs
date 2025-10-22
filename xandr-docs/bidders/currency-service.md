---
title: Bidders - Currency Service
description: This page covers Currency service that shows you the list of currencies that you can set a line-item or insertion-order to use. This page also lists code examples for viewing all available currencies.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Currency service

> [!WARNING]
> The API Currency Service is available to clients solely to reconcile amounts paid or received by them resulting from their transactions through the Xandr Platform and may not be used by clients for any other purpose.

This is a read-only service that shows you the list of currencies that you can set a line-item or insertion-order to use.

For buy side Open RTB for bidders, you can send currencies other than USD in the outgoing bid request to bidders and accept other currencies in the response. In order for a bidder to change currency of their bid, they must send the `"cur"` field. If the `"cur"` field is not specified, it will be defaulted to USD. A bidder can respond with any currency, regardless of what value is set in the default currency. They just need to indicate the currency in the `"cur"` field and no additional enablement is required.

For sell side Open RTB, by default USD is used as currency where the `"cur"` field is ignored. If the seller member has a member entitlement for `seller_bid_currency` explicitly set up, the `"cur"` field in bid requests is respected.

Exchange rates are sourced **once daily** from [Refinitiv](https://www.lseg.com/en/fx) at approximately **3:00 a.m. UTC**. 

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| `GET` | `https://api.appnexus.com/currency` | View all available currencies |
| `GET` | `https://api.appnexus.com/currency?code=CURRENCY_CODE` | View a specific currency |
| `GET` | `https://api.appnexus.com/currency?code=CURRENCY_CODE&show_rate=true` | View a currency's exchange rate for today |
| `GET` | `https://api.appnexus.com/currency?show_rate=true&code=CURRENCY_CODE&ymd=2012-03-01` | View a currency's exchange rate for a day in the past |

## JSON fields

| Fields | Type | Description |
|--|--|--|
| `as_of` | string | The date and time that [Refinitiv](https://www.lseg.com/en/fx) last updated the exchange rate in UTC. We pull the rates from [Refinitiv](https://www.lseg.com/en/fx) every day at 3:00 a.m. UTC. This is returned only when you pass `show_rate=true` in the query string. |
| `code` | string | The code for the currency. |
| `description` | string | A description of the currency. |
| `is_exposed` | boolean | If `true`, the currency is exposed. |
| `last_modified` | string | The date and time when the currency was last modified. (See **Note** *) |
| `name` | string | The full name of the currency. |
| `position` | enum | Whether the currency symbol appears before or after the amount. Possible values: `"before"` or `"after"`. |
| `rate_per_usd` | double | The exchange rate. This is returned only when you pass `show_rate=true` in the query string. |
| `symbol` | string | The symbol for the currency, e.g. "`$"` for USD |

To show conversion rates, pass `show_rate=true` in the URL. You can also retrieve a past day's rate by passing in `ymd=YYYYMMDD` via the URL.

> [!NOTE]
>
> *When querying the currency API (eg: `rate_per_usd`), the service is currently returning all the correct values, with the exception for `last_modified`. The actual rates are accurate, and the API is returning updated exchange rates. Currently, use the `as_of` column instead of `last_modified` to know the version of the exchange rate being returned.

## Examples

**View all available currencies**

``` 
curl -b cookies -c cookies 'https://api.adnxs.com/currency'
{
    "response": {
        "status": "OK",
        "currencies": [
            {
                "code": "ARS",
                "symbol": "₱",
                "name": "Argentine Peso (ARS)",
                "description": null,
                "position": "before",
                "last_modified": "2010-08-16 23:07:23",
                "is_exposed": true
            },
            {
                "code": "AUD",
                "symbol": "AUD$",
                "name": "Australian Dollar (AUD)",
                "description": null,
                "position": "before",
                "last_modified": "2010-08-24 19:29:04",
                "is_exposed": true
            },
            {
                "code": "BRL",
                "symbol": "R$",
                "name": "Brazilian Real (BRL)",
                "description": null,
                "position": "before",
                "last_modified": "2010-08-16 23:07:23",
                "is_exposed": true
            }
                        ...
        ],
        "count": 17,
        "start_element": null,
        "num_elements": null
    }
}
```

**View the EUR exchange rate on March 1, 2020**

``` 
$ curl -b cookies -c cookies  'https://api.adnxs.com/currency?show_rate=true&code=EUR&ymd=2020-03-01'
{
    "response": {
        "status": "OK",
        "currency": {
            "code": "EUR",
            "symbol": "€",
            "name": "Euro (EUR)",
            "description": null,
            "position": "before",
            "last_modified": "2020-02-16 23:07:23",
            "rate_per_usd": 0.7506,
            "as_of": "2020-03-01 11:24:00",
            "is_exposed": true
        },
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```
