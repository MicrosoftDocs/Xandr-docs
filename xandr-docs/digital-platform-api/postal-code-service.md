---
title: Digital Platform API - Postal Code Service
description: Explore the read-only Postal Code service to retrieve postal code IDs registered for geography targeting and configuring dimension-supported reports.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Postal Code service

The Postal Code Service is a read-only service. This service can be used to retrieve postal code IDs, that are registered with Xandr for geography targeting purposes when setting up a or for configuring reports that support that dimension. The main use case for the Postal Code Service is to keep your postal code database up-to-date with Xandr's. To access the changes that were made to the database since the last call that you made to the service, make sure to use the `min_last_modified` field in your call.

> [!WARNING]
> Due to the large number of `GET` calls you would need to make to obtain a complete list of postal codes (as a result of pagination), we recommend the following:
>
> - Create a cache and populate it with a `GET` call for all objects on the service.
> - Then, for subsequent `GET` calls, use the `min_last_modified` filter to obtain updates (once per hour or once per day, since postal codes are updated infrequently).
>
> You should only omit the `min_last_modified` filter if you are querying this service for the first time.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/postal-code](https://api.appnexus.com/postal-code) | View all postal codes using [pagination](05---throttling-pagination-and-filtering.md). |
| `GET`  | - [https://api.appnexus.com/postal-code?min_last_modified=LAST_MODIFIED](https://api.appnexus.com/postal-code?min_last_modified=LAST_MODIFIED)<br>- [https://api.appnexus.com/postal-code?max_last_modified=LAST_MODIFIED](https://api.appnexus.com/postal-code?max_last_modified=LAST_MODIFIED) | View all postal codes since last modified. |
| `GET` | [https://api.appnexus.com/postal-code?country_code=COUNTRY_CODE](https://api.appnexus.com/postal-code?country_code=COUNTRY_CODE) | View postal codes in a specific country/region. |
| `GET` | [https://api.appnexus.com/postal-code/meta](https://api.appnexus.com/postal-code/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the postal code. |
| `code` | string | The postal code can be an alphanumeric string of up to 14 characters and can contain a space or hyphen. |
| `country_id` | string | The ID of the country/region. |
| `country_code` | string | The ISO Alpha-2 code for the country/region to which the city belongs. You can use the [country/region Service](country-service.md) to retrieve a complete list of country codes. |
| `country_name` | string | The name of the country/region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country/region names. |
| `last_modified` | timestamp | The date and time when the postal code was last modified. |
| `active` | Boolean | Designates whether the postal code is active. If `true`, the postal code is active and available for targeting. If `false`, there is no geo-location data for the postal code and so targeting is not possible.<br><br>**Note:**<br>The postal codes may occasionally become active or inactive based on changes to IP addressing or changes in geolocation technologies, as well as changes to geographical borders. |

## Examples

### View all postal codes

```
$ curl -b cookies -c cookies -X GET  'https://api.appnexus.com/postal-code'
      
{
    "response": {
        "status": "OK",
        "count": 238899,
        "start_element": 0,
        "num_elements": 100,
        "postal_codes": [
            {
                "id": 120560,
                "code": "AD100",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120561,
                "code": "AD200",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120562,
                "code": "AD300",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120563,
                "code": "AD400",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120564,
                "code": "AD500",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120565,
                "code": "AD600",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 120566,
                "code": "AD700",
                "country_id": "4",
                "country_code": "AD",
                "country_name": "Andorra"
            },
            {
                "id": 173241,
                "code": "1701",
                "country_id": "6",
                "country_code": "AF",
                "country_name": "Afghanistan"
            },
            {
                "id": 173242,
                "code": "3001",
                "country_id": "6",
                "country_code": "AF",
                "country_name": "Afghanistan"
            },
            ...
       ]
    }
}
```

### View all postal codes since last modified

```
$ curl -b cookies -c cookies -X GET  'https://api.appnexus.com/postal-code?min_last_modified=2016-05-18+15:29:37'
      
{
    "response": {
        "status": "OK",
        "count": 247890,
        "start_element": 0,
        "num_elements": 100,
        "postal_codes": [
            {
                "id": 1,
                "code": "00010",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 14:40:30"
            },
            {
                "id": 2,
                "code": "00011",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 14:40:32"
            },
            {
                "id": 3,
                "code": "00012",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 17:29:04"
            },
            {
                "id": 4,
                "code": "00013",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 17:29:04"
            },
            {
                "id": 5,
                "code": "00015",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 17:29:05"
            },
            {
                "id": 6,
                "code": "00017",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 17:29:05"
            },
            {
                "id": 7,
                "code": "00018",
                "active": true,
                "country_id": "113",
                "country_code": "IT",
                "country_name": "Italy",
                "last_modified": "2015-09-15 17:29:05"
            },
            ...
       ]
    }
}
```

### View all postal codes in Canada

```
$ curl -b cookies -c cookies -X GET  'https://api.appnexus.com/postal-code?country_code=CA'
      
{
    "response": {
        "status": "OK",
        "count": 44101,
        "start_element": 0,
        "num_elements": 100,
        "postal_codes": [
            {
                "id": 119892,
                "code": "A09 0A1",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"
            },
            {
                "id": 119893,
                "code": "A0A 0B3",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"
            },
            {
                "id": 119894,
                "code": "A0A 0C3",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"
            },
            {
                "id": 119895,
                "code": "A0A 1B0",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"
            },
            {
                "id": 119896,
                "code": "A0A 1C0",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"
            },
            {
                "id": 119897,
                "code": "A0A 1E0",
                "country_id": "41",
                "country_code": "CA",
                "country_name": "Canada"  
        },
        ...
      ],
   }
}
```

### View postal code by postal code ID

```
$ curl -b cookies -c cookies  'https://api.appnexus.com/postal-code?id=10'
      
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "postal_code": {
            "id": 10,
            "code": "00021",
            "country_id": "113",
            "country_code": "IT",
            "country_name": "Italy",
            "last_modified": "2015-09-15 17:29:05"
        }
    }
    }
```

## Related topics

- [Throttling, Paging, and Filtering](05---throttling-pagination-and-filtering.md)
- [API Semantics](api-semantics.md)
- [City Service](city-service.md)
- [Country Service](country-service.md)
