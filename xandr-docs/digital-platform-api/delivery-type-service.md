---
title: Digital Platform API - Delivery Type Service
description: Use the read-only Delivery Type service to see what video content delivery types are registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Delivery Type service

Use the read-only Delivery Type Service to see what video content delivery types are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/video-delivery-type` | To view all defined delivery types |
| `GET` |`https://api.appnexus.com/video-delivery-type?id=<id value>` | To view a defined delivery type |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the delivery type |
| `name` | string | The video taxonomy referential value<br>**Required On**: `POST`/`PUT` |
| `last_modified` | timestamp | The time of last modification |

## Example

### To retrieve all defined delivery types

```
curl -b cookies -c cookies "https://api.appnexus.com/video-delivery-type"
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-delivery-types": [
      {
        "id": 1,
        "name": "Live",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 2,
        "name": "VOD",
        "last_modified": "2020-09-21 13:59:43"
      }
    ],
    "count": 2,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-delivery-types"
    }
  }
  }
```

## Related topics

- [Profile Service](./profile-service.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
