---
title: Yield Management Floor Service
description: Explore the Yield Management Floor service to create and update floors within an existing Yield Management Profile.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Yield Management Floor service

The Yield Management Floor Service is used to create and update floors within an existing [Yield Management Profile](yield-management-profile-service.md).

A floor can be thought of as the minimum price a network or publisher would like to receive for a creative. There are subtleties, however.

> [!WARNING]
> Floor settings supersede any reserve prices set via the [Placement Service](placement-service.md).
>
> **Example:** You have a soft floor setting, but no hard floor, and you've set a reserve price at the [Placement](placement-service.md) level. Since you're using [Yield Management](yield-management-profile-service.md) tools, however, your reserve price setting will be ignored. You must set it here via a hard floor.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/ym-floor?member_id=MEMBER_ID](https://api.appnexus.com/ym-floor?member_id=MEMBER_ID) | View all floors associated with a given member. |
| `GET` | - [https://api.appnexus.com/ym-floor?ym_profile_id=YM_PROFILE_ID](https://api.appnexus.com/ym-floor?ym_profile_id=YM_PROFILE_ID)<br>- [https://api.appnexus.com/ym-floor?ym_profile_code=YM_PROFILE_CODE](https://api.appnexus.com/ym-floor?ym_profile_code=YM_PROFILE_CODE) | View all floors associated with a given [Yield Management Profile](yield-management-profile-service.md). |
| `GET` | - [https://api.appnexus.com/ym-floor?id=YM_FLOOR_ID](https://api.appnexus.com/ym-floor?id=YM_FLOOR_ID)<br>- [https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE](https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE) | View a specific floor. |
| `GET` | [https://api.appnexus.com/ym-floor?id=1,2,3](https://api.appnexus.com/ym-floor?id=1,2,3) | View multiple yield management floors by ID using a comma-separated list. |
| `POST` | - [https://api.appnexus.com/ym-floor?ym_profile_id=YM_PROFILE_ID](https://api.appnexus.com/ym-floor?ym_profile_id=YM_PROFILE_ID)<br>- [https://api.appnexus.com/ym-floor?ym_profile_code=YM_PROFILE_CODE](https://api.appnexus.com/ym-floor?ym_profile_code=YM_PROFILE_CODE)<br>(ym-floor JSON) | Add a new floor. |
| `PUT` | - [https://api.appnexus.com/ym-floor?member_id=MEMBER_ID](https://api.appnexus.com/ym-floor?member_id=MEMBER_ID)<br>- [https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE](https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE)<br>(ym-floor JSON) | Modify an existing floor. |
| `DELETE` | - [https://api.appnexus.com/ym-floor?id=YM_FLOOR_ID](https://api.appnexus.com/ym-floor?id=YM_FLOOR_ID)<br>- [https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE](https://api.appnexus.com/ym-floor?code=YM_FLOOR_CODE) | Delete an existing floor.<br><br>**Note:** You cannot delete a floor that is used as the base floor for one or more Yield Management Profiles. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | int | The unique identifier for the member with which the floor is associated.<br>**Default:** `NULL`<br>**Required On:** `PUT`, in query string. |
| `id` | int | The unique identifier for a yield management floor.<br>**Default:** Auto-incremented Number (i.e. 123).<br>**Required On:** `PUT` |
| `name` | string | The name used to describe a yield management floor.<br>**Default:** `None`<br>**Required On:** `POST` |
| `code` | string | The optional custom code used to reference a yield management floor.<br>**Default:** `NULL` |
| `description` | string | The optional description of how the yield management floor is being used.<br>**Default:** `NULL` |
| `hard_floor` | double | The CPM floor used as the hard reserve price to be applied.<br>**Default:** `None`<br>**Required On:** `POST` |
| `soft_floor` | double | The CPM floor used as the soft reserve, defined as the lowest price at which price reduction will occur. This must be greater than or equal to the hard floor if set. <br>**Default:** `NULL` |
| `default_calculation_type` | enum | Whether the floor should be applied to the `gross` or `net` bid. <br>Possible values: `gross` or `net`. A `default_calculation_type` of `net` is a floor applied to the media cost paid out to the publisher.<br>**Default:** `gross` |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a floor. A profile is a generic set of rules for targeting inventory, and certain floors may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md).<br>**Default:** `NULL` |
| `priority` | int | The priority field (optional) is used to create a hierarchy of how the floor should to be applied. Value may be between `1`-`10`, where priority `10` is treated as the highest priority value.<br>**Default:** `5` |
| `ym_profile_id` | int | The ID of the yield management profile that the yield management floor is associated with. For details, see the [Yield Management Profile Service](yield-management-profile-service.md).<br><br>**Note:** This ID cannot be changed once it is set.<br><br>**Default:** `NULL`<br>**Required On:** `POST` |
| `floor_application_target` | enum | The type of bids to which the price floor is applied. <br>Possible values:<br>- `external_only`: The price floor is applied only to external bids (buying member and selling member are different). Use this option if you would rather serve an available managed learn impression than serve a default, even if this means exceeding the maximum % of daily volume for learn (`max_learn_pct` field in [Publisher Service](publisher-service.md)).<br>- `external_non_preferred`: The price floor is applied to external bids (buying member and selling member are different) or when the impression is an available managed learn impression that exceeds the maximum % of daily volume for learn. Use this option if you would rather serve a default than serve an available managed learn impression that would exceed the maximum % of daily volume for learn.<br>- `all`: The price floor is applied to all bids except managed learn impressions within the maximum % of daily volume for learn.<br>**Default:** `all` |
| `apply_floor_to_direct` | Boolean | **Removed.** Use `floor_application_target` instead. |
| `allow_tag_reserve_override` | Boolean | If `true`, allow a reserve price sent in via the ad tag query string to override the existing hard floor. The floor will only be overridden if the tag-supplied reserve price is greater than the floor price.<br>**Default:** `false` |
| `floor_optimization_enabled` | Boolean | **Deprecated** |
| `members` | array | The members to which the yield management floor should be applied. If left set to `NULL`, the floor will apply to all members. For more details, see [Members](#members) below.<br>**Default:** `NULL` |
| `brands` | array | The brands to which the yield management floor should be applied. For more details, see [Brands](#brands) below.<br>**Default:** `NULL` |
| `categories` | array | The brands or creative categories to which this yield management floor should be applied. For more details, see [Categories](#categories) below.<br>**Default:** `NULL` |
| `allowed_media_types` | array | The media types to which this yield management floor should be applied. For more details, see [Media Types](#media-types) below.<br>**Default:** `NULL` |
| `allowed_media_subtypes` | array | The media subtypes to which this yield management floor should be applied. For more details, see [Media Subtypes](#media-subtypes) below.<br>**Default:** `NULL` |

### Members

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The id of the buyer member (as found in the [Platform Member Service](platform-member-service.md)) for which the floor should be applied.<br>**Required On:** `POST`/`PUT` |
| `name` | string | The name of the buyer member.This field is **read-only**. |

### Brands

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand of the creative (as found in the [Brand Service](brand-service.md)) for which the floor should be applied.<br>**Required On:** `POST`/`PUT` |
| `name` | string | The name of the brand. This field is **read-only**. |

### Categories

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand or creative category (as described in the [Category Service](category-service.md)) to which this floor should be applied.<br>**Required On:** `POST`/`PUT` |
| `name` | string | The name of the brand or creative category. This field is **read-only**. |

### Media types

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the media type (as described in the [Media Type Service](media-type-service.md)) to which this floor should be applied.<br>**Required On:** `POST`/`PUT` |
| `name` | string | The name of the media type. This field is **read-only**. |

### Media subtypes

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the media subtype (as described in the [Media Subtype Service](media-subtype-service.md)) to which this floor should be applied.<br>**Required On:** `POST`/`PUT` |
| `name` | string | The name of the media subtype. This field is **read-only**. |

## Examples

### View a specific floor

```
$ curl -b cookies -c cookies  "https://api.appnexus.com/ym-floor?id=1234"
{
    "ym-floor": {
        "member_id": 3,
        "id": 1234,
        "name": "Germany Floor",
        "description": "This rule will used to set the floor for a set of demand attributes across Germany inventory.",
        "hard_floor": 1.20,
        "soft_floor": null,
        "default_calculation_type": "gross",
        "apply_floor_to_direct": true,
        "floor_application_target": "all",
        "profile_id": 1542,
        "priority": 6,
        "ym_profile_id": 1234,
        "members": [{
            "id": 100,
            "name": "eBay"
        }, {
            "id": 256,
            "name": "MiG"
        }],
        "brands": [{
            "id": 102,
            "name": "Netflix"
        }, {
            "id": 256,
            "name": "Blockbuster"
        }],
        "categories": [{
            "id": 2,
            "name": "Apparel"
        }, {
            "id": 8,
            "name": "Dating"
        }],
        "allowed_media_types": [{
            "id": 1,
            "name": "Banner"
        }, {
            "id": 4,
            "name": "Video"
        }],
        "allowed_media_subtypes": [{
            "id": 1,
            "name": "Standard Banner"
        }, {
            "id": 8,
            "name": "30-second VAST"
        }]
    }
}
```

### View all floors associated with a [Yield Management Profile](yield-management-profile-service.md)

Notice that the following floors target by optional `{{profile_id}}` rather than via the `{{members}}` array. For details, see [JSON fields](#json-fields) above.

```
$ curl -b cookies "https://api.appnexus.com/ym-floor?ym_profile_id=9999"
{
    "response": {
        "start_element": null,
        "count": 2,
        "ym-floors": [{
            "priority": 5,
            "last_modified": "2011-11-03 23:04:24",
            "soft_floor": 0.23999999999999999,
            "member_id": 123,
            "name": "Placement 60 + Size 300x250 Floor",
            "floor_application_target": "all",
            "default_calculation_type": "gross",
            "brands": null,
            "ym_profile_id": 9999,
            "code": "Tattooed Bikers Galore",
            "hard_floor": 0,
            "id": 555,
            "description": null,
            "profile_id": 23,
            "members": null,
            "categories": null,
            "allowed_media_types": null,
            "allowed_media_subtypes": null
        }, {
            "priority": 5,
            "last_modified": "2011-11-04 01:18:35",
            "soft_floor": 0.050000000000000003,
            "member_id": 1,
            "name": "Placement+Size 728x90 Floor",
            "floor_application_target": "all",
            "default_calculation_type": "gross",
            "brands": null,
            "ym_profile_id": 9999,
            "code": "Tattooed Bikers Knit and Sew",
            "hard_floor": 0,
            "id": 4,
            "description": null,
            "profile_id": 9,
            "members": null,
            "categories": null,
            "allowed_media_types": null,
            "allowed_media_subtypes": null
        }],
        "status": "OK",
        "num_elements": null
    }
}
```
