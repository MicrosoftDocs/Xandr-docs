---
title: Creative Custom Request Template Type Service
description: In this article, learn about the Creative Custom Request Template Type service, their JSON fields, and REST API with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Creative Custom Request Template Type service

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

The Creative Custom Request Template Type Service is a read-only service that lists the specific types of creative custom request templates needed to integrate with various ad servers. When you create a new custom request template using the [Creative Custom Request Template Service](creative-custom-request-template-service.md), you must specify that your template is one of the types listed by this service. Together they describe how to make requests to that ad server that use the correct query string parameters and are populated with the correct creative macros.

For more information, see the [Creative Custom Request Template Service](creative-custom-request-template-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET`  | [https://api.appnexus.com/creative-custom-request-template-type](https://api.appnexus.com/creative-custom-request-template-type) | View all template types. |
| `GET` | [https://api.appnexus.com/creative-custom-request-template-type?id=TEMPLATE_TYPE_ID](https://api.appnexus.com/creative-custom-request-template-type?id=TEMPLATE_TYPE_ID) | View an individual template type. |
| `GET` | [https://api.appnexus.com/creative-custom-request-template-type/meta](https://api.appnexus.com/creative-custom-request-template-type/meta) | See all of the available fields, and whether they can be filtered or sorted. |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of this template type.<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `name` | string | The internal name of the template type as used by our systems.<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `display_name` | string | The "print name" of the template type, suitable for a user interface.<br>**Sort by:** Yes<br>**Filter by:** Yes |
| `last_modified` | date | The date and time at which this template type was last updated.<br>**Sort by:** Yes<br>**Filter by:** Yes |

## Examples

### View all template types

```
{code}
$ curl -b cookies 'https://api.appnexus.com/creative-custom-request-template-type'
{
    "response": {
        "status": "OK",
        "count": 5,
        "start_element": 0,
        "num_elements": 100,
        "creative-custom-request-templates-types": [
            {
                "id": 1,
                "name": "none",
                "display_name": "",
                "last_modified": "2013-07-10 14:04:57"
            },
            {
                "id": 2,
                "name": "inmobi",
                "display_name": "InMobi",
                "last_modified": "2013-07-10 14:04:57"
            },
            {
                "id": 3,
                "name": "millenial",
                "display_name": "Millenial Media",
                "last_modified": "2013-07-10 14:04:57"
            },
            {
                "id": 4,
                "name": "mojiva",
                "display_name": "Mojiva",
                "last_modified": "2013-07-10 14:04:57"
            },
            {
                "id": 5,
                "name": "jumptap",
                "display_name": "Jumptap",
                "last_modified": "2013-07-10 14:04:57"
            }
        ],
        "dbg_info": {
            "instance": "29.bm-hbapi.prod.nym1",
            "slave_hit": false,
            "db": "master",
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 43.544054031372,
            "start_microtime": 1373907586.5736,
            "version": "1.13.53",
            "slave_miss": "no_service_index",
            "slave_lag": 0,
            "member_last_modified_age": 1373907586
        }
    }
}
{code}
```

### View an individual template type

```
{code}
$ curl -b cookies https://api.appnexus.com/creative-custom-request-template-type?id=1
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "creative-custom-request-template-type": {
            "id": 1,
            "name": "none",
            "display_name": "",
            "last_modified": "2013-07-10 14:04:57"
        },
        "dbg_info": {
            "instance": "29.bm-hbapi.prod.nym1",
            "slave_hit": false,
            "db": "master",
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 223.9089012146,
            "start_microtime": 1373908192.0697,
            "version": "1.13.53",
            "slave_miss": "no_service_index",
            "slave_lag": 0,
            "member_last_modified_age": 1373908192
        }
    }
}
{code}
```

## Related topics

- [Creative Custom Request Template Service](creative-custom-request-template-service.md)
- [Creative Custom Request Template Parameters](creative-custom-request-template-parameters.md)
