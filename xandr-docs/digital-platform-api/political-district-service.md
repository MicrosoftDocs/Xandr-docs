---
title: Political District Service
description: Explore the Political District service, enabling political buyers to target geographies based on legislative district boundaries.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Political District service

The Political District Service allows political buyers to target geographies based on legislative district boundaries.

The feature is available within the existing geo targeting module in Microsoft Invest, and it's called "Political District (US Only)". It allows political buyers to target the following political geography levels:

- Congressional District
- State Senate District
- State House District  

## REST API

| HTTP Method | Endpoint  | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/political-district?id=DISTRICT_ID](https://api.appnexus.com/political-district?id=DISTRICT_ID) | View an existing political district. |
| `GET` | [https://api.appnexus.com/political-district?search=SEARCH_TERM](https://api.appnexus.com/political-district?search=SEARCH_TERM) | Search a political district (only available for `district_id`, `district_name`, `district_type_id`, `region_id`). |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the political district.  |
| `name` | string | The name of the political district.  |
| `description` | string  | (Optional) The detailed description of political district information. |
| `postal_codes_count` | int | The total number of post codes belonging to a particular district. |
| `postal_code_list_id` | int | The ID of the postal code list associated with political district. |
| `postal_codes` | array of objects | The postal codes that are to be included in the postal code list. <br> See [example](#postal_codes-example).<br>**Required On:** `POST` and `PUT`. |
| `political_district` | array of objects | The list details the complete information for political district. |

#### `postal_codes` example

```
"postal_codes":[
{"id": 1},
{"id": 2},
{"id": 3}
]
```

#### Postal code object

The `postal_codes` object contains the following fields:

| Field | Type (length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the postal code. |
| `code` | string | The postal code, which can be an alphanumeric string containing 5 characters. |
| `country_id` | int | The ID associated with the country. |
| `active` | string | The status of the postal code, which highlights if the postal code is `active`/`inactive`. |
| `country_code` | string | The ISO Alpha-2 code for the country to which the city belongs. To retrieve a complete list of country codes, see [Country Service](country-service.md). |
| `country_name` | string | The name of the country to which the city belongs. To retrieve a complete list of country names, see [Country Service](country-service.md). |

#### Political district object

The `political_district` object contains the following fields:

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the political district. |
| `district_name` | string | The name of the political district. |
| `district_type_id` | int | The type of district. Possible values are:<br>- `Congress`<br>- `State House`<br>- `State Senate` |
| `region_id` | int | The `region_id` is obtained by the API, from the `region_code` which is passed in the request header. |
| `postal_code_list_id` | int | The ID of postal code list. |
| `created_on` | timestamp | **Read Only.**<br>The time of creation of the political district list. |
| `last_modified` | timestamp | **Read Only.**<br>The time of last modification made to the political district list. |
| `country_id` | int | The ID associated with the country. |
| `region_code` | string | The `region_code` is present in the request header which is used by the API to find the `region_id`. |

## Examples

### View an existing political district by ID

```
curl -b cookies -c cookies -s "https://api.appnexus.com/political-district?id=145125" {
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "political-district": {
            "id": 145125,
            "name": "AR State House 012",
            "description": null,
            "postal_codes_count": 7,
            "postal_code_list_id": "145125",
            "postal_codes": [
                {
                    "id": 53520,
                    "code": "72714",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53521,
                    "code": "72715",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53527,
                    "code": "72722",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53535,
                    "code": "72736",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53538,
                    "code": "72739",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53544,
                    "code": "72747",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                },
                {
                    "id": 53563,
                    "code": "72768",
                    "country_id": 233,
                    "active": true,
                    "country_code": "US",
                    "country_name": "United States"
                }
            ],
            "political_district": [
                {
                    "id": 5199,
                    "district_name": "AR State House 012",
                    "district_type_id": 2,
                    "region_id": 3921,
                    "postal_code_list_id": 145125,
                    "created_on": "2022-04-11 16:10:08",
                    "last_modified": "2022-04-11 16:10:08",
                    "country_id": 233
                }
            ]
        },
        "count": 1,
        "dbg_info": {
            "warnings": [],
            "version": "1.1.61",
            "output_term": "political-district"
        }
    }
}
```

### View an existing political district by district name

```
curl -b cookies -c cookies -s "https://api.appnexus.com/political-district?district_name=NY+State+House+001" {    
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "political-districts": [
            {
                "id": 144908,
                "name": "NY State House 001",
                "description": null,
                "postal_codes_count": 36,
                "postal_code_list_id": "144908",
                "postal_codes": [
                    {
                        "id": 8190,
                        "code": "11954",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8191,
                        "code": "11955",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8192,
                        "code": "11956",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8193,
                        "code": "11957",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8194,
                        "code": "11958",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8195,
                        "code": "11959",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8197,
                        "code": "11960",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8199,
                        "code": "11962",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8200,
                        "code": "11963",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8201,
                        "code": "11964",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8202,
                        "code": "11965",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8204,
                        "code": "11968",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8205,
                        "code": "11969",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8207,
                        "code": "11971",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8208,
                        "code": "11972",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8212,
                        "code": "11977",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 8213,
                        "code": "11978",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    }
                ],
                "political_district": [
                    {
                        "id": 4987,
                        "district_name": "NY State House 001",
                        "district_type_id": 2,
                        "region_id": 3950,
                        "postal_code_list_id": 144908,
                        "created_on": "2022-04-11 16:09:07",
                        "last_modified": "2022-04-11 16:09:07",
                        "country_id": 233
                    }
                ]
            }
        ],
        "count": 1,
        "dbg_info": {
            "warnings": [],
            "version": "1.1.61",
            "output_term": "political-districts"
        }
    }
}    
```

### View an existing political district by `postal_code_list_id`

```
$ curl -b cookies -X GET --url 'https://api.appnexus.com/political-district?postal_code_list_id=139897' {
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "political-districts": [
            {
                "id": 139897,
                "name": "AK Congress 01",
                "description": null,
                "postal_codes_count": 267,
                "postal_code_list_id": "139897",
                "postal_codes": [
                    {
                        "id": 70153,
                        "code": "99501",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                    },
                    {
                        "id": 70154,
                        "code": "99502",
                        "country_id": 233,
                        "active": true,
                        "country_code": "US",
                        "country_name": "United States"
                        },
```

## Related topic

[Profile Service](profile-service.md)
