---
title: Bidders - Program Type Service
description: In this article, find information about the Program-Type Service and the fields associated with it along with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Program type service

Use the read-only Program-Type Service to see what video content program types are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|---|---|---|
| GET | `https://api.adnxs.com/video-program-type` | To view all defined program types |
| GET | `https://api.adnxs.com/video-program-type?id=<id value>` | To view a defined program type |

## JSON fields

| Field | Type | Description  |
|---|---|---|
| `id` | int | The Xandr referential ID associated with the program type |
| `last_modified` | timestamp | The time of last modification |
| `name` | string | **Required on POST/PUT** <br> The video taxonomy referential value |

## Example

### To retrieve all defined program types  
  
```
curl -b cookies -c cookies "https://api.adnxs.com/video-program-type"
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

- [Profile Service](../digital-platform-api/profile-service.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
