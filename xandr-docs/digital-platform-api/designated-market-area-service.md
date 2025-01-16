---
title: Designated Market Area Service
description: Use the read-only Designated Market Area service to retrieve the IDs of designated market areas for targeting in campaigns.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Designated Market Area service

The read-only Designated Market Area (DMA) Service allows you to retrieve the IDs of designated market areas for targeting in campaigns (see `dma_targets` in the [Profile Service](./profile-service.md)).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/dma` | View all designated market areas |
| `GET` | `https://api.appnexus.com/dma?id=ID` | View a specific designated market area |
| `GET` | `https://api.appnexus.com/dma?name=NAME` | View a specific designated market area |
| `GET` | `https://api.appnexus.com/dma?like_name=XX` | View all designated market areas in a specific state where `XX` is the state code |
| `GET` | `https://api.appnexus.com/dma/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `active` | Boolean | If `true`, the DMA is available for targeting. If false, there is no geolocation data for the DMA and so delivery is not possible. |
| `code` | string | The code of the DMA. |
| `country_code` | string | The [ISO code](https://dev.maxmind.com/geoip/release-notes/2022#geoip-legacy-databases-have-been-retired) for the country/region to which the DMA belongs. You can use the [Country Service](./country-service.md) to retrieve a complete list of country codes. |
| `country_id` | int | The ID of the country/region to which the DMA belongs. You can use the [Country Service](./country-service.md) to retrieve a complete list of country IDs. |
| `country_name` | string | The name of the country/region to which the DMA belongs. You can use the [Country Service](./country-service.md) to retrieve a complete list of country/region names. |
| `id` | int | The ID of the DMA. |
| `name` | string | The name of the DMA. |

## Example

### View all designated market areas

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/dma'
{
    "response": {
        "status": "OK",
        "count": 211,
        "start_element": null,
        "num_elements": null,
        "dmas": [
            {
                "id": 500,
                "code": 500,
                "name": "Portland-Auburn ME",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 501,
                "code": 501,
                "name": "New York NY",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 502,
                "code": 502,
                "name": "Binghamton NY",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 503,
                "code": 503,
                "name": "Macon GA",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 504,
                "code": 504,
                "name": "Philadelphia PA",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 505,
                "code": 505,
                "name": "Detroit MI",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            {
                "id": 506,
                "code": 506,
                "name": "Boston MA-Manchester NH",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true,
                "last_modified": "2013-02-15 14:16:07"
            },
            ...
        ]
    }
}
```
