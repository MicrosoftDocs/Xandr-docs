---
title: Bidders - Region Service
description: In this article, find information about the Region Service and the fields associated with it along with examples.
ms.date: 10/28/2023
---

# Bidders - Region service

The read-only Region Service allows you to see information about the regions and states registered in the Xandr system, including the country or region to which each region/state belongs. You can use this service to retrieve region IDs for targeting in [profiles](legacy-bidder-profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/region` | View all regions. |
| GET | `https://api.adnxs.com/region?id=ID` | View a specific region. |
| GET | `https://api.adnxs.com/region?name=NAME` | View a specific region. |
| GET | `https://api.adnxs.com/region?code=CODE` | View a specific region. |
| GET | `https://api.adnxs.com/region/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `code` | enum | The ISO or FIPS code for the region. |
| `country_code` | enum | The [ISO code](https://www.maxmind.com/en/iso3166) for the country or region to which the region belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |
| `country_id` | int | The ID of the country or region to which the region belongs. |
| `country_name` | string | The name of the country or region to which the region belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country names. |
| `id` | int | The ID of the region. |
| `name` | string | The name of the region. |

## Examples

### View all regions in Germany

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/region?country or region_code=DE'
{
    "response": {
        "status": "OK",
        "count": 16,
        "start_element": null,
        "num_elements": null,
        "regions": [
            {
                "id": 825,
                "name": "Baden-Wurttemberg",
                "code": "01",                
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 826,
                "name": "Bayern",
                "code": "02",                
                "country_id": 69,                
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 827,
                "name": "Bremen",
                "code": "03",
                "country_id": 69,                                
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 828,
                "name": "Hamburg",
                "code": "04",
                "country_id": 69,                                
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 829,
                "name": "Hessen",
                "code": "05",
                "country_id": 69,                                                
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 830,
                "name": "Niedersachsen",
                "code": "06",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 831,
                "name": "Nordrhein-Westfalen",
                "code": "07",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 832,
                "name": "Rheinland-Pfalz",
                "code": "08",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 833,
                "name": "Saarland",
                "code": "09",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 834,
                "name": "Schleswig-Holstein",
                "code": "10",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 835,
                "name": "Brandenburg",
                "code": "11",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 836,
                "name": "Mecklenburg-Vorpommern",
                "code": "12",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 837,
                "name": "Sachsen",
                "code": "13",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 838,
                "name": "Sachsen-Anhalt",
                "code": "14",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 839,
                "name": "Thuringen",
                "code": "15",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 840,
                "name": "Berlin",
                "code": "16",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            }
        ],
        "dbg_info": {
            ...
        }
    }
}
```

### View all regions in Germany and France

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/region?country_code=DE,FR'
{
    "response": {
        "status": "OK",
        "count": 38,
        "start_element": null,
        "num_elements": null,
        "regions": [
            {
                "id": 825,
                "name": "Baden-Wurttemberg",
                "code": "01",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 826,
                "name": "Bayern",
                "code": "02",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 827,
                "name": "Bremen",
                "code": "03",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            {
                "id": 828,
                "name": "Hamburg",
                "code": "04",
                "country_id": 69,
                "country_code": "DE",
                "country_name": "Germany"
            },
            ...
            {
                "id": 1070,
                "name": "Aquitaine",
                "code": "97",
                "country_id": 78,
                "country_code": "FR",
                "country_name": "France"
            },
            {
                "id": 1071,
                "name": "Auvergne",
                "code": "97",
                "country_id": 78,
                "country_code": "FR",
                "country_name": "France"
            },
            {
                "id": 1072,
                "name": "Basse-Normandie",
                "code": "99",
                "country_id": 78,
                "country_code": "FR",
                "country_name": "France"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}
```

### View all regions that contain "California" in their names

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/region?like_name=California'
{
    "response": {
        "status": "OK",
        "count": 3,
        "start_element": null,
        "num_elements": null,
        "regions": [
            {
                "id": 2600,
                "name": "Baja California",
                "code": "02",
                "country_id": 42,
                "country_code": "MX",
                "country_name": "Mexico"
            },
            {
                "id": 2601,
                "name": "Baja California Sur",
                "code": "03",
                "country_id": 42,
                "country_code": "MX",
                "country_name": "Mexico"
            },
            {
                "id": 3922,
                "name": "California",
                "code": "CA",
                "country_id": 233,
                "country_code": "US",
                "country_name": "United States"
            }
        ]
    }
}
```
