---
title: Bidder - Inventory Attribute Service
description: Use the Inventory Attribute Service to view the inventory attributes that are registered in the system. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder - Inventory attribute service

Use the read-only Inventory Attribute Service to see what inventory attributes are registered in the Xandr system. These IDs are provided in the `inventory_audits` objects on the bid request.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.adnxs.com/inventory-attribute` | To view all the inventory attributes in the Xandr system |
| `GET` | `https://api.adnxs.com/inventory-attribute/INVENTORY_ATTRIBUTE_ID` | To view information about a particular inventory attribute |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the inventory attribute. |
| `last_activity` | string | When the inventory attribute was last modified. |
| `name` | string | Inventory attribute name. |

## Example

### View all inventory attributes (below output is subject to change)

```
curl -b cookies -c cookies "https://api.adnxs.com/inventory-attribute"
{
  "response": {
    "status": "OK",
    "count": 10,
    "start_element": null,
    "num_elements": null,
    "inventory_attributes": [
      {
        "id": 2,
        "name": "Political",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 4,
        "name": "Social media",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 6,
        "name": "Photo & video sharing",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 8,
        "name": "Forums (moderated)",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 10,
        "name": "Forums (unmoderated)",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 12,
        "name": "Incentivized clicks",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 14,
        "name": "Non-english languages",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 16,
        "name": "Streaming media",
        "last_activity": "2010-10-19 19:26:08"
      },
      {
        "id": 17,
        "name": "Toolbars, plugins, or extensions",
        "last_activity": "2012-12-04 21:00:58"
      },
      {
        "id": 29,
        "name": "Contextual Nudity",
        "last_activity": "2014-04-22 19:11:56"
      }
    ]
  }
}
```
