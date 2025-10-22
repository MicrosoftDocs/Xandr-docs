---
title: Bidders - Network Service
description: In this article, learn about bidders network service, their JSON fields, and REST API with a detailed set of example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Network service

Use the read-only Network Service to see what video content networks are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | `https://api.adnxs.com/video-content-network` | To view all defined networks. |
| `GET` | `https://api.adnxs.com/video-content-network?id=id_value` | To view a defined network. |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the network. |
| `name` | string | **Required on:** `POST`/`PUT`<br>The video taxonomy referential value. |
| `last_modified` | timestamp | The time of last modification. |

## Example

### Retrieve all defined networks

```
curl -b cookies -c cookies "https://api.adnxs.com/video-content-network"
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

- [Profile Service](../digital-platform-api/profile-service.md)
- [API Best Practices](../digital-platform-api/api-best-practices.md)
- [API Semantics](../digital-platform-api/api-semantics.md)
