---
title: Digital Platform API - Carrier Service
description: In this article, learn about the Digital Platform API's Carrier service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Carrier service

Mobile carriers, also known as wireless carriers or mobile network operators, own or control all the elements necessary to sell and deliver wireless communication services to users of mobile devices. The read-only Mobile Carrier Service allows you to see what mobile carriers are registered in our system. You can use this service to retrieve the IDs of carriers for targeting in mobile campaigns.

> [!NOTE]
> You can target mobile campaigns based on the make and model of mobile devices as well. For more details, see the [Device Make Service](device-make-service.md) and [Device Model Service](device-model-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/carrier](https://api.appnexus.com/carrier) | View all carriers. |
| `GET` | [https://api.appnexus.com/carrier?country_code=COUNTRY_CODE](https://api.appnexus.com/carrier?country_code=COUNTRY_CODE) | View all carriers in a specific country or region. |
| `GET` | [https://api.appnexus.com/carrier?id=CARRIER_ID](https://api.appnexus.com/carrier?id=CARRIER_ID) | View a specific carrier. |
| `GET` | [https://api.appnexus.com/carrier/meta](https://api.appnexus.com/carrier/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the mobile carrier. |
| `name` | string | The name of the mobile carrier. |
| `country_code` | enum | The [ISO code](https://www.maxmind.com/en/iso3166) for the country or region in which the carrier operates. |
| `country_name` | string | The name of the country or region in which the carrier operates. |
| `codes` | array of objects | Third-party representations for the mobile carrier. For more details, see [Codes Object](#codes-object) below. |

### Codes object

Each object in the `codes` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the carrier code. |
| `code` | string | The third-party representation for the carrier. |
| `notes` | string | Identification information about the third party. |
| `carrier_id` | int | The ID of the carrier. (This is the same as the `id` field described above.) |

## Examples

### View all mobile carriers

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/carrier'
{
    "response": {
        "status": "OK",
        "count": 143,
        "start_element": null,
        "num_elements": 10,
        "carriers": [
            {
                "id": 1,
                "name": "WIFI",
                "country_code": "",
                "is_aggregated": false,
                "codes": null
            },
            {
                "id": 2,
                "name": "Verizon - AR",
                "country_code": "AR",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 3,
                "name": "Verizon - AU",
                "country_code": "AU",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 4,
                "name": "Verizon - CA",
                "country_code": "CA",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 5,
                "name": "Verizon - DE",
                "country_code": "DE",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 6,
                "name": "Verizon - FR",
                "country_code": "FR",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 7,
                "name": "Verizon - GB",
                "country_code": "GB",
                "is_aggregated": true,
                "codes": null
            },
            ...
        ],
        
    }
}
{code}
```

### View all mobile carriers in the US

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/carrier?country_code=US'
{
    "response": {
        "status": "OK",
        "count": 7,
        "start_element": null,
        "num_elements": null,
        "carriers": [
            {
                "id": 14,
                "name": "Verizon - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 26,
                "name": "Sprint - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 40,
                "name": "Orange - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 55,
                "name": "T-Mobile - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 60,
                "name": "AT&T - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 90,
                "name": "Vodafone - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            },
            {
                "id": 108,
                "name": "Telefonica - US",
                "country_code": "US",
                "is_aggregated": true,
                "codes": null
            }
        ]
    }
}
{code}
```

### View a specific mobile carrier

```
{code}
$ curl -b cookies -c cookies 'https://api.appnexus.com/carrier?id=1'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "carriers": [
            {
                "id": 1,
                "name": "WIFI",
                "country_code": null,
                "codes": null
            }
        ]
    }
}
{code}
```
