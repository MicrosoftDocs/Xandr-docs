---
title: Validate Inventory Item Service
description: Explore the Validate Inventory Item service to check if the app bundle IDs and/or raw URLs (domains or apps) in your lists are currently supported by the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Validate Inventory Item service

The `inventory-list/validate-inventory-item` service is used to determine whether the app bundle IDs and/or raw URLs (domains or apps) you provide in your inventory lists are currently supported by Xandr. This service will validate whether these URLs and app IDs are properly formed and supported as well as indicate whether they violate Xandr policies.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/inventory-list/validate-inventory-item](https://api.appnexus.com/inventory-list/validate-inventory-item)<br>(inventory list JSON) | Validate a list of inventory items. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `is_valid` | boolean | Indicates if the app or domain is properly formed (e.g., uses an HTTP or HTTPS protocol). If `true`, it is properly formed. |
| `is_supported` | boolean | Indicates if the app or domain is currently supported by Xandr (i.e., whether it has been audited). If `true`, it is supported. |
| `url` | string | Raw URL or app bundle ID that you provided for the item (domain or app) to be validated.<br>**Required On:** `POST` |
| `inventory_url` | string | URL of the app or domain once it has been validated. |
| `inventory_url_id` | int | The ID assigned to an inventory URL. If `inventory_url_id` has a `null` value, this means the inventory has not yet been approved. |
| `audit_status` | enum | Current audit status of the domain or app. Possible values are:<br>- `audited`: The domain or app has passed the Xandr inventory audit.<br>- `rejected`: The domain or app has failed the Xandr inventory audit (due to Xandr policy violations). |
| `app_name` | string | The name of the mobile application. If the inventory item is a domain, a `null` value appears. |
| `rejection_reason` | string | The reason why this domain or app is in violation of Xandr policies (e.g., `Violence`) if the `audit_status` field is set to `rejected`. If the `audit_status` field is not set to `rejected`, this field will be `null`. |
| `is_parent_domain` | boolean | Indicates whether the domain also includes subdomains. |

## Example

### Validate a list of inventory items

In this example, we validate a list of inventory items.

```
$cat validate-inventory-item
 
{ 
    "inventory-items": [{ 
          "url": "yahoo.com"
       },
       { 
          "url": "breitbart.com"
       }
    ]
}
 
curl -b cookies -X POST -d @validate-inventory-item "https://api.appnexus.com/inventory-list/validate-inventory-item"
 
{
  "response": {
    "status": "OK",
    "inventory-items": [
      {
        "is_valid": true,
        "is_supported": true,
        "inventory_url": "yahoo.com",
        "inventory_url_id": 640,
        "app_name": null,
        "audit_status": "audited",
        "rejection_reason": null,
        "is_parent_domain": true,
        "visits": null 
      },
      {
        "is_valid": true,
        "is_supported": true,
        "inventory_url": "breitbart.com",
        "inventory_url_id": 678,
        "app_name": null,
        "audit_status": "rejected",
        "rejection_reason": "Hate Speech",
        "is_parent_domain": false,
        "visits": null 
      }
    ]
  }
}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Inventory List Service](inventory-list-service.md)
- [Inventory List Item Service](inventory-list-item-service.md)
- [Line Item Service](line-item-service.md)
- [Insertion Order Service](insertion-order-service.md)
