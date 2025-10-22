---
title: Digital Platform API - Content Category Service
description: In this article, learn about the Digital Platform API's Content Category service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Content Category service

Xandr provides a set of "universal" categories, which are commonly used categories that members can apply to their sites (placement groups) and placements for later targeting or informational purposes. You can also create your own custom categories by using this service.

You apply content categories to sites and placements through the [Site Service](site-service.md) and [Placement Service](placement-service.md) using the content category ID, retrieved from this service. Content categories can then be used for site and placement targeting for direct campaigns through the [Profile Service](profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/content-category?type=standard](https://api.appnexus.com/content-category?type=standard) | View all standard custom content categories belonging to your member. |
| `GET` | [https://api.appnexus.com/content-category?category_type=universal&id=CONTENT_CATEGORY_ID](https://api.appnexus.com/content-category?category_type=universal&id=CONTENT_CATEGORY_ID) | View a specific custom content category. |
| `GET` | [https://api.appnexus.com/content-category?id=1,2,3](https://api.appnexus.com/content-category?id=1,2,3) | View multiple content categories by ID using a comma-separated list. |
| `POST` | [https://api.appnexus.com/content-category](https://api.appnexus.com/content-category) | Add a custom content category. |
| `PUT` | [https://api.appnexus.com/content-category?id=CONTENT_CATEGORY_ID](https://api.appnexus.com/content-category?id=CONTENT_CATEGORY_ID) | Modify a custom content category. |
| `DELETE` | [https://api.appnexus.com/content-category?id=CONTENT_CATEGORY_ID](https://api.appnexus.com/content-category?id=CONTENT_CATEGORY_ID) | Delete a custom content category.<br><br>**Tip:** You cannot add, modify, or delete universal content categories (where `is_system` is set to `true`). Universal content categories are managed by Xandr. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `code` | string | Used only for deals. |
| `description` | string (255) | The description of the content category |
| `id` | int | The ID of the category.<br>**Required On:** `PUT`<br>**Default:** Auto-generated number. |
| `is_system` | boolean | **Read Only.** If `true`, this is a "universal" content category created by Xandr. You can apply universal content categories to your sites and placements, but you cannot edit them. |
| `last_modified` | timestamp | **Read Only.** The date and time that this content category was last modified. |
| `member_id` | int | **Read Only.** Your member ID. |
| `name` | string (100) | The name of the category.<br>**Required On:** `POST` |
| `parent_category` | object | If the category is the child of a parent category, the ID and name of the parent is listed in a [format](#parent_category-format). |
| `type` | enum | The type of content category. Possible values are `"standard"`, `"deal"`, or `"deal_priority"`. |

### `parent_category` format

```
"parent_category": {
"id": 10,
"name": "Games"
}
```

## Examples

### View all custom content categories belonging to your member

```
$ curl -b cookies 'https://api.appnexus.com/content-category'
{
   "response":{
      "status":"OK",
      "content-categories":[
         {
            "id":9999,
            "name":"Animals",
            "description":null,
            "is_system":false,
            "type":"standard",
            "code": null,
            "last_modified":"2010-05-12 22:46:42"
         },
         {
            "id":8888,
            "name":"Arts & Humanities",
            "description":null,
            "is_system":false,
            "type":"standard",
            "code": null,
            "last_modified":"2010-05-12 22:46:42"
         },
         ...
         {
            "id":7777,
            "name":"Travel",
            "description":null,
            "is_system":false,
            "type":"standard",
            "code": null,
            "last_modified":"2010-05-12 22:46:42"
         }
      ]
   }
}
```

### View all universal content categories

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/content-category?is_system=true'
{
    "response": {
        "status": "OK",
        "content-categories": [
            {
              "id": 1,
              "name": "Music",
              "description": null,
              "is_system": true,
              "parent_category": null,
              "type": "standard",
              "code": null,
              "last_modified": "2010-03-04 18:18:52"
            },
            
            {
              "id": 2,
              "name": "Pets & Animals",
              "description": null,
              "is_system": true,
              "parent_category": null,
              "type": "standard",
              "code": null,
              "last_modified": "2010-10-24 02:43:16"
            },
            {
              "id": 3,
              "name": "Fun & Trivia",
              "description": null,
              "is_system": true,
              "parent_category": {
                "id": "10",
                "name": "Arts & Entertainment"
              },
              "type": "standard",
              "code": null,
              "last_modified": "2010-10-24 02:43:16"
            },
            {
              "id": 4,
              "name": "Autos & Vehicles",
              "description": null,
              "is_system": true,
              "parent_category": null,
              "type": "standard",
              "code": null,
              "last_modified": "2010-10-24 02:43:16"
            },
            ...
        ],
        "count": 34,
        "start_element": null,
        "num_elements": null
    }
}
```

### View a specific custom content category

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/content-category?category_type=universal&id=11111'
{
    "response": {
        "status": "OK",
        "content-category": {
            "id": 11111,
            "name": "A fine and private placement",
            "description": null,
            "is_system": false,
            "parent_category": null,
            "type": "standard",
            "code": null,
            "last_modified": "2012-08-29 15:42:01"
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### View a specific universal content category

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/content-category?is_system=true&id=2222'
{
    "response": {
        "status": "OK",
        "content-category": {
            "id": 2222,
            "name": "Small Business",
            "description": null,
            "is_system": true,
            "type": "standard",
            "code": null,
            "parent_category": {
                "id": "8"
            },
            "last_modified": "2010-10-24 02:43:16"
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
}
```
