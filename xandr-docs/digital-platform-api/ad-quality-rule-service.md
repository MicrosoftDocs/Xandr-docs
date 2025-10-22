---
title: Ad Quality Rule Service
description: In this article, learn about the Ad Quality Rule service, their JSON parameters, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Ad quality rule service

An ad quality rule defines the ad quality settings which a network can define for its managed publishers. A network may have more than one ad quality rule applied conditionally across a publisher's inventory. For instance, traffic originating from certain geo-locations may require different ad quality settings.

## REST API

> [!NOTE]
>
> - `publisher_code` can be used in place of `publisher_id`, and `ad_quality_rule_code` can be used in place of `ad_quality_rule_id` for all of the calls below.
> - If an Ad Quality (AQ) is set as `"default_brand_status": "banned"` but the parent brand is set as `"status": "trusted"`, the child brand overrides the setting in `"default_brand_status"` and it will be able to serve unless it is explicitly banned in the Ad Profile's brand override list.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/ad-quality-rule?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ad-quality-rule?publisher_id=PUBLISHER_ID)<br>(payment rule JSON) | Add an Ad Quality Rule. |
| `PUT` | [https://api.appnexus.com/ad-quality-rule?id=AD_QUALITY_RULE_ID&publisher_id=PUBLISHER_ID](https://api.appnexus.com/ad-quality-rule?id=AD_QUALITY_RULE_ID&publisher_id=PUBLISHER_ID)<br>(publisher rule JSON) | Modify an existing Ad Quality Rule. |
| `GET` | [https://api.appnexus.com/ad-quality-rule?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ad-quality-rule?publisher_id=PUBLISHER_ID) | View all of the ad quality rules for a publisher. |
| `GET` | [https://api.appnexus.com/ad-quality-rule?id=AD_QUALITY_RULE_ID](https://api.appnexus.com/ad-quality-rule?id=AD_QUALITY_RULE_ID) | View a specific ad quality rule for a publisher. |
| `GET` | [https://api.appnexus.com/ad-quality-rule?id=1,2,3](https://api.appnexus.com/ad-quality-rule?id=1,2,3) | View multiple ad quality rules by ID using a comma-separated list. |

## JSON parameters

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for a ad quality rule.<br>**Default:** Auto-incremented number (i.e. 123).<br>**Required On:** `PUT` |
| `code` | string | A optional custom code used to reference an ad quality rule.<br>**Default:** Null |
| `name` | string | A name used to describe an ad quality rule.<br>**Default:** None<br>**Required On:** `POST` |
| `description` | string | Optional description. |
| `ad_profile_id` | int | You are required to provide an ad profile which defines quality restrictions that should be applied to this rule.<br>**Required On:** `POST` |
| `publisher_id` | int | The id of the publisher for which this ad quality rule will apply.<br>**Required On:** `POST` and `PUT` |
| `member_id` | int | The id of the publisher's member for which this ad quality rule will apply. |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply an ad quality rule. A profile is a generic set of rules for targeting inventory, and certain ad quality rules may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md). |
| `priority` | int | You can optionally provide a priority which defines the level at which this rule should that be applied relative to other payment rules.<br>**Default:** 5 |
| `last_modified` | timestamp | Time of last modification to this ad quality rule. |

## Examples

### Define an Ad Quality rule

```
$ cat ad-quality-rule.json
{"ad-quality-rule":
      {
        "name": "Default Ad Quality Rule",
        "description": "These quality standards will serve as the catch-all settings for this publisher",
        "active": true,
        "publisher_id": 34147,
        "ad_profile_id": 32,
        "profile_id": null,
        "priority": 1
      }
}
```

### `POST` the Ad Quality rule for a publisher

```
$ curl -s -c cookies -b cookies -X POST -d @ad-quality-rule.json "https://api.appnexus.com/ad-quality-rule?publisher_id=34147" | json_reformat
{
  "response": {
    "status": "OK",
    "id": 103679,
    "dbg_info": {
      ...
    }
  }
}
```

### View a specific Ad Quality rule

```
$ curl -s -c cookies -b cookies "https://api.appnexus.com/ad-quality-rule?id=103679" | json_reformat
{
  "response": {
    "status": "OK",
    "ad-quality-rule": {
      "id": 103679,
      "code": null,
      "name": "Default Ad Quality Rule",
      "description": "These quality standards will serve as the catch-all settings for this publisher",
      "active": true,
      "publisher_id": 34147,
      "ad_profile_id": 32,
      "profile_id": 0,
      "priority": 1
    },
    "dbg_info": {
      ...
    }
  }
}
```
