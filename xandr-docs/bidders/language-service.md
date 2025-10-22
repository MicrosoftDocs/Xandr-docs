---
title: Bidders - Language Service
description: In this article, learn about bidders language service, their JSON fields, and REST API with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Language service

Use the read-only Language Service to see what languages are registered in the Xandr system. Creatives are tagged with a specific language, and ad profiles can be configured to include/exclude particular languages.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/language](https://api.adnxs.com/language) | To view all the languages. |
| `GET` | [https://api.adnxs.com/language?id=LANGUAGE_ID](https://api.adnxs.com/language?id=LANGUAGE_ID) | To view information about a particular language. |
| `POST` | [https://api.adnxs.com/language](https://api.adnxs.com/language) | To add a language (admin only). |
| `PUT` | [https://api.adnxs.com/language?id=LANGUAGE_ID](https://api.adnxs.com/language?id=LANGUAGE_ID) | To modify a language (admin only). |
| `DELETE` | [https://api.adnxs.com/language?id=LANGUAGE_ID](https://api.adnxs.com/language?id=LANGUAGE_ID) | To delete a language (admin only). |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the language. |
| `last_activity` | string | When the language was last modified. |
| `name` | string | Lanaguage name. |

## Example

### View all languages (below output is truncated)

```
curl -b cookies -c cookies "https://api.adnxs.com/language"
{
  "response": {
    "status": "OK",
    "languages": [
      {
        "id": 1,
        "name": "English",
        "last_activity": "2010-05-21 21:05:28"
      },
      {
        "id": 2,
        "name": "Chinese",
        "last_activity": "2010-05-21 21:05:28"
      },
      {
        "id": 3,
        "name": "Spanish",
        "last_activity": "2010-05-21 21:05:28"
      },
      {
        "id": 4,
        "name": "Japanese",
        "last_activity": "2010-05-21 21:05:28"
      },
      {
        "id": 5,
        "name": "French",
        "last_activity": "2010-05-21 21:05:28"
      },
. . . .
 ],
    "count": 14,
    "start_element": null,
    "num_elements": null
  }
}
```
