---
title: Bidders - City Service
description: Learn how the read-only City Service allows you to see information about the cities registered in the Xandr system.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Bidders - City service

The read-only City Service allows you to see information about the cities registered in the Xandr system, including the region, designated market area, and country or region to which each city belongs. You can use this service to retrieve the IDs of cities for targeting in campaigns (see `city_targets` in the [Enhanced Bidder Profiles](enhanced-bidder-profiles.md)).

## REST API

| HTTP Methods | Endpoint | Example |
|--|--|--|
| GET | [https://api.adnxs.com/city](https://api.adnxs.com/city) | View all cities. |
| GET | [https://api.adnxs.com/city?country_code=COUNTRY_CODE](https://api.adnxs.com/city?country_code=COUNTRY_CODE) | View all cities in a specific country or region. |
| GET | [https://api.adnxs.com/city?country_name=COUNTRY_NAME](https://api.adnxs.com/city?country_name=COUNTRY_NAME) | View all cities in a specific country or region. |
| GET | [https://api.adnxs.com/city?dma_id=DMA_ID](https://api.adnxs.com/city?dma_id=DMA_ID) | View all cities in a specific designated market area. |
| GET | [https://api.adnxs.com/city?dma_name=DMA_NAME](https://api.adnxs.com/city?dma_name=DMA_NAME) | View all cities in a specific designated market area. |
| GET | [https://api.adnxs.com/city?id=ID](https://api.adnxs.com/city?id=ID) | View a specific city. |
| GET | [https://api.adnxs.com/city?name=NAME](https://api.adnxs.com/city?name=NAME) | View a specific city. |
| GET | [https://api.adnxs.com/city/meta](https://api.adnxs.com/city/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `country_code` | enum | The [ISO code](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) for the country or region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |
| `country_name` | string | The name of the country or region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country or region names. |
| `dma_id` | int | The ID of the designated market area to which the city belongs. You can use the [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md) to retrieve a complete list of dma IDs. |
| `dma_name` | string | The name of the designated market area to which the city belongs. You can use the [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md) to retrieve a complete list of dma names. |
| `id` | int | The ID of the city. |
| `name` | string | The name of the city. |
| `region_id` | int | The ID of the region to which the city belongs. You can use the [Region Service](region-service.md) to retrieve a complete list of region IDs. |
| `region_name` | string | The name of the region to which the city belongs. You can use the [Region Service](region-service.md) to retrieve a complete list of region names. |

## Examples

**View all cities in Germany**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/city?country_code=DE'
{
    "response": {
        "status": "OK",
        "count": 19786,
        "start_element": null,
        "num_elements": null,
        "cities": [
            {
                "id": 36677,
                "country_code": "DE",
                "name": "Aach",
                "region_name": "Baden-Wurttemberg",
                "region_id": 825,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            {
                "id": 36678,
                "country_code": "DE",
                "name": "Aalen",
                "region_name": "Baden-Wurttemberg",
                "region_id": 825,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            {
                "id": 36679,
                "country_code": "DE",
                "name": "Abstatt",
                "region_name": "Baden-Wurttemberg",
                "region_id": 825,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}
```

**View all cities in the Bayern region of Germany**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/city?region_name=Bayern'
{
    "response": {
        "status": "OK",
        "count": 3799,
        "start_element": null,
        "num_elements": null,
        "cities": [
            {
                "id": 39026,
                "country_code": "DE",
                "name": "Abenberg",
                "region_name": "Bayern",
                "region_id": 826,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            {
                "id": 39027,
                "country_code": "DE",
                "name": "Abensberg",
                "region_name": "Bayern",
                "region_id": 826,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            {
                "id": 39028,
                "country_code": "DE",
                "name": "Absberg",
                "region_name": "Bayern",
                "region_id": 826,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}
```

**View all cities named "Karlsruhe"**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/city?name=Karlsruhe'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": null,
        "num_elements": null,
        "cities": [
            {
                "id": 37739,
                "country_code": "DE",
                "name": "Karlsruhe",
                "region_name": "Baden-Wurttemberg",
                "region_id": 825,
                "dma_name": "Other DMA",
                "dma_id": -1,
                "country_name": "Germany"
            },
            {
                "id": 195431,
                "country_code": "US",
                "name": "Karlsruhe",
                "region_name": "North Dakota",
                "region_id": 3952,
                "dma_name": "Minot-Bismarck-Dickinson(Williston) ND",
                "dma_id": 687,
                "country_name": "United States"
            }
        ],
        "dbg_info": {
            ...
        }
    }
} 
```
