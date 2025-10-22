---
title: Bidders - Rating Service
description: In this article, find information about the Rating Service and the fields associated with it along with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Rating service

Use the read-only Rating Service to see what video content ratings are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|---|---|---|
| GET | `https://api.adnxs.com/video-content-rating` | To view all defined ratings |
| GET | `https://api.adnxs.com/video-content-rating?id=<id value>` | To view a defined rating |

## JSON fields

| Field | Type | Description  |
|---|---|---|
| `id` | int | The Xandr referential ID associated with rating |
| `last_modified` | timestamp | The time of last modification |
| `name` | string | **Required on POST/PUT** <br> The video taxonomy referential value |

## Example

### To retrieve all defined ratings  
  
```
curl -b cookies -c cookies "https://api.adnxs.com/video-content-rating"  
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

- [Profile Service](../digital-platform-api/profile-service.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
