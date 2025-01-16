---
title: Bidders - Postal Code Service
description: In this article, find information about the Postal code service and the fields associated with it along with examples.
ms.date: 10/28/2023
---

# Bidders - Postal code service

The Postal Code Service is a read-only service. This service can be used to retrieve postal code IDs that are registered with Xandr for geography targeting purposes when setting up a line item or for configuring reports that support that dimension. The main use case for the Postal Code Service is to keep your postal code database up-to-date with Xandr's. To access the changes that were made to the Xandr database since the last call that you made to the service, make sure to use the `min_last_modified` field in your call.

> [!WARNING]
> Due to the large number of GET calls you would need to make to obtain a complete list of postal codes (as a result of pagination), we recommend the following:
>
> - create a cache and populate it with a GET call for all objects on the service
> - then, for subsequent GET calls, use the `min_last_modified` filter to obtain updates (once per hour or once per day, since postal codes are updated infrequently)
>
> You should only omit the `min_last_modified` filter if you are querying this service for the first time.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnxs.com/postal-code` | View all postal codes |
| GET | `https://api.adnxs.com/postal-code?country_code=COUNTRY_CODE` | View postal codes in a specific country or region |
| GET | `https://api.adnxs.com/postal-code/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type (Length) | Description |
|---|---|---|
| `active` | boolean | Designates whether the postal code is active. If `true`, the postal code is active and available for targeting. If `false`, there is no geo-location data for the postal code and so targeting is not possible. |
| `code` | string | The postal code can be an alphanumeric strings of up to 14 characters and can contain a space or hyphen. |
| `country_code` | string | The ISO Alpha-2 code for the country or region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |
| `country_id` | string | The ID of the country or region. |
| `country_name` | string | The name of the country or region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country names. |
| `id` | int | The ID of the postal code. |
| `last_modified` | timestamp | The date and time when the postal code was last modified. |

## Examples

### View all postal codes in Canada

```
$ curl -b cookies -c cookies -X GET  'https://api.adnxs.com/postal-code?country_code=CA'
{
        "response": {
        "status": "OK",
        "count": 44101,
        "start_element": null,
        "num_elements": null,
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
            ...
      ]
   }
}
```

### View postal code by postal code ID

```
$ curl -b cookies -c cookies  'https://api.adnxs.com/postal-code?id=10'
      
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "postal_code": {
            "id": 10,
            "code": "00021",
            "country_id": "113",
            "country_code": "IT",
            "country_name": "Italy"
        }
    }
}
```

### View all postal codes since last modified

```
$ curl -b cookies -c cookies -X GET  'https://api.adnxs.com/postal-code?min_last_modified=2017-06-28+15:02:37
{
    "response": {
        "status": "OK",
        "count": 8735,
        "start_element": null,
        "num_elements": null,
        "postal_codes": [{
            "id": 322567,
            "code": "2645-018",
            "active": true,
            "country_id": "186",
            "country_code": "PT",
            "country_name": "Portugal",
            "last_modified": "2017-06-26 15:39:18"
         },
         {
            "id": 322568,
            "code": "BS5 7XA",
            "active": true,
            "country_id": "80",
            "country_code": "GB",
            "country_name": "United Kingdom",
            "last_modified": "2017-06-26 15:39:18"
         },
         {
            "id": 322569,
            "code": "DE7 8HB",
            "active": true,
            "country_id": "80",
            "country_code": "GB",
            "country_name": "United Kingdom",
            "last_modified": "2017-06-26 15:39:18"
      },
      ...
    ]
  }
}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [City Service](city-service.md)
- [Country Service](country-service.md)
