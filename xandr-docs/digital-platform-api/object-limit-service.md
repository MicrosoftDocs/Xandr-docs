---
title: Digital Platform API - Object Limit Service
description: Learn about the Object Limit service. Limits are set for various categories of content on the platform, including line items, campaigns, creatives, and domains.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Object Limit service

Xandr limits the number of line items, campaigns, creatives, publishers, sites, placements, packages, deals, mediated networks, and mediated bids that you can have on the platform. In addition, Xandr limits the number of domains that can be used in a single domain list, the number of certain targets that can be used in a single profile, and the number of content categories that can be assigned to a single placement. For all object types except creatives, both active and inactive objects are counted against the limit. For creatives, only non-expired objects are counted against the limit.

The Object Limit Service allows you to view these limits and proactively monitor your current usage.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/object-limit` | View your limits and current usage for all object types. |
| `GET` | `https://api.appnexus.com/object-limit?object_type=OBJECT_TYPE` | View your limit and current usage for a specific object type.<br><br>**Note**: The following object types are available: <br> - `campaign` <br> - `profile` <br> - `domain_list` <br> - `creative` <br> - `publisher` <br> - `site` <br> - `placement` <br> - `package` <br> - `deal` <br> - `mediated_network` <br> - `mediated_bid`. <br>Note that to retrieve your limit for line items, you must use `campaign_group`. |

## JSON fields

| Field | Type  | Description |
|:---|:---|:---|
| `count_active` | int | The current number of active objects. For creatives, this count does not include expired objects. |
| `count_inactive` | int | The current number of inactive objects, not including deleted objects. For creatives, this count does not include expired objects. |
| `count_total` | int | The current total number of active and inactive objects. For creatives, this count does not include expired objects. |
| `limit` | int | The maximum number of objects that the member is allowed. For all object types except `"creative"`, both active and inactive objects are counted agains the limit. For creatives, only non-expired objects are counted against the limit. |
| `mapping_limits` | object | This field is populated only for the `"profile"`, `"domain_list"`, and `"placement"` object types. It lists the limits for objects within each profile and domain list, for example, the maximum number of segment targets you can use in a single profile or the maximum number of domains you can use in a single domain list. For placements, it lists the maximum number of content categories that can be applied to a placement See [Mapping Limits](#mapping-limits) below for more details. |
| `object_type` | enum | The type of object. Possible values: <br> - `"line_item"` <br> - `"campaign"` <br> - `"profile"` <br> - `"domain_list"` <br> - `"creative"` <br> - `"publisher"` <br> - `"site"` <br> - `"placement"` <br> - `"package"` <br> - `"deal"` <br> - `"mediated_network"` <br> - `"mediated bid"`.<br><br>**Note**:<br>For `"profile"` and `"domain_list"`, the `limit`, `count_active`, `count_inactive`, `count_total` fields will show a value of `null`, as Xandr does not limit the number of profiles and domain lists that you can have. Xandr does limit the number of objects within each profile or domain list, however. These limits will be shown in the `mapping_limits` field. |

## Mapping limits

This part of the JSON response is populated only for the `"profile"`, `"domain_list"`, and `"placement"` object types.

### For profiles

| Field | Type  | Description |
|:---|:---|:---|
| `content_category_targets` | int | The maximum number of custom content categories that you can target in a single profile. |
| `inventory_source_targets` | int | **Deprecated**. |
| `placement_targets` | int | The maximum number of placements that you can target in a single profile. |
| `platform_content_category_targets` | int | The maximum number of platform-defined content categories that you can target in a single profile. |
| `postal_code_targets` | int | The maximum number of postal codes that you can target in a single profile. |
| `publisher_targets` | int | The maximum number of publishers that you can target in a single profile. |
| `segment_targets` | int | The maximum number of segments that you can target in a single profile. |
| `segment_group_targets` | int | The maximum number of segment groups that you can target in a single profile. |
| `site_targets` | int | The maximum number of sites that you can target in a single profile. |

### For domain lists

| Field | Type  | Description |
|:---|:---|:---|
| `domains` | int | The maximum number of domains that you can include or exclude in a single domain list. |

### For placements

| Field | Type  | Description |
|:---|:---|:---|
| `content_categories` | int | The maximum number of content categories that you can apply to a single placement. |

## Examples

### View your limits and current usage for all object types

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/object-limit'
{
    "response": {
        "status": "OK",
        "count": 21,
        "start_element": 0,
        "num_elements": 100,
        "object-limits": [
            {
                "object_type": "site",
                "limit": 10000,
                "mappings": [
                ],
                "count_active": 8,
                "count_inactive": 0,
                "count_total": 8
            },
            {
                "object_type": "publisher",
                "limit": 3000,
                "mappings": [
                ],
                "count_active": 8,
                "count_inactive": 0,
                "count_total": 8
            },
            {
                "object_type": "profile",
                "limit": null,
                "mappings": {
                    "site_targets": 100,
                    "publisher_targets": 300,
                    "inventory_source_targets": 500,
                    "content_category_targets": 300,
                    "placement_targets": 250,
                    "segment_targets": 400
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "placement",
                "limit": 20000,
                "mappings": [
                ],
                "count_active": 21,
                "count_inactive": 0,
                "count_total": 21
            },
            {
                "object_type": "line_item",
                "limit": 3000,
                "mappings": [
                ],
                "count_active": 4,
                "count_inactive": 1,
                "count_total": 5
            },
            {
                "object_type": "domain_list",
                "limit": null,
                "mappings": {
                    "domain": 30000
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "creative",
                "limit": 10000,
                "mappings": [
                ],
                "count_active": 32,
                "count_inactive": 0,
                "count_total": 32
            },
            {
                "object_type": "campaign",
                "limit": 10000,
                "mappings": [
                ],
                "count_active": 6,
                "count_inactive": 6,
                "count_total": 12
            }
        ]
    }
}
```

### View your limits and current usage for creatives

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/object-limit?object_type=creative'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "object-limits": [
            {
                "object_type": "creative",
                "limit": 10000,
                "mappings": [
                ],
                "count_active": 32,
                "count_inactive": 0,
                "count_total": 32
            }
        ]
    }
}
```

## Default limits

For a list of default object limits and frequently asked questions, see [API Usage Constraints](./api-usage-constraints.md).

## Deleting objects

When you approach or reach your limit for line items, campaigns, publishers, sites, or placements, you can use reports such as [Network Advertiser Analytics](./network-advertiser-analytics.md) and [Network Publisher Analytics](./network-publisher-analytics.md) to identify objects that have, for example, not been modified or used in the last 30 days, and then delete those objects manually. For line items and campaigns, you can also use a query string filter to find objects based on when they first or last had impressions. See [Line Item Service](./line-item-service.md) and [Campaign Service](./campaign-service.md) for more information.

When you approach or reach your limit for creatives, you should delete non-expired creatives. Non-expired creatives have the `is_expired` field set to `false`. Note that removing expired creatives will not impact your creative count.
