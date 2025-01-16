---
title: Bidders - Country Service
description: Learn how the Country Service allows you to see information about the countries or regions registered in the Xandr system. This page covers examples with code to view all countries or regions, view by ID and view by country code.
ms.date: 11/20/2023

---


# Bidders - Country service

The read-only Country Service allows you to see information about the countries or regions registered in the Xandr system. You can use this service to retrieve the IDs for targeting in [profiles](legacy-bidder-profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| GET | [https://api.adnxs.com/country](https://api.adnxs.com/country) | View all countries or regions. |
| GET | [https://api.adnxs.com/country?id=ID](https://api.adnxs.com/country?id=ID) | View a specific country or region. |
| GET | [https://api.adnxs.com/country?name=NAME](https://api.adnxs.com/country?name=NAME) | View a specific country or region. |
| GET | [https://api.adnxs.com/country?code=CODE](https://api.adnxs.com/country?code=CODE) | View a specific country or region. |
| GET | [https://api.adnxs.com/country/meta](https://api.adnxs.com/country/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `code` | enum | The [ISO code](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) for the country or region. |
| `id` | int | The ID of the country or region. |
| `name` | string | The name of the country or region. |

## Examples

**View all countries or regions**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/country'
{
    "response": {
        "status": "OK",
        "count": 250,
        "start_element": null,
        "num_elements": null,
        "countries": [
            {
                "id": 1,
                "name": "Anonymous Proxy",
                "code": "A1"
            },
            {
                "id": 2,
                "name": "Satellite Provider",
                "code": "A2"
            },
            {
                "id": 3,
                "name": "Other Country",
                "code": "O1"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}         
```

**View a specific country or region by ID**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/country?id=59'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "country": {
            "id": 59,
            "name": "Germany",
            "code": "DE"
        },
        "dbg_info": {
            ...
        }
    }
}
```

**View a specific country or region by code**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/country?code=DE'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "countries": [
            {
                "id": 59,
                "name": "Germany",
                "code": "DE"
            }
        ],
        "dbg_info": {
            ...
        }
    }
}
```

**View all countries or regions that contain "United" in their names**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/country?like_name=United'
{
    "response": {
        "status": "OK",
        "count": 5,
        "start_element": null,
        "num_elements": null,
        "countries": [
            {
                "id": 5,
                "name": "United Arab Emirates",
                "code": "AE"
            },
            {
                "id": 80,
                "name": "United Kingdom",
                "code": "GB"
            },
            {
                "id": 229,
                "name": "Tanzania, United Republic of",
                "code": "TZ"
            },
            {
                "id": 232,
                "name": "United States Minor Outlying Islands",
                "code": "UM"
            },
            {
                "id": 233,
                "name": "United States",
                "code": "US"
            }
        ],
        "dbg_info": {
            ...
        }
    }
}     
```
