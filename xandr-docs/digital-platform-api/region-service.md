---
title: Digital Platform API - Region Service
description: Explore the read-only Region service to view information about the regions and states registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Region service

The read-only Region Service allows you to see information about the regions and states registered in the Xandr system, including the country to which each region/state belongs. You can use this service to retrieve region IDs for targeting in campaigns (see `region_targets` in the [Profile Service](profile-service.md)).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/region](https://api.appnexus.com/region) | View all regions. |
| `GET` | [https://api.appnexus.com/region?id=ID](https://api.appnexus.com/region?id=ID) | View a specific region by ID. |
| `GET` | [https://api.appnexus.com/region?name=NAME](https://api.appnexus.com/region?name=NAME) | View a specific region by NAME. |
| `GET` | [https://api.appnexus.com/region?code=CODE](https://api.appnexus.com/region?code=CODE) | View a specific region by CODE. |
| `GET` | [https://api.appnexus.com/region/meta](https://api.appnexus.com/region/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `active` | Boolean | If `true`, the region is available for targeting. If `false`, there is no geolocation data for the region and so delivery is not possible. <br><br>**Note:** Regions may occasionally become `active` or `inactive` based on changes to IP addressing or changes in geolocation technologies, as well as based on changes to geographical borders. |
| `code` | string | **Deprecated.** |
| `country_code` | enum | The [ISO code](https://www.maxmind.com/en/iso3166) for the country to which the region belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |
| `country_id` | int | The ID of the country to which the region belongs. |
| `country_name` | string | The name of the country to which the region belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country names. |
| `id` | int | The ID of the region. |
| `iso_3166_2` | string | The ISO 3166-2 code for the region. |
| `name` | string | The name of the region. |
| `sales_tax_rate_pct` | float | Sales tax for member in region acting as buyer. |

## Examples

### View all regions in Germany

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/region?country_code=DE'
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
                "iso_3166_2": "BW",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 826,
                "name": "Bayern",
                "code": "02",
                "iso_3166_2": "BY",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 827,
                "name": "Bremen",
                "code": "03",
                "iso_3166_2": "HB",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 828,
                "name": "Hamburg",
                "code": "04",
                "iso_3166_2": "HH",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 829,
                "name": "Hessen",
                "code": "05",
                "iso_3166_2": "HE",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 830,
                "name": "Niedersachsen",
                "code": "06",
                "iso_3166_2": "NI",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 831,
                "name": "Nordrhein-Westfalen",
                "code": "07",
                "iso_3166_2": "NW",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 832,
                "name": "Rheinland-Pfalz",
                "code": "08",
                "iso_3166_2": "RP",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 833,
                "name": "Saarland",
                "code": "09",
                "iso_3166_2": "SL",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 834,
                "name": "Schleswig-Holstein",
                "code": "10",
                "iso_3166_2": "SH",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 835,
                "name": "Brandenburg",
                "code": "11",
                "iso_3166_2": "BR",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 836,
                "name": "Mecklenburg-Vorpommern",
                "code": "12",
                "iso_3166_2": "MV",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 837,
                "name": "Sachsen",
                "code": "13",
                "iso_3166_2": "SN",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 838,
                "name": "Sachsen-Anhalt",
                "code": "14",
                "iso_3166_2": "ST",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 839,
                "name": "Thuringen",
                "code": "15",
                "iso_3166_2": "TH",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 840,
                "name": "Berlin",
                "code": "16",
                "iso_3166_2": "BE",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            }
        ]
    }
}
```

### View all regions in Germany and France

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/region?country_code=DE,FR'
{
    "response": {
        "status": "OK",
        "count": 38,
        "start_element": 0,
        "num_elements": 100,
        "regions": [
            {
                "id": 825,
                "name": "Baden-Wurttemberg",
                "code": "01",
                "iso_3166_2": "BW",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 826,
                "name": "Bayern",
                "code": "02",
                "iso_3166_2": "BY",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 827,
                "name": "Bremen",
                "code": "03",
                "iso_3166_2": "HB",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            {
                "id": 828,
                "name": "Hamburg",
                "code": "04",
                "iso_3166_2": "HH",
                "country_id": 59,
                "country_name": "Germany",
                "country_code": "DE",
                "active": true
            },
            ...
            {
                "id": 1070,
                "name": "Aquitaine",
                "code": "97",
                "iso_3166_2": "B",
                "country_id": 78,
                "country_name": "France",
                "country_code": "FR",
                "active": true
            },
            {
                "id": 1071,
                "name": "Auvergne",
                "code": "98",
                "iso_3166_2": "C",
                "country_id": 78,
                "country_name": "France",
                "country_code": "FR",
                "active": true
            },
            {
                "id": 1072,
                "name": "Basse-Normandie",
                "code": "99",
                "iso_3166_2": "P",
                "country_id": 78,
                "country_name": "France",
                "country_code": "FR",
                "active": true
            },
            ...
        ]
    }
}
```

### View all regions that contain `"California"` in their names

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/region?like_name=California'
{
    "response": {
        "status": "OK",
        "count": 3,
        "start_element": 0,
        "num_elements": 100,
        "regions": [
            {
                "id": 2600,
                "name": "Baja California",
                "code": "02",
                "iso_3166_2": "BCN",
                "country_id": 159,
                "country_name": "Mexico",
                "country_code": "MX",
                "active": true
            },
            {
                "id": 2601,
                "name": "Baja California Sur",
                "code": "03",
                "iso_3166_2": "BCS",
                "country_id": 159,
                "country_name": "Mexico",
                "country_code": "MX",
                "active": true
            },
            {
                "id": 3922,
                "name": "California",
                "code": "CA",
                "iso_3166_2": "CA",
                "country_id": 233,
                "country_name": "United States",
                "country_code": "US",
                "active": true
            }
        ]
    }
}
```
