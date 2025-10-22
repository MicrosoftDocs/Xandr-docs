---
title: Digital Platform API - City Service
description: In this article, learn about the Digital Platform API's City service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - City service

The read-only City Service allows you to see information about the cities registered in the Xandr system, including the region, designated market area, and country to which each city belongs. You can use this service to retrieve the IDs of cities for targeting in campaigns (see `city_targets` in the [Profile Service](profile-service.md)).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/city](https://api.appnexus.com/city) | View all cities. |
| `GET` | [https://api.appnexus.com/city?country_code=COUNTRY_CODE](https://api.appnexus.com/city?country_code=COUNTRY_CODE) | View all cities in a specific country. |
| `GET` | [https://api.appnexus.com/city?country_name=COUNTRY_NAME](https://api.appnexus.com/city?country_name=COUNTRY_NAME) | View all cities in a specific country. |
| `GET` | [https://api.appnexus.com/city?dma_id=DMA_ID](https://api.appnexus.com/city?dma_id=DMA_ID) | View all cities in a specific designated market area. |
| `GET` | [https://api.appnexus.com/city?dma_name=DMA_NAME](https://api.appnexus.com/city?dma_name=DMA_NAME) | View all cities in a specific designated market area. |
| `GET` | [https://api.appnexus.com/city?id=ID](https://api.appnexus.com/city?id=ID) | View a specific city by ID. |
| `GET` | [https://api.appnexus.com/city?name=NAME](https://api.appnexus.com/city?name=NAME) | View a specific city by name. |
| `GET` | [https://api.appnexus.com/city/meta](https://api.appnexus.com/city/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the city. |
| `name` | string | The name of the city. |
| `country_id` | int | The ID of the country to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country IDs. |
| `country_name` | string | The name of the country to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country names. |
| `country_code` | string | The [ISO code](https://www.maxmind.com/en/iso3166) for the country to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |
| `region_id` | int | The ID of the region to which the city belongs. You can use the [Region Service](region-service.md) to retrieve a complete list of region IDs. |
| `region_name` | string | The name of the region to which the city belongs. You can use the [Region Service](region-service.md) to retrieve a complete list of region names. |
| `region_code` | string | The ISO or FIPS code for the region to which the city belongs. You can use the [Region Service](region-service.md) to retrieve a complete list of region codes. |
| `dma_id` | int | The ID of the designated market area to which the city belongs. You can use the [Designated Market Area Service](designated-market-area-service.md) to retrieve a complete list of DMA IDs. |
| `dma_name` | string | The name of the designated market area to which the city belongs. You can use the [Designated Market Area Service](designated-market-area-service.md) to retrieve a complete list of DMA names. |
| `active` | Boolean | If `true`, the city is available for targeting. If `false`, there is no geolocation data for the city and so delivery is not possible. |

## Examples

### View all cities in Germany

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/city?country_code=DE'
{
    "response": {
        "status": "OK",
        "count": 15769,
        "start_element": 0,
        "num_elements": 100,
        "cities": [
            {
                "id": 36677,
                "name": "Aach",
                "region_id": 825,
                "region_name": "Baden-Wurttemberg",
                "region_code": "01",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "dma_id": 1,
                "dma_name": "--",
                "active": true,
                "last_modified": "2015-04-09 19:40:57"
            },
            {
                "id": 36678,
                "name": "Aalen",
                "region_id": 825,
                "region_name": "Baden-Wurttemberg",
                "region_code": "01",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "dma_id": 1,
                "dma_name": "--",
                "active": true,
                "last_modified": "2015-04-09 19:40:57"
            },
            {
                "id": 36679,
                "name": "Abstatt",
                "region_id": 825,
                "region_name": "Baden-Wurttemberg",
                "region_code": "01",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "dma_id": 1,
                "dma_name": "--",
                "active": true,
                "last_modified": "2015-04-09 19:40:57"
            },
            ...
        ]
    }
}
```

### View all cities in the Bayern region of Germany

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/city?region_name=Bayern'
{
  "response": {
    "status": "OK",
    "count": 3066,
    "start_element": 0,
    "num_elements": 100,
    "cities": [
      {
        "id": 39026,
        "name": "Abenberg",
        "region_id": 826,
        "region_name": "Bayern",
        "region_code": "02",
        "country_id": 59,
        "country_name": "Germany",
        "country_code": "DE",
        "dma_id": 1,
        "dma_name": "--",
        "active": true,
        "last_modified": "2015-04-09 19:40:57"
      },
      {
        "id": 39027,
        "name": "Abensberg",
        "region_id": 826,
        "region_name": "Bayern",
        "region_code": "02",
        "country_id": 59,
        "country_name": "Germany",
        "country_code": "DE",
        "dma_id": 1,
        "dma_name": "--",
        "active": true,
        "last_modified": "2015-04-09 19:40:57"
      },
      {
        "id": 39028,
        "name": "Absberg",
        "region_id": 826,
        "region_name": "Bayern",
        "region_code": "02",
        "country_id": 59,
        "country_name": "Germany",
        "country_code": "DE",
        "dma_id": 1,
        "dma_name": "--",
        "active": true,
        "last_modified": "2015-04-09 19:40:57"
      },
      ...
    ]
  }
}
```

### View all cities named "Karlsruhe"

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/city?name=Karlsruhe'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "cities": [
            {
                "id": 37739,
                "name": "Karlsruhe",
                "region_id": 825,
                "region_name": "Baden-Wurttemberg",
                "region_code": "01",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "dma_id": 1,
                "dma_name": "--",
                "active": true,
                "last_modified": "2015-04-09 19:40:57"
            },
            {
                "id": 195431,
                "name": "Karlsruhe",
                "region_id": 3952,
                "region_name": "North Dakota",
                "region_code": "ND",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "dma_id": 687,
                "dma_name": "Minot-Bismarck-Dickinson(Williston) ND",
                "active": false,
                "last_modified": "2016-10-19 05:01:12"
            }
        ]
    }
}
```
