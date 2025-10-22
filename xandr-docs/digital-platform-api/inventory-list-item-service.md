---
title: Inventory List Item Service
description: Learn about the Inventory List Item service that lets you add app bundle IDs and raw URLs (domain or app) to an existing inventory list.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Inventory List Item service

The Inventory List Item Service lets you add app bundle IDs and raw URLs (domain or app) to an existing inventory list. For example:

- app bundle IDs:
  - *617263396*
  - *com.magmamobile.game.Elements*
- raw URL (domain): *[yahoo.com](https://yahoo.com/)*
- raw URL (app): *[https://itunes.apple.com/us/app/funny-pics-lol!-daily-laughs/id617263396](https://itunes.apple.com/us/app/funny-pics-lol!-daily-laughs/id617263396)*

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item](https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item) | View all items (domains/apps) in a specific inventory list. |
| `GET` | [https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item?search=SEARCH_TERM](https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item?search=SEARCH_TERM) | Search for domains or apps containing certain characters. |
| `POST` | [https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item](https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item) | Add new domains/apps to an inventory list.<br><br>**Note:** 1000 items (domains/apps) is the maximum number of items you can add to an inventory list for each `POST` request. |
| `PUT` | [https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item/%5BINVENTORY_LIST_ITEM_ID%5D](https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item/%5BINVENTORY_LIST_ITEM_ID%5D) | Update an inventory list item.<br><br>**Note:** The `include_children` field is the only field in an inventory list item that you can update with a `PUT` request. |
| `DELETE` | [https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item?id=1,2,3](https://api.appnexus.com/inventory-list/%5BLIST_ID%5D/item?id=1,2,3) | Delete items (domains/apps) from an inventory list. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `app_name` | string | Name of the app item (`null` if a domain). |
| `audit_status` | enum | Current status of the domain or app. Possible values are:<br> - `audited`: The domain or app has passed the Xandr inventory audit.<br>- `rejected`: The domain or app has failed the Xandr inventory audit (due to Xandr policy violations).<br> - `unaudited`: The domain or app was not audited.<br> - `unauditable`: The domain or app was not audited.<br>- `pending`: The domain or app was not audited (default value).<br> - `masked`: The actual URL of the domain or app was not exposed by the seller for targeting or reporting, but was still audited and passed the Xandr inventory audit.<br> - `is_adserver`: The domain or app was not audited and was detected as an ad server domain. |
| `id` | int | ID associated with the app or domain you are adding. Auto-generated on `POST`.<br>**Read Only.**<br>**Required On:** `PUT` |
| `is_supported` | boolean | Indicates whether the app or domain is currently supported by Xandr (e.g., whether it has been audited). If `true`, it is supported. |
| `inventory_url` | string | URL of the app or domain once it has been validated. For details on how validation is performed, see [Validate Inventory Item service](validate-inventory-item-service.md). |
| `include_children` | boolean | Indicates whether subdomains and subpaths of the parent domain should be included. If `true`, subdomains will be included. |
| `rejection_reason` | string | The reason why this domain or app is in violation of Xandr policy (e.g., `Violence`, `Hate Speech`) if the `audit_status` field is set to `rejected`. If the `audit_status` field is not set to `rejected`, this field will be `null`. |
| `url` | string | **Required On:** `POST`<br>Raw URL or app bundle ID that you provide for the item (domain or app) to be added. |

## Examples

### Add domains and apps (items) to an inventory list

In this example, we add domains and apps (items) to an inventory list.

```
$ cat inventory-list-item
 
{
    "inventory-list-items": [
        {
            "url": "bad-domain.com",
            "include_children": false
        }, 
        {
            "url": "app_id"
        }, 
        ...
    ]
}
 
curl -b cookies -X POST -d @inventory-list-item "https://api.appnexus.com/inventory-list/3452/item"
 
{ 
    "response": { 
        "status": "OK",
        "inventory-list-items": [
            {
                "audit_status": "rejected",
                "inventory_url": "bad-domain.com",
                "include_children": false,
                "is_supported": true, 
                "rejection_reason": "Violence"
            }, 
            {
                "audit_status": "audited",
                "inventory_url": "app_url.com",
                "include_children": false,
                "is_supported": true, 
                "rejection_reason": null
            }, 
            ...
        ]
    }
}
```

### View all domains/apps (items) in a specific inventory list

In this example, we view domains and apps (items) in an inventory list.

```
$ curl -b cookies -X GET "https://api.appnexus.com/inventory-list/3452/item" 

{ 
    "response": { 
        "status": "OK",
        "inventory-list-items": [
            {
                "id": 1, 
                "audit_status": "rejected",
                "app_name": null, 
                "inventory_url": "bad-domain.com",
                "include_children": false,
                "is_supported": true, 
                "rejection_reason": "Violence"
            }, 
            {
                "id": 2, 
                "audit_status": "audited",
                "app_name": "Name of the app", 
                "inventory_url": "app_url.com",
                "include_children": false,
                "is_supported": true, 
                "rejection_reason": null
            }, 
            ...
        ]
    }
}
```

### Update an inventory list item in an inventory list

In this example, we update an inventory list item in an inventory list.

```
$ cat inventory-list-item

{
    "inventory-list-item": {
        "include_children": true
    }
}

curl -b cookies -X PUT -d @nventory-list-item 'https://api.appnexus.com/inventory-list/3452/item/2'

{
    "response": {
        "inventory-list-item": {
            "id": 2,
            "include_children": true,
            "audit_status": "audited",
            "app_name": "Name of the app",
            "inventory_url": "app_url.com"
        },
        "status": "OK",
        "num_elements": 1,
        "start_element": 0,
        "count": 1
    }
}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Inventory List Service](inventory-list-service.md)
- [Validate Inventory Item Service](validate-inventory-item-service.md)
- [Line Item Service](line-item-service.md)
- [Insertion Order Service](insertion-order-service.md)
