---
title: Digital Platform API - Category Service
description: In this article, learn about the Digital Platform API's Category service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Category service

The read-only Category Service allows you to view all buy-side categories that are registered in our system. Categories are applied to both brands and creatives - you can see what categories are assigned to a brand or creative using the [Brand Service](brand-service.md) or the [Creative Service](creative-service.md). Sellers can then allow or disallow these categories of brands and creatives using the [Ad Profile Service](ad-profile-service.md). When looking at a creative in , you will see "Sensitive categories" and "Offer category" - both of these pull from the Category Service. Sensitive categories will have the is_sensitive field set to true.

Sellers will categorize sites and placements using the [Content Category Service](content-category-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/category](https://api.appnexus.com/category) | View all categories. |
| `GET` | [https://api.appnexus.com/category?id=CATEGORY_ID](https://api.appnexus.com/category?id=CATEGORY_ID) | View a particular category. |
| `GET`  | [https://api.appnexus.com/category/meta](https://api.appnexus.com/category/meta) | Find out which fields you can filter and sort by. |

## JSON fields

> [!NOTE]
> The fields `countries_and_brands` and `countries_and_regions` defined below are being used by our system to allow gambling-related creatives to serve in the countries and regions where they're legally allowed, putting us in compliance with applicable laws.
>
> - For more information about our official gambling-related policies, see our [Part of Service Policies](../policies-regulations/index.yml) gambling policies.
> - For more information on how allowlisting works by country and region, contact [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the category. |
| `name` | string | The name of the category. |
| `is_sensitive` | bool | If `true`, the category is listed as "sensitive", and is often banned by publishers. |
| `requires_allowlist` | boolean | Whether brands or creatives in this category require allowlisting in order to serve. |
| `requires_allowlist_on_managed` | boolean | Whether brands or creatives in this category require allowlisting in order to serve on managed inventory. |
| `requires_allowlist_on_external` | boolean | Whether brands or creatives in this category require allowlisting in order to serve on external (i.e., RTB) inventory. |
| `last_modified` | timestamp | The date and time when the category was last modified. |
| `is_brand_eligible` | boolean | If true, Xandr's audit team may associate the category with brands. |
| countries_and_brands | array of objects | This array contains brand allowlist settings grouped by country/region. For more information, see [Countries and Brands](#countries-and-brands) below. |

### Countries and brands

| Field | Type | Description |
|:---|:---|:---|
| `brand_id` | int | The ID of the brand. |
| `brand_name` | string | The name of the brand. |
| `brand` | multi_object | An object containing information about the brand allowlisted in this country/region. For more information, see [Brand](#brand) below. |
| `country` | string | A 2-character string referencing the country/region in which the brand is allowlisted.|

### Brand

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand. |
| `name` | string | The name of the brand. |

## Examples

### View a single category

```
{code}
$ curl -b cookies "https://api.appnexus.com/category?id=1"
{
  "response": {
    
    "category": {
      "allowlist": {
        "countries_and_brands": [
        ],
        "countries": [
        ]
      },
      "requires_allowlist": false,
      "is_brand_eligible": true,
      "requires_allowlist_on_managed": false,
      "requires_allowlist_on_external": false,
      "last_modified": "2010-03-19 17:48:36",
      "is_sensitive": false,
      "name": "Airlines",
      "id": 1
    },
    "num_elements": null,
    "start_element": null,
    "count": 1,
    "status": "OK"
  }
}
{code}
```

### View all categories

```
{code}
$ curl -b cookies "https://api.appnexus.com/category"
{
  "response": {
    
    "categories": [
      {
        "allowlist": {
          "country or region_and_brands": [
          ],
          "country or region": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Airlines",
        "id": 1
      },
      {
        "allowlist": {
          "country or region_and_brands": [
          ],
          "country or region": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Apparel",
        "id": 2
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Appliances",
        "id": 3
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Automotive and Vehicles",
        "id": 4
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Computers and Electronics",
        "id": 5
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-06-01 20:41:02",
        "is_sensitive": true,
        "name": "Context Link Providers",
        "id": 6
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-07-01 20:23:31",
        "is_sensitive": false,
        "name": "Cosmetics and Hygiene",
        "id": 7
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-06-02 19:23:05",
        "is_sensitive": true,
        "name": "Dating",
        "id": 8
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Education",
        "id": 9
      },
      {
        "allowlist": {
          "countries_and_brands": [
          ],
          "countries": [
          ]
        },
        "requires_allowlist": false,
        "is_brand_eligible": true,
        "requires_allowlist_on_managed": false,
        "requires_allowlist_on_external": false,
        "last_modified": "2010-03-19 17:48:36",
        "is_sensitive": false,
        "name": "Employment",
        "id": 10
      },
      ...
    ],
    "num_elements": null,
    "start_element": null,
    "count": 78,
    "status": "OK"
  }
}
{code}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
