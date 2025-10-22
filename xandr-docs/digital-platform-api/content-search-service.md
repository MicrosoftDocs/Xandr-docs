---
title: Content Search Service
description: In this article, learn about the Content Search service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Content Search service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

Xandr admins can use this read-only service to search for creative IDs that have not been deleted and have not expired, based on the `content` and `media_url` attributes of a creative.

> [!NOTE]
> After using this service to retrieve creative IDs, you can use other services to lookup additional data. For example, to find out who a particular creative belongs to, you would make a `GET` call with the creative ID to the [Creative Service](creative-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com//creative-content-search?q=xxx](https://api.appnexus.com//creative-content-search?q=xxx) | Search for creative IDs based on terms in `content` and `media_url`. |

### Rules

- **For creative IDs to be returned, ALL search terms must match either** `content` **or** `media_url`**.**
- **Queries must be between 3 and 15 characters.** Queries outside this range will not return results.
- **This service does not return expired creatives.**
- **This service returns only creative IDs.** If more information is required; such as who the creative belongs to, or if you want to join the creative table with other tables, use the IDs returned in future queries/lookups. For more details, see the [example](#example) below.

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative. |

## Example

### Get creative IDs for the 'adnxs' search parameter

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-content-search?q=adnxs'
{
  "response": {
    "status": "OK",
    "num_elements": 100,
    "start_element": 0,
    "count": 516001,
    "results": [
      {
        "id": 17500999
      },
      {
        "id": 17501020
      },
      {
        "id": 17501040
      },
      {
        "id": 17501052
      },
      {
        "id": 17501060
      },
        ...
    ],
    "dbg_info": {
      "instance": "63.bm-hbapi.prod.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [],
      "time": 154.0949344635,
      "start_microtime": 1423773726.0317,
      "version": "1.15.368",
      "s1ave_miss": "no_service_index",
      "s1ave_lag": 0,
      "member_last_modified_age": 1423773726,
      "output_term": "not_found"
    }
  }
}
```
