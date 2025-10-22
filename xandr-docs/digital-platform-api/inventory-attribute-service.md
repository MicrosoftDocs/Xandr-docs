---
title: Digital Platform API - Inventory Attribute Service
description: Explore the read-only Inventory Attribute service to view the inventory attributes that are registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Inventory Attribute service

Use the read-only Inventory Attribute Service to see what inventory attributes are registered in the Xandr system. These IDs are provided in the `inventory_audits` objects on the bid request.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/inventory-attribute](https://api.appnexus.com/inventory-attribute) | To view all the inventory attributes in the Xandr system. |
| `GET` | [https://api.appnexus.com/inventory-attribute?id=INVENTORY_ATTRIBUTE_ID](https://api.appnexus.com/inventory-attribute?id=INVENTORY_ATTRIBUTE_ID) | To view information about a particular inventory attribute. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the inventory attribute. |
| `name` | string (50) | Inventory attribute name. |
| `last_activity` | timestamp | When the inventory attribute was last modified. |

## Example

### View all inventory attributes (below output is subject to change)

```
curl -b cookies -c cookies "https://api.adnxs.com/inventory-attribute"
{
    "response": {
        "count": 8,
        "inventory-attributes": [
            {
                "id": 2,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Political"
            },
            {
                "id": 4,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Social media"
            },
            {
                "id": 6,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Photo & video sharing"
            },
            {
                "id": 8,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Forums (moderated)"
            },
            {
                "id": 10,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Forums (unmoderated)"
            },
            {
                "id": 12,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Incentivized clicks"
            },
            {
                "id": 14,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Non-english languages"
            },
            {
                "id": 17,
                "last_activity": "2010-10-19 19:26:08",
                "name": "Toolbars, plugins, or extensions"
            }
        ],
        "num_elements": null,
        "start_element": null,
        "status": "OK"
    }
}
```
