---
title: Offline Attribution Product Group Service
description: The Offline Attribution Product Group service helps track offline sales performance against specific products and their categories, brands, or product lines.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Offline Attribution Product Group service

The Offline Attribution Product Group Service is used to discover and locate product group information (IDs) from the Xandr product catalog. If your line item has Offline Attribution enabled, this catalog is used to track your line item's offline sales performance against a product category, brand product, product line, or specific product.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` |  `https://api.appnexus.com/offline-attribution-product-group` | View all product groups. |
| `GET` |  `https://api.appnexus.com/offline-attribution-product-group?search=STRING` | Search for a product group by `string`. |

## JSON Fields

### General

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID for a certain product group. |
| `offline_attribution_provider_member_id` | int | The ID of the entity providing information for the offline attribution catalog. |
| `provider_member_name` | string | The name of the entity providing information for the offline attribution catalog. |
| `vendor_product_code` | string | The vendor-provided code for the product to report on. |
| `offline_attribution_category_id` | int | The respective ID of an offline attribution category. This ID is returned to the user in their service responses. |
| `category_name` | string | The name used for a certain product category (**example**: SOFT DRINKS).<br>Category names are used to search for a product group's ID. |
| `brand_name` | string | The name used for a certain brand (**example**: COCA-COLA COMPANY). |
| `product_high_name` | string | The name of a specific product line (**example**: COCA-COLA). |
| `product_low_name` | string | The name of a specific product name (**example**: DIET COKE). |

## Examples

### ID request for an offline attribution product group

#### Request

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/offline-attribution-product-group'
```

#### Response

```
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "offline-attribution-product-groups": [
            {
                "id": 3449,
                "offline_attribution_provider_member_id": 12515,
                "provider_member_name": "NCS",
                "vendor_product_code": "2968042",
                "offline_attribution_category_id": 3446,
                "category_name": "ADULT INCONTINENCE",
                "offline_attribution_brand_id": 3430,
                "brand_name": "BUTTERFLY HEALTH, INC.",
                "offline_attribution_product_high_id": 3421,
                "product_high_name": "BUTTERFLY",
                "offline_attribution_product_low_id": null,
                "product_low_name": "null",
                "last_modified": "2021-02-22 18:04:45",
                "created_on": "2020-02-22 18:04:45",
                "deleted": 0
            }
        ],
        "count": 1,
        "dbg_info": {
            "warnings": [],
            "version": "local",
            "output_term": "offline-attribution-product-groups"
        }
    }
}
```

### Search query with response

#### Request

```
// The search term needs to be URL-encoded:
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/offline-attribution-product-group?search=BRICK%20RIVER%20CIDER%20CO'
```

#### Response

```
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "offline-attribution-product-groups": [
            {
                "id": 3496,
                "offline_attribution_provider_member_id": 12515,
                "provider_member_name": "NCS",
                "vendor_product_code": "5559739",
                "offline_attribution_category_id": 3506,
                "category_name": "ALCOHOLIC CIDER",
                "offline_attribution_brand_id": 3499,
                "brand_name": "BRICK RIVER CIDER CO",
                "offline_attribution_product_high_id": 3486,
                "product_high_name": "BRICK RIVER CIDER CO",
                "offline_attribution_product_low_id": null,
                "product_low_name": "null",
                "last_modified": "2021-02-22 18:05:09",
                "created_on": "2021-02-22 18:05:09",
                "deleted": 0
            }
        ],
        "count": 1,
        "dbg_info": {
            "warnings": [],
            "version": "local",
            "output_term": "offline-attribution-product-groups"
        }
    }
    }
```

## Related topics

- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
- [Line Item (ALI) Service](./line-item-service---ali.md)
- [Insertion Order Service](./insertion-order-service.md)
