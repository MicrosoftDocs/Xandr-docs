---
title: Bidders - Object Limit Service
description: In this article, learn about bidders Object Limit service, their JSON fields, and REST API with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Object Limit service

Xandr limits the number of non-expired creatives that you can have on the platform. In addition, Xandr limits the number of domains that can be used in a single domain list and the number of certain targets that can be used in a single profile. For all object types except creatives, both active and inactive objects are counted against the limit. For creatives, only non-expired objects are counted against the limit. A creative expires when it has neither served nor been modified in over last 14 days (on the 15th day, it is updated as **Expired**).

The Object Limit Service allows you to view these limits and proactively monitor your current usage.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/object-limit](https://api.adnxs.com/object-limit) | View your limits and current usage for all object types. |
| `GET` | [https://api.adnxs.com/object-limit?object_type=OBJECT_TYPE](https://api.adnxs.com/object-limit?object_type=OBJECT_TYPE) | View your limit and current usage for a specific object type.<br><br>**Tip:** The following object types are available: `creative`, `profile`, and `domain_list`. |

## JSON fields

| Field | Type  | Description |
|:---|:---|:---|
| `count_active` | int | The current number of active objects. For creatives, this count does not include expired creatives. |
| `count_inactive` | int | The current number of inactive objects, not including deleted objects. For creatives, this count does not include expired creatives. |
| `count_total` | int | The current total number of active and inactive objects. For creatives, this count does not include expired creatives. |
| `limit` | int | The maximum number of objects that the bidder is allowed. For all object types except `"creative"`, both active and inactive objects are counted agains the limit. For creatives, only non-expired objects are counted against the limit. |
| `mapping_limits` | object | This field is populated only for the `"profile"` and `"domain_list"` object types. It lists the limits for objects within each profile and domain list, for example, the maximum number of segment targets you can use in a single profile or the maximum number of domains you can use in a single domain list. For more details, see "[Mapping Limits](#mapping-limits)" below. |
| `object_type` | enum | The type of object. Possible values: `"creative"`, `"profile"`, or `"domain_list"`.<br><br>**Note:** For `"profile"` and `"domain_list"`, the `limit`, `count_active`, `count_inactive`, and `count_total` fields will show a value of `null`, as Xandr does not limit the number of profiles and domain lists that you can have. Xandr does limit the number of objects within each profile or domain list, however. These limits will be shown in the `mapping_limits` field. |

### Mapping limits

This part of the JSON response is populated only for the `"profile"` and `"domain_list"` object types. It lists the limits for objects within each profile and domain list.

#### For profiles

| Field | Type  | Description |
|:---|:---|:---|
| `content_category_targets` | int | The maximum number of custom content categories that you can target in a single profile. |
| `inventory_source_targets` | int | **Deprecated.** |
| `placement_targets` | int | The maximum number of placements that you can target in a single profile. |
| `platform_content_category_targets` | int | The maximum number of Xandr-defined content categories that you can target in a single profile. |
| `postal_code_targets` | int | The maximum number of postal codes that you can target in a single profile. |
| `publisher_targets` | int | The maximum number of publishers that you can target in a single profile. |
| `segment_group_targets` | int | The maximum number of segment groups that you can target in a single profile. |
| `segment_targets` | int | The maximum number of segments that you can target in a single profile. |
| `site_targets` | int | The maximum number of sites that you can target in a single profile. |

#### For domain lists

| Field | Type  | Description |
|:---|:---|:---|
| `domains` | int | The maximum number of domains that you can include or exclude in a single domain list. |

## Examples

### View your limits and current usage for all object types

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/object-limit'
{
    "response": {
        "status": "OK",
        "count": null,
        "start_element": null,
        "num_elements": null,
        "object-limits": [
            {
                "object_type": "profile",
                "limit": null,
                "mapping_limits": {
                    "inventory_source_targets": 500,
                    "content_category_targets": 300,
                    "platform_content_category_targets": 300,
                    "postal_code_targets": 4000,
                    "segment_targets": 400,
                    "publisher_targets": 300,
                    "site_targets": 100,
                    "placement_targets": 250,
                    "segment_group_targets": 400
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "domain_list",
                "limit": null,
                "mapping_limits": {
                    "domains": 30000
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "creative",
                "limit": 16000,
                "mapping_limits": [
                ],
                "count_active": 0,
                "count_inactive": 0,
                "count_total": 0
            }
        ],
        "dbg": {
        ...
        }
    }
}
```

### View your limits and current usage for creatives

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/object-limit?object_type=creative'
{
    "response": {
        "status": "OK",
        "count": null,
        "start_element": null,
        "num_elements": null,
        "object-limits": [
            {
                "object_type": "creative",
                "limit": 16000,
                "mapping_limits": [
                ],
                "count_active": 0,
                "count_inactive": 0,
                "count_total": 0
            }
        ],
        "dbg": {
            ...
        }
    }
}
```

## FAQs

For a list of frequently asked questions about object limits, see [Object Limits - FAQ](object-limits---faq.md).

## Deleting objects

When you approach your limit for domain lists or profile target, you should remove inactive, unused, or unnecessary objects.

- To remove domains from a domain list, you make a `PUT` call to the [Domain List Service](domain-list-service.md), updating the `domains` array.
- For information about removing a target from a profile, see [Enhanced Bidder Profiles](enhanced-bidder-profiles.md).

When you approach your limit for creatives, you should remove non-expired creatives. Non-expired creatives have the `is_expired` field set to `false`.

> [!NOTE]
> Removing expired creatives will not impact your creative count.

To remove a creative, you make a `DELETE` call to the [Creative Service](../digital-platform-api//creative-service.md).
