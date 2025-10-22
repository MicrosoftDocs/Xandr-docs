---
title: Digital Platform API - Network Service
description: Use the Network service to view registered video content networks and add video content fields to line item or deal line item targeting.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Network service

Use the read-only Network Service to see what video content networks are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/video-content-network` | To view all defined networks |
| `GET` | `https://api.appnexus.com/video-content-network?id=<id value>` | To view a defined network |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the network |
| `name` | string | The video taxonomy referential value<br>**Required On**: `POST`/`PUT` |
| `last_modified` | timestamp | The time of last modification |

## Example

### To retrieve all defined networks

```
curl -b cookies -c cookies "https://api.appnexus.com/video-content-network"
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-content-networks": [
      {
        "id": 1,
        "name": "Network 1",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 2,
        "name": "Network 2",
        "last_modified": "2020-09-21 13:59:39"
      }
    ],
    "count": 2,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-content-networks"
    }
  }
  }
```

## Related topics

- [Profile Service](./profile-service.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
