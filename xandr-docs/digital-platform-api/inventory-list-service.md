---
title: Inventory List Service
description: Explore the Inventory List service, designed for creating lists of inventory that include the domains and apps you intend to target.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Inventory List service

The Inventory List Service is used to create inventory lists that contain the domains and apps you wish to target. These inventory lists can then be associated with line items for targeting. Use the Inventory List Service to create, view, and update inventory lists. You can then add domains and apps (or app bundle IDs) to the inventory list via the [Inventory List Item Service](inventory-list-item-service.md).

## REST API

> [!NOTE]
> To edit an inventory list in the API based on the ID of the inventory list in the UI, you must first obtain the `id` of the list via the API using the following `GET` call:
>
> ```
> GET https://api.appnexus.com/inventory-list?inventory_url_list_id=[CONSOLE_UI_LIST_ID]
> ```
>
> Use the value of the `id` field returned for all subsequent API calls to edit the desired inventory list.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/inventory-list](https://api.appnexus.com/inventory-list) | View all inventory lists. |
| `GET` | [https://api.appnexus.com/inventory-list?search=SEARCH_TERM](https://api.appnexus.com/inventory-list?search=SEARCH_TERM) | Search for inventory lists with domains or apps containing certain characters. |
| `POST` | [https://api.appnexus.com/inventory-list](https://api.appnexus.com/inventory-list) | Add a new inventory list. |
| `PUT` | [https://api.appnexus.com/inventory-list/%5BINVENTORY_LIST_ID%5D](https://api.appnexus.com/inventory-list/%5BINVENTORY_LIST_ID%5D) | Update an inventory list. |
| `DELETE` | [https://api.appnexus.com/inventory-list?id=INVENTORY_LIST_ID](https://api.appnexus.com/inventory-list?id=INVENTORY_LIST_ID) | Delete an inventory list. |

> [!NOTE]
> **Helpful Query String Filters:**
>
> For general information on query string filters available to most services, see [API Semantics](api-semantics.md) (e.g., `num_elements`,
> `start elements`, `search`, `sort`). The `has_apps` and `has_domains` query string filters are unique to `inventory-list` service.
>
> | HTTP Method | Endpoint | Description |
> |:---|:---|:---|
> | `GET` | [https://api.appnexus.com/inventory-list?has_apps=true&has_domains=true](https://api.appnexus.com/inventory-list?has_apps=true&has_domains=true) | Returns all lists that contains apps and domains. |
> | `GET` | [https://api.appnexus.com/inventory-list?has_apps=false&has_domains=true](https://api.appnexus.com/inventory-list?has_apps=false&has_domains=true) | Returns all lists that contain only domains. |
> | `GET` | [https://api.appnexus.com/inventory-list?has_apps=true&has_domains=false](https://api.appnexus.com/inventory-list?has_apps=true&has_domains=false) | Returns all lists that contain only apps. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the specific advertiser this inventory list is associated with.<br>If `null`, the inventory list is available to all of the member's advertisers.<br>**Default:** `null`. |
| `created_on` | string | Timestamp when inventory list was created. |
| `description` | string | Description of the inventory list. |
| `id` | int | ID of the inventory list (auto-generated on `POST`).<br>**Read Only.**<br>**Required On:** `PUT` |
| `name` | string | **Required On:** `POST`<br>Name of the inventory list. |
| `insertion_order_id` | int | The ID of the insertion order under which the inventory list was created. |
| `inventory_list_type` | enum | **Required On:** `POST`<br><br>**Note:** Going forward, "allowlist" and "blocklist" terminology will be followed for our APIs. This is a part of an ongoing effort to evaluate our current terminology usage and usher in more inclusive terminology for Xandr platforms.<br>Type of inventory list. Possible values:<br> - `allowlist`<br> - `blocklist`<br><br>**Note:** The value of this field cannot be edited on `PUT` calls. |
| `inventory_url_list_id` | int | ID of the inventory list as it appears in the UI. |
| `last_modified` | string | Timestamp when inventory list was last updated. |
| `line_item_id` | int | The ID of the line item using this list for domain/app targeting. |
| `num_apps` | int | Total number of apps in the inventory list.<br>**Read Only.** |
| `num_domains` | int | Total number of domain in the inventory list.<br>**Read Only.** |
| `required_for_all` | Boolean | If `true`, the inventory list will be applied to all line items under the advertiser (see `advertiser_id`).<br>**Default:** `false`. |

## Examples

### Create an inventory list

In this example, we create a new inventory list.

```
$ cat inventory-list-create
 
{
    "inventory-list": {
        "name": "XYZ Allowlist",
        "description": "A list of domains that Company XYZ wants to target",
        "inventory_list_type": "allowlist"
    }
}
 
$ curl -b cookies -X POST -d @inventory-list-create 'https://api.appnexus.com/inventory-list'
 
{
    "response": {
        "status": "OK",
        "inventory-list": {
           "id": 3901,
           "name": "XYZ Allowlist"
           ....
         }
    }
}
```

### Update an inventory list

In this example, we update an inventory list.

```
$ cat inventory-list-update
 
{
    "inventory-list": {
        "description": "Updated Description"
    }
}
 
$ curl -b cookies -X PUT -d @inventory-list-update 'https://api.appnexus.com/inventory-list/3901'
 
{
    "response": {
        "status": "OK",
        "inventory-list": {
           "id": 3901,
           "name": "XYZ Allowlist"
           "description": "Updated Description",
           ....
         }
    }
}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Inventory List Item Service](inventory-list-item-service.md)
- [Validate Inventory Item Service](validate-inventory-item-service.md)
- [Line Item Service](line-item-service.md)
- [Insertion Order Service](insertion-order-service.md)
