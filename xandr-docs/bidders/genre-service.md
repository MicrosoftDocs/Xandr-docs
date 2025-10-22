---
title: Bidders - Genre Service
description: Genre Service helps you to view the registered video content genres in the system. Video content fields can be added to line item or deal line item targeting.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Genre service

Use the read-only Genre Service to see what video content genres are registered in the Xandr system. Video content fields can be added to line item or deal line item targeting.

## REST API

| HTTP Method | Endpoint | Description  |
|:---|:---|:---|
| `GET` | `https://api.adnxs.com/video-content-genre` | To view all defined genres |
| `GET` | `https://api.adnxs.com/video-content-genre?id=<id value>` | To view a defined genre |

## JSON fields

| Field | Type | Description  |
|:---|:---|:---|
| `id` | int | The Xandr referential ID associated with the genre |
| `name` | string | **Required on**:  `POST`/`PUT`<br><br>The video taxonomy referential value |
| `last_modified` | timestamp | The time of last modification |

## Example

### To retrieve all defined genres

```
curl -b cookies -c cookies "https://api.adnxs.com/video-content-genre"
{
  "response": {
    "status": "OK",
    "start_element": 0,
    "num_elements": 100,
    "video-content-genres": [
      {
        "id": 1,
        "name": "Horror",
        "last_modified": "2020-09-21 13:59:38"
      },
      {
        "id": 2,
        "name": "Crime",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 3,
        "name": "Game-show",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 4,
        "name": "Documentary",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 5,
        "name": "Romance",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 6,
        "name": "Other-sport",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 7,
        "name": "Talk",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 8,
        "name": "Drama",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 9,
        "name": "Fantasy",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 10,
        "name": "Music",
        "last_modified": "2020-09-21 13:59:39"
      },
      {
        "id": 11,
        "name": "Shopping",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 12,
        "name": "Other",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 13,
        "name": "Action",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 14,
        "name": "Thriller",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 15,
        "name": "News",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 17,
        "name": "Reality",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 18,
        "name": "Comedy",
        "last_modified": "2020-09-21 13:59:40"
      },
      {
        "id": 19,
        "name": "Business",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 20,
        "name": "Cooking",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 21,
        "name": "Sitcom",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 22,
        "name": "Adventure",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 23,
        "name": "Sci-fi",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 25,
        "name": "Football",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 26,
        "name": "Animation",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 27,
        "name": "Baseball",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 28,
        "name": "Basketball",
        "last_modified": "2020-09-21 13:59:41"
      },
      {
        "id": 29,
        "name": "Biography",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 30,
        "name": "History",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 31,
        "name": "Musical",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 32,
        "name": "Mystery",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 33,
        "name": "Soccer",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 34,
        "name": "War",
        "last_modified": "2020-09-21 13:59:42"
      },
      {
        "id": 35,
        "name": "Western",
        "last_modified": "2020-09-21 13:59:42"
      }
    ],
    "count": 33,
    "dbg_info": {
      "warnings": [],
      "version": "1.0.194",
      "output_term": "video-content-genres"
    }
  }
}
```

## Related topics

- [Profile Service](../digital-platform-api/profile-service.md)
- [API Best Practices](../digital-platform-api/api-best-practices.md)
- [API Semantics](../digital-platform-api/api-semantics.md)
