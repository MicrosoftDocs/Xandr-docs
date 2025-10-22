---
title: Curated Deal Ad Quality API Setup Guide
description: Learn the process of creating and configuring a curated deal ad quality through the API
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Curated deal ad quality API setup guide

Curated deals offer a range of ad quality settings, granting control over what demand can serve through a curated deal. The updated suite of ad quality settings for curators provide robust controls at both the deal and member levels. Configured uniquely, these updated ad quality settings are currently accessible solely through the API. This guide explains how you can start using them.

## Overview

The ad quality settings are specified within a dedicated object known as an ad profile. This ad profile is subsequently linked with either a curated deal or your curator member.

The primary benefits of utilizing ad profiles with curated deals include:

- These settings can be configured to permit or restrict attributes such as brands, brand categories, creative ad servers, landing pages, and languages at either the curator deal or curator member level. Unlike legacy ad quality settings, which could only be configured to allow brands.
- Curators can easily discern which ad quality controls were employed for a specific deal.
>[!NOTE]
>Ad quality controls are implemented in an auction either at the member-level or deal-level, but not through a combination of both. Refer the table below for more details.
- Curators can assess the potential revenue impact of their ad quality controls.
- They offer the ability to allow or block creative ad servers, granting curators control over which creative pixels can serve through their deals.

| Auction | Curator member's ad profile | Curator deal's ad profile | Ad profile used to evaluate bids against curated deals |
|:---|:---|:---|:---|
| A | 123 | | 123 |
| B | | 456 | 456 |
| C | 123 | 456 | 456 |

>[!NOTE]
> - In an auction, only one ad profile will be utilized and an ad profile associated with your deal supersedes an ad profile associated with your member.
> - In auction C, the platform does not combine ad profiles 123 and 456. Instead, only ad profile 456 is utilized to assess eligible bids against the deal.

## REST API

| API Endpoint | API Object | Detailed Reference |
|:---|:---|:---|
| https://api.appnexus.com/auth | auth | [Authentication Service](./authentication-service.md) |
| https://api.appnexus.com/ad-profile | ad-profile | [Ad Profile Service](./ad-profile-service.md) |
| https://api.appnexus.com/deal | deal | [Deal Service](./deal-service.md) |


## Prerequisites

Before beginning this setup, familialize yourself with the foundational concepts outlined in the following pages. These concepts are essential prerequisites before delving into Curated Deal Ad Quality Settings.
- [API Getting Started](./api-getting-started.md) - It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices.
- [Curated Deal Line Item API Setup Guide](./curated-deal-line-item-api-setup-guide.md) - It explains the steps to create a curated deal line item and its associated deal object.

## Best practices

- You can utilize both legacy ad quality settings and new ad quality settings concurrently on the same deal. Nevertheless, for streamlined maintenance and troubleshooting purposes, we advise exclusively employing the updated ad quality settings.
- Utilize the Curator Bid Error report to monitor errors caused by ad quality settings and determine if they unintentionally block demand.
- The ad quality settings are defined on an ad profile object inked to a deal. You can reuse the same ad profile across multiple deals, simplifying the maintenance of your ad quality settings overall.
- If you're utilizing an ad profile for your curator member and need to create an exception for a buyer, you can assign an ad profile to their curated deal. This action will fully substitute your curator member's ad profile in the auction for this deal, ensure you retain any member-level ad quality settings you wish to preserve on your curated deal.    

## Setup procedure

1. Authenticate
   See the [Authentication Service](./authentication-service.md) for steps to authenticate.
