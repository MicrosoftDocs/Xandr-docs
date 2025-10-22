---
title: Bidders - Content Category Service
description: This page tells us what content categories are registered in the Xandr system. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Bidders - Content category service

Use the read-only Content Category Service to see what content categories are registered in the Xandr system. These IDs are provided in the inventory_audits objects on the bid request.

Content categories are arranged in a two-level hierarchy. There are top-level categories and child categories. The child categories have a parent_category_id pointing to their parent. The top-level categories have a null parent_category_id.

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| GET | [https://api.adnxs.com/content-category](https://api.adnxs.com/content-category) | To view all the content categories in the Xandr system. |
| GET | [https://api.adnxs.com/content-category/CONTENT_CATEGORY_ID](https://api.adnxs.com/content-category/CONTENT_CATEGORY_ID) | To view information about a particular content category. |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `description` | string | The description of the content category. |
| `id` | int | The ID of the content category. |
| `is_system` | bool | If true, the content category is defined by Xandr. |
| `last_modified` | timestamp | The date and time that this content category was last modified. |
| `name` | string | The name of the content category. |
| `parent_category` | object | If the category is the child of a parent category, the ID and name of the parent is listed here in the following format: <br>`"parent_category": { "id":10, "name": "Games" }` |

## Example

**View all content categories (below output is truncated)**

``` 
curl -b cookies -c cookies "https://api.adnxs.com/content-category"
{
    "response": {
        "status": "OK",
        "count": 325,
        "start_element": null,
        "num_elements": null,
        "content_categories": [
            {
                "id": 4,
                "name": "Pets & Animals",
                "description": null,
                "is_system": true,
                "last_modified": "2010-10-24 02:43:16",
                "parent_category": null
            },
            {
                "id": 5,
                "name": "Fun & Trivia",
                "description": null,
                "is_system": true,
                "last_modified": "2010-10-24 02:43:16",
                "parent_category": {
                    "id": 10,
                    "name": "Arts & Entertainment"
                }
            },
            {
                "id": 6,
                "name": "Autos & Vehicles",
                "description": null,
                "is_system": true,
                "last_modified": "2010-10-24 02:43:16",
                "parent_category": null
            },
            {
                "id": 7,
                "name": "Beauty & Personal Care",
                "description": null,
                "is_system": true,
                "last_modified": "2010-03-04 19:14:12",
                "parent_category": null
            },
            [...]
        ],
        "count": 326,
        "num_elements": 5,
        "start_element": 1,
        "status": "OK"
    }
}              
```
