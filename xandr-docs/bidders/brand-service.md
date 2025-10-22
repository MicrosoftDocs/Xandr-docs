---
title: Bidders - Brand Service
description: In this article, learn about bidders brand service, their JSON fields, and REST API with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Brand service

Use the read-only Brand Service to see what brands are registered in the Xandr system. You can also use the Brand Service to obtain the ID assigned to a certain brand. This ID is used as an optional input for the [Creative Service](creative-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/brand](https://api.adnxs.com/brand) | To view all the brands in the Xandr system. |
| `GET` | [https://api.adnxs.com/brand?search=BRAND_NAME](https://api.adnxs.com/brand?search=BRAND_NAME) | To view all brands with names containing certain characters. |
| `GET` | [https://api.adnxs.com/brand?url_search=BRAND_URL](https://api.adnxs.com/brand?url_search=BRAND_URL) | To view all brands with URLS starting with certain characters. |
| `GET` | [https://api.adnxs.com/brand/BRAND_ID](https://api.adnxs.com/brand/BRAND_ID) | To view a specific brand. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `category_id` | int | The ID of the category associated with this brand - see [Category Service](category-service.md). |
| `company_id` | int | This field is not currently used. |
| `id` | int | The ID of the brand. |
| `is_premium` | bool | This field is not currently used. |
| `last_activity` | string | When the brand was last modified. |
| `name` | string | Brand name. |
| `num_creatives` | int | Number of active, serveable creatives with this brand that are registered with Xandr. |
| `url` | string | URL for this brand. This field has been deprecated in favor or the urls field (below). |
| `urls` | string array | URLs associated with this brand. |

## Example

### View all brands (below output is truncated)

```
curl -b cookies -c cookies "https://api.adnxs.com/brand"
{
   "response":{
      "status":"OK",
      "brands":[
         {
            "last_activity" : "2009-01-02 19:53:15",
            "urls" : ["weightwatchers.com"],
            "name" : "Weight Watchers",
            "id" : 154,
            "num_creatives" : 10,
            "category_id" : 14
         },
         {
            "last_activity" : "2009-01-02 19:53:16",
            "urls" : ["yahoo.com"],
            "name" : "Yahoo",
            "id" : 15,
            "num_creatives" : 50,
            "category_id" : 15
         },
         ....
      ]
   }
}
```