1. Create an ad profile
   Use the [Ad Profile Service](./ad-profile-service.md) to create a new ad profile. When using ad profiles with curated deals or curator members the following fields are supported:
    ### JSON fields
    | Field | Type | Description |
    |:---|:---|:---|
    | `id` | int | The Xandr ID assigned by the API to reference this ad_profile.<br> **Required On:** PUT, in  query string. |
    | `description` | string | An optional description to reference this ad_profile |
    | `default_brand_status` | enum | The brand status to be used by default when no explicit selection is made. Possible values: <br> - trusted <br> - banned |
    | `default_category_status` | enum | The brand category status to be used by default when no explicit selection is made. Possible values: <br> - trusted <br> - banned |
    | `default_language_status` | enum | The language status to be used by default when no explicit selection is made. Possible values: <br> - trusted <br> - banned |
    | `default_ad_server_status` | enum | The creative ad server status to be used by default when no explicit selection is made. Possible values: <br> - trusted <br> - banned |
    | `brands` | array of objects | Array of brands with their status. See Brands below for more details. |
    | `categories` | array of objects | Array of brand categories with their status. See Brand Categories below for more details. |
    | `languages` | array of objects | Array of languages with their status. See Languages below for more details. |
    | `ad_servers` | array of objects | Array of creative ad servers with their status. See Creative Ad Servers below for more details. |
    
    ### Brands
    | Field | Type | Description |
    |:---|:---|:---|
    | `id` | int | The ID of the brand. You can use the [Brand Service](./brand-service.md) to retrieve brand IDs. |
    | `status` | enum | Whether creatives of this brand can or cannot serve through the curated deal or curator member associated with this ad profile. Possible values: <br> - trusted <br> - banned |

    ### Brand category
    | Field | Type | Description |
    |:---|:---|:---|
    | `id` | int | The ID of the brand category. You can use the [Category Service](./category-service.md) to retrieve category IDs. |
    | `status` | enum | Whether creatives of this brand category can or cannot serve through the curated deal or curator member associated with this ad profile. Possible values: <br> - trusted <br> - banned |

    ### Language
    | Field | Type | Description |
    |:---|:---|:---|
    | `id` | int | The ID of the language. You can use the [Language Service](./language-service.md) to retrieve language IDs. |
    | `status` | enum | Determines if the creatives with this language can or cannot serve through the curated deal or curator member associated with this ad profile. Possible values: <br> - trusted <br> - banned |

    ### Creative ad servers
    | Field | Type | Description |
    |:---|:---|:---|
    | `id` | int | The ID of the creative ad server. You can use the [Ad Server Service](./ad-server-service.md) to retrieve ad server IDs. |
    | `status` | enum | Determines if the creatives with this creative ad server can or cannot serve through the curated deal or curator member associated with this ad profile. Possible values: <br> - trusted <br> - banned |

1. Associate the ad profile with a curated deal or curator member
   **To associate the ad profile with a curated deal:**
    ```
    $ cat deal.json
    {
        “deal”: {
        “ad_profile_id”: 123456
                }
    }
    $ curl -b cookies -c cookies -X PUT -d ‘@deal.json’ ‘https://api.appnexus.com/deal?id=987654’
    ```
   **To associate the ad profile with your curator member:**
    ```
    $ cat member.json
    {
        “member”: {
        “default_ad_profile_id”: 123456
                  }
    }
    $ curl -b cookies -c cookies -X PUT -d ‘@member.json’ ‘https://api.appnexus.com/member’
    ```

## Examples
**Block brand category alcohol on your curator member**

Create the ad profile and associate it with your member:
```
$ cat ad-profile.json
{
 
  "ad-profile": {
    "description": "Block supermarkets",
    "categories": [
 
        {
            "id": 74,
            "status": "banned"
        }
    ],
    "default_category_status": "trusted"
  }
}
 
$ curl -b cookies -c cookies -X POST -d ‘@ad-profile.json’ ‘https://api.appnexus.com/ad-profile’
 

#response.ad-profile.id = 9876
 
$ cat member.json
 
{
  “member”: {
    “default_ad_profile_id”: 9876
  }
 
} 
 
$ curl -b cookies -c cookies -X PUT -d ‘@member.json’ ‘https://api.appnexus.com/member’
```
**Only allow Spanish creatives on curated deal 12345**

Create the ad profile and associate it with the curated deal:
```
$ cat ad-profile.json
 
{
  "ad-profile": {
    "description": "Spanish creatives only",
    "languages": [
        {
            "id": 3,
            "status": "trusted"
        }
    ],
    "default_language_status": "banned"
  }
}
 
$ curl -b cookies -c cookies -X POST -d ‘@ad-profile.json’ ‘https://api.appnexus.com/ad-profile’
 
 
#response.ad-profile.id = 5432
 
$ cat deal.json
 
{
  “deal”: {
    “ad_profile_id”: 5432
  }
}
 
$ curl -b cookies -c cookies -X PUT -d ‘@deal.json’ ‘https://api.appnexus.com/deal?id=123456’
```
