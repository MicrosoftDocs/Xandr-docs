---
title: Digital Platform API - Rating Service
description: Explore the read-only Rating Service to view what video content ratings are registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Rating service

Use the read-only Rating Service to see what video content ratings are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/video-content-rating](https://api.appnexus.com/video-content-rating) | To view all defined ratings. |
| `GET` | [https://api.appnexus.com/video-content-rating?id=id_value](https://api.appnexus.com/video-content-rating?id=id_value) | To view a defined rating. |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with rating. |
| `name` | string | The video taxonomy referential value.<br>**Required On:** `POST`/`PUT` |
| `last_modified` | timestamp | The time of last modification. |

## Example

### Retrieve all defined ratings

```
curl -b cookies -c cookies "https://api.appnexus.com/video-content-rating"  
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-content-ratings": [
      {
        "id": 1,
        "name": "all",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 2,
        "name": "children",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 3,
        "name": "teens",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 4,
        "name": "young_adults",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 5,
        "name": "adults",
        "last_modified": "2020-09-21 13:59:38"
      }
    ],
    "count": 5,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-content-ratings"
    }
  }
  }
```

## Related topics

- [Profile Service](profile-service.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
