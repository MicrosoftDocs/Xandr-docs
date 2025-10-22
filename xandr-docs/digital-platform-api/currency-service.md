---
title: Digital Platform API - Currency Service
description: Clients can reconcile amounts paid or received by them resulting from their transactions through the Xandr platform.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Currency service

> [!WARNING]
> The API Currency Service is available to clients solely to reconcile amounts paid or received by them resulting from their transactions through the Xandr Platform and may not be used by clients for any other purpose.

This is a read-only service that shows you the list of currencies that you can set a line-item or insertion-order to use.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/currency` | View all available currencies |
| `GET` | `https://api.appnexus.com/currency?code=CURRENCY_CODE` | View a specific currency |
| `GET` | `https://api.appnexus.com/currency?code=CURRENCY_CODE&show_rate=true` | View a currency's exchange rate for today |
| `GET` | `https://api.appnexus.com/currency?show_rate=true&code=CURRENCY_CODE&ymd=2012-03-01` | View a currency's exchange rate for a day in the past |

> [!NOTE]
> Exchange rates are sourced **once daily** from [Refinitiv](https://www.lseg.com/en/fx) at approximately **3:00 a.m. UTC**. 

## JSON fields

| Fields | Type | Description |
|:---|:---|:---|
| `as_of` | string | The date and time that [Refinitiv](https://www.lseg.com/en/fx) last updated the exchange rate in UTC. We pull the rates from [Refinitiv](https://www.lseg.com/en/fx)at approximately 3:00 a.m UTC. This is returned only when you pass `show_rate=true`  in the query string. |
| `code` | string | The code for the currency. |
| `description` | string | A description of the currency. |
| `is_exposed` | boolean | If `true`, the currency is exposed. |
| `last_modified` | string | The date and time when the currency was last modified. (See **Note** *) |
| `name` | string | The full name of the currency. |
| `position` | enum | Whether the currency symbol appears before or after the amount. Possible values: `"before"` or `"after"`. |
| `rate_per_usd` | double | The exchange rate. This is returned only when you pass `show_rate=true` in the query string. |
| `symbol` | string | The symbol for the currency, e.g. `"$"` for USD |

> [!NOTE]
> - To show conversion rates, pass `show_rate=true` in the URL. You can also retrieve a past day's rate by passing in `ymd=YYYYMMDD` via the URL.
>
> - \* When querying the currency API (eg: `rate_per_usd`), the service returns all the correct values, with the exception for `last_modified`. The actual rates are accurate, and the API returns updated exchange rates.
>
  > Use the `as_of` column instead of `last_modified` to know the version of the exchange rate being returned.

## Examples

### View all available currencies

```
curl -b cookies -c cookies 'https://api.appnexus.com/currency'
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
            },
            {
                "code": "CAD",
                "symbol": "CDN$",
                "name": "Canadian Dollar (CAD)",
                "description": null,
                "position": "before",
                "last_modified": "2010-08-24 19:29:04",
                "is_exposed": true
            },
            {
                "code": "CNY",
                "symbol": "元",
                "name": "Chinese Yuan (CNY)",
                "description": null,
                "position": "before",
                "last_modified": "2010-08-16 23:07:23",
                "is_exposed": true
            },
                        ...
        ],
        "count": 17,
        "start_element": null,
        "num_elements": null
    }
}
```

### View the EUR exchange rate on January 2, 2024

```
$ curl -b cookies -c cookies  'https://api.appnexus.com/currency?show_rate=true&code=EUR&ymd=2012-03-01'
{
    "response": {
        "status": "OK",
        "currency": {
            "code": "EUR",
            "symbol": "€",
            "name": "Euro (EUR)",
            "description": null,
            "position": "before",
            "last_modified": "2010-08-16 23:07:23",
            "rate_per_usd": 0.7506,
            "as_of": "2024-01-02 11:24:00",
            "is_exposed": true
        },
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```
