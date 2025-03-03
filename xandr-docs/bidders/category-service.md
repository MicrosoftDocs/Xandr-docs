---
title: Bidders - Category Service
description: In this article, learn about bidders category service, their JSON fields, REST API, along with a detailed set of examples.
ms.date: 10/28/2023
---

# Bidders - Category service

The read-only Category Service allows you to view all categories that are registered in the Xandr system. Categories are assigned to both brands and creatives - you can see what categories are assigned using the [Brand Service](brand-service.md) or the [Creative Service](creative-service.md). You can then allow or disallow these categories of brands and creatives using the [Ad Profile Service](ad-profile-service.md).

> [!NOTE]
> For site and placement categories, use the [Content Category Service](content-category-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET`  | [https://api.adnxs.com/category](https://api.adnxs.com/category) | View all the categories in the Xandr system. |
| `GET`  | [https://api.adnxs.com/category/CATEGORY_ID](https://api.adnxs.com/category/CATEGORY_ID) | View information about a particular category. |

## JSON fields

> [!NOTE]
> The fields `countries_and_brands` and `countries_and_regions` defined below are being used by our system to allow gambling-related creatives to serve in the countries and regions where they're legally allowed, putting us in compliance with applicable laws.
>
> - For more information about our official gambling-related policies, see our buy-side and sell-side gambling policies.
> - For more information on how allowlisting works by country and region, contact [Customer Support](https://support.ads.microsoft.com).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the category.<br>**Required On:** `PUT`, in query string |
| `name` | string | The name of the category.<br>**Required On:** `POST` |
| `is_sensitive` | boolean | If `true`, the category is listed as "sensitive", and is often banned by publishers.<br>**Default:** `false` |
| `last_modified` | timestamp | The date and time when the category was last modified. |
| `requires_allowlist_on_external` | boolean | Whether brands or creatives in this category require allowlisting in order to serve on external (i.e. RTB) inventory.<br>**Default:** `false` |
| `requires_allowlist_on_managed` | boolean | Whether brands or creatives in this category require allowlisting in order to serve on managed inventory.<br>**Default:** `false` |
| `is_brand_eligible` | boolean | If `true`, then the category is eligible to be associated with brands within the audit process.<br>**Default:** `true` |
| `requires_allowlist` | boolean | Whether brands or creatives in this category require allowlisting in order to serve.<br>**Default:** `false` |
| `countries_and_brands` | array of objects | This array contains brand allowlist settings grouped by country or region. For more information, see "[Countries and Brands](#countries-and-brands)" below. |

### Countries and brands

| Field | Type | Description |
|:---|:---|:---|
| `brand_id` | int | The ID of the brand. |
| `brand_name` | string | The name of the brand. |
| `brand` | multi_object | An object containing information about the brand allowlisted in this country or region. For more information, see "[Brand](#regions-and-brands)" below. |
| `country` | string | A 2-character string referencing the country or region in which the brand is allowlisted. For a list of supported codes, refer the ISO 3166-1 country codes. |

### Regions and brands

| Field | Type | Description |
|:---|:---|:---|
| `brand_id` | int | The ID of the brand. |
| `brand_name` | string | The name of the brand. |
| `brand` | multi_object | An object containing information about the brand allowlisted in this region. |
| `region` | string | A string referencing the region in which the brand is allowlisted. For a list of supported codes, see the [ISO 3166-2](https://www.maxmind.com/download/geoip/misc/region_codes.csv). |

## Examples

### View all categories

```
$ curl -b cookies -c cookies "https://api.adnxs.com/category"
{
  "response": {
    "status": "OK",
    "count": 88,
    "start_element": null,
    "num_elements": null,
    "categories": [
      {
        "id": 1,
        "name": "Airlines",
        "is_sensitive": false,
        "last_modified": "2010-03-19 17:48:36",
        "requires_allowlist_on_external": false,
        "requires_allowlist_on_managed": false,
        "is_brand_eligible": true,
        "requires_allowlist": false,
        "allowlist": {
          "countries_and_brands": [],
          "regions_and_brands": []
        }
      },
      {
        "id": 2,
        "name": "Apparel",
        "is_sensitive": false,
        "last_modified": "2010-03-19 17:48:36",
        "requires_allowlist_on_external": false,
        "requires_allowlist_on_managed": false,
        "is_brand_eligible": true,
        "requires_allowlist": false,
        "allowlist": {
          "countries_and_brands": [],
          "regions_and_brands": []
        }
      },
      {
        "id": 3,
        "name": "Appliances",
        "is_sensitive": false,
        "last_modified": "2010-03-19 17:48:36",
        "requires_allowlist_on_external": false,
        "requires_allowlist_on_managed": false,
        "is_brand_eligible": true,
        "requires_allowlist": false,
        "allowlist": {
          "countries_and_brands": [],
          "regions_and_brands": []
        }
      },
      "dbg": {
      ...
    }
  }
}
```

### View a specific category

```
$ curl -b cookies -c cookies "https://api.adnxs.com/category/1"
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "category": {
      "id": 1,
      "name": "Airlines",
      "is_sensitive": false,
      "last_modified": "2010-03-19 17:48:36",
      "requires_allowlist_on_external": false,
      "requires_allowlist_on_managed": false,
      "is_brand_eligible": true,
      "requires_allowlist": false,
      "allowlist": {
        "countries_and_brands": [],
        "regions_and_brands": []
      }
    },
    "dbg": {
      ...
    }
  }
}
```
