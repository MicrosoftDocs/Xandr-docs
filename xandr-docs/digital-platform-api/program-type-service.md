---
title: Digital Platform API - Program Type Service
description: Explore the read-only Program Type service to view video content fields that can be added to line item or deal line item targeting.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Program Type service

Use the read-only Program-Type Service to see what video content program types are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/video-program-type](https://api.appnexus.com/video-program-type) | To view all defined program types. |
| `GET` | [https://api.appnexus.com/video-program-type?id=id_value](https://api.appnexus.com/video-program-type?id=id_value) | To view a defined program type. |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the program type. |
| `name` | string | The video taxonomy referential value.<br>**Required On:** `POST`/`PUT` |
| `last_modified` | timestamp | The time of last modification. |

## Example

### Retrieve all defined program types

```
curl -b cookies -c cookies "https://api.appnexus.com/video-program-type"
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-program-types": [
      {
        "id": 1,
        "name": "Movie",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 2,
        "name": "Series",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 3,
        "name": "Special",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 4,
        "name": "Show",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 5,
        "name": "Event",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 6,
        "name": "Clip",
        "last_modified": "2020-09-21 13:59:43"
      }
    ],
    "count": 6,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-program-types"
    }
  }
  }
```

## Related topics

- [Profile Service](profile-service.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
