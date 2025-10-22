---
title: Digital Platform API - Duration Service
description: Use the Duration service to see what video content durations are registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Duration service

Use the read-only Duration Service to see what video content durations are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/video-content-duration` | To view all defined durations |
| `GET` | `https://api.appnexus.com/video-content-duration?id=<id value>` | To view a defined duration |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the duration |
| `name` | string | The video taxonomy referential value<br>**Required On**: `POST`/`PUT` |
| `last_modified` | timestamp | The time of last modification |

## Example

### To retrieve all defined durations  

```
curl -b cookies -c cookies "https://api.appnexus.com/video-content-duration"
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-content-durations": [
      {
        "id": 1,
        "name": "long-form",
        "last_modified": "2020-09-21 13:59:43"
      },
      {
        "id": 2,
        "name": "short-form",
        "last_modified": "2020-09-21 13:59:43"
      }
    ],
    "count": 2,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-content-durations"
    }
  }
  } 
```

## Related topics

- [Profile Service](./profile-service.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
