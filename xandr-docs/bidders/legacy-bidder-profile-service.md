---
title: Legacy Bidder Profile Service
description: In this article, learn about legacy bidder profile service, their filtering criteria, JSON fields, and REST API with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Legacy Bidder Profile service

Bidder Profiles are used to create and manage filtering criteria for which real-time [Bid Requests](outgoing-bid-request-to-bidders.md) you wish to receive. Profiles allow you to limit resources required to process unwanted bid requests. See the [Bidder Profile - FAQ](bidder-profile---faq.md).

## Important notes

- For a bid request to pass a bidder profile, the bid request must meet ALL of the specified filter criteria.
- You may create multiple profiles for your bidder, but **only one** parent profile can be **active** for your bidder at any given time. Activate a profile by associating it with your bidder, using the [Bidder Service](bidder-service.md).
- Your bidder will always receive bid requests for inventory that is owned by a member associated with your bidder. Bidder profiles are not applied in this case.
- Data Provider bidders can only have one parent profile and no child profiles.

> [!WARNING]
> Profiles must be attached to an active bidder object.
>
> After you create a profile, you must attach the profile to your bidder by specifying `"parent_profile_id"` via the [Bidder Service](bidder-service.md).
>
> Do not use deprecated fields.
>
> Do not include any of the fields marked as deprecated below when you are configuring your profile(s). This will lead to your bidder not receiving the expected volume of bid requests.
>
> Frequent profile updates may temporarily lock that profile.
>
> If you make multiple updates to a bidder profile within 30 minutes, the profile can potentially get locked as a safety precaution. If a profile gets locked, traffic matching only this profile will not go through for approximately 5 minutes.

## Supported filtering criteria

The following filtering criteria are currently supported:

- Selling Member
  - Specify whether to require or exclude inventory from members, see the [Platform Member Service](platform-member-service.md).

> [!NOTE]
> The Xandr Direct Seller Member Group is included by default and cannot be excluded via the API. For more information, see [Supply for External Demand Partners](xandr-monetize-supply-for-external-demand-partners.md).

- Geography
  - Country
    - Include/exclude requests for a specified set of countries, OR
    - Receive bid requests for any countries EXCEPT a specified set of countries.
  - Region
    - Include/exclude requests for a specified set of regions, OR
    - Receive bid requests for any regions EXCEPT a specified set of regions.
  - DMA
    - Include/exclude requests for a specified set of DMAs, OR
    - Receive bid requests for any regions EXCEPT a specified set of DMAs.
- Inventory
  - Domain List
    - Include/exclude requests for impressions that meet the requirements of allowlists or blocklists.
  - Inventory Attribute
    - Include/exclude requests for impressions that contain certain inventory attributes.
  - Audit Status
    - Exclude requests from domains that have not been audited by Xandr.
- Audience

> [!WARNING]
> As of April 27, 2019, Xandr no longer supports segments on the platform for externally integrated DSPs.

- Segment Targeting
  - Include/exclude requests for users that satisfy the segment targeting criteria.

- Creative Size
  - Include/exclude bid requests for the specified set of creative sizes.
- Supply Type (web/mobile_app/mobile_web)
  - Include/exclude impressions for regular web and mobile apps.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/profile/BIDDER_ID](https://api.adnxs.com/profile/BIDDER_ID) | **View Profiles:** To see all of the profiles attached to your bidder. |
| `GET`  | [https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID](https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID) | **View Profiles:** To see a specific profile attached to your bidder. |
| `POST` | [https://api.adnxs.com/profile/BIDDER_ID](https://api.adnxs.com/profile/BIDDER_ID)<br>(profile JSON) | Add a Profile for your bidder. |
| `PUT`  | [https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID](https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID)<br>(profile JSON) | Modify an Existing Profile. |
| `DELETE` | [https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID](https://api.adnxs.com/profile/BIDDER_ID/PROFILE_ID)<br><br>**Note:** Only inactive profiles can be deleted; that is profiles that are not associated with the bidder object. | Delete an existing profile. |
|  | Use the [Bidder Service](bidder-service.md) to set the `profile_id` field on the bidder to the id of the desired bidder profile. | Activate a profile for your bidder as the parent profile. |
|  | Use the [Bidder Service](bidder-service.md) to update the child_profiles array on the bidder to include id of the desired bidder profile. | Activate a profile for your bidder as a child profile. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `ID` | String | Unique identifier for the bidder profile.<br>**Required:** Yes, on update. |
| `code` | String | Alternative identifier for the bidder profile, specific to the bidder.<br>**Required:** No. |
| `description` | String | Description of the bidder profile.<br>**Required:** No. |
| `last_activity` | timestamp | The timestamp of the last modification to the profile.<br>**Required:** No. |
| **Bid Throttling** |  |  |
| `passthrough_percent` | double | The percent (50 = 50%) of bid requests which satisfy your profile targeting that you wish to receive. Requests that are sent to your bidder are randomly chosen, although you can choose for your bidder to always receive requests for users in segments of members associated with your bidder. If you set `passthrough_percent` to `0`, your bidder will only receive requests for users in at least one of your members' segments. These values take effect in increments of 0.1.<br>**Required:** No. |
| **Member Filtering** |  |  |
| `member_targets` | Array of Objects | Array of objects that include the member IDs of members. The default action, if no action is specified, is `"include"` - meaning the member IDs must be included. This may be overridden by specifying an `"action"` in the object, e.g. `"member_targets":[{"id":"100","action": "exclude"}]`. <br>For more details, see [Platform Member Service](platform-member-service.md). <br>**Required:** No. |
| **Geography Filtering** |  |  |
| `country_action` | Enum - "exclude" or "include" | If `"exclude"`, only bid requests for countries NOT in `"country_targets"` will be sent to the bidder. If `"include"`, only bid requests for countries in `"country_targets"` will be sent to the bidder. Default is `exclude`.<br>**Required:** No. |
| `country_targets` | Array of Objects | The country IDs to be either excluded or included, as defined by the `country_action` field. You can use the [Country Service](country-service.md) to retrieve a list of country IDs. For more details and format, see [Country Targets](#country-targets).<br>**Required:** No. |
| `region_action` | Enum - "exclude" or "include" | If `"exclude"`, only bid requests for regions NOT in `"region_targets"` will be sent to the bidder. If `"include"`, only bid requests for regions in `"region_targets"` will be sent to the bidder.<br>Default is `exclude`.<br>**Required:** No. |
| `region_targets` | Array of Objects | The region/state IDs to be either excluded or included, as defined by the `region_action` field. You can use the [Region Service](region-service.md) to retrieve a list of region IDs. <br>For more details and format, see [Region Targets](#region-targets).<br>**Required:** No. |
| `dma_targets` | Array of Objects | Array of objects specifying the dmas to be targeted (for inclusion or exclusion).<br>E.g. `[{"dma":123}, {"dma":124}]`<br>**Required:** No. |
| `dma_action` | Enum - "exclude" or "include" | Defaults to `"exclude"`. See `dma_targets`.<br>**Required:** No. |
| `city_targets` | Array of Objects | The IDs of cities to be either included or excluded, as defined by the `city_action` field. You can use the [City Service](city-service.md) to retrieve a list of city IDs. For more details and format, see [City targets](#city-targets).<br>**Required:** No. |
| `city_action` | Enum - "exclude" or "include" | If `"exclude"`, only bid requests for cities NOT in `"city_targets"` will be sent to the bidder. If `"include"`, only bid requests for cities in `"city_targets"` will be sent to the bidder.<br>Default is `exclude`.<br>**Required:** No. |
| **Inventory** |  |  |
| `inventory_action` | Enum - "exclude" or "include" | **Deprecated**. Leave it as `"exclude"` and don't use this field, as this can reduce the available inventory sent to your bidder.<br>**Required:** No. |
| `use_inventory_attribute_targets` | Boolean | If set to `"true"`, then `inventory_attribute_targets` will be applied. This flag allows you to `"opt-in"` to receive certain inventory attributes, such as toolbars, if they exist for a piece of inventory. If `"false"`, the bidder will receive all inventory. <br>**Required:** No. |
| `inventory_attribute_targets` | Array of [inventory attribute](inventory-attribute-service.md) objects. | An array of objects for the targets to include, e.g. `[{"id":12}]`. If `use_inventory_attribute_targets` is enabled, we will send bid requests that contain the selected attributes. We will also send bid requests that contain no inventory attributes. To exclude a particular inventory attribute, simply include all the IDs except for the attribute you wish to exclude.<br>**Required:** No. |
| `non_audited_url_action` | string | If this is set to `"exclude"`, all inventory that has not been audited by Xandr will be excluded. Otherwise, all inventory will be included.<br>**Required:** No. |
| `domain_list_action` | Enum - "exclude" or "include" | Default action to apply to `domain_list_target`.<br>**Required:** No. |
| `domain_list_targets` | Array of objects with the ID of the domain lists. | Array of objects for the domain list targets, e.g. `[]`. Only bid requests for inventory that match the `domain_list_action` for the enumerated domain lists will be sent to the bidder.<br>**Required:** No. |
| `domain_action` |  | **Required:** Deprecated. |
| `domain_targets` |  | **Required:** Deprecated. |
| **Audience** |  |  |
| `segment_targets` | Array of segment targets with the ID and action for each. | If `"segment_boolean_operator"` is `"and"`, then if `"action"` for a segment is set to `"exclude"`, then impressions for users that are in that segment not be sent to the bidder; if any `"action"` is set to `"include"`, then users in the segments being included will be sent to the bidder. If `"segment_boolean_operator"` is set to `"or"`, then users that meet any of the `segment_targets` criteria will be sent to the bidder.<br><br>**Warning:** As of April 27, 2019, Xandr will no longer support segments on the platform for externally integrated DSPs.<br>**Required:** No. |
| `segment_boolean_operator` | Enum - "and" or "or" | Action to apply to the `segment_targets`. "And" means all of the criteria must be satisfied. "Or" means at least one must be met.<br><br>**Warning:** As of April 27, 2019, Xandr will no longer support segments on the platform for externally integrated DSPs.<br>**Required:** No. |
| **Supply Type (web / mobile)** |  |  |
| `supply_type_targets` | Array of supply type targets:<br>"mobile_app" (for mobile app inventory),<br>"mobile_web" (for mobile web inventory),<br>"web" (for regular display inventory) | Determines which supply type targets should be included or excluded pursuant to `supply_type_action`.<br>**Required:** No. |
| `supply_type_action` | Enum - "exclude" or "include" | Action to apply to `supply_type_targets`.<br>**Required:** No. |
| **Mobile-Specific** |  |  |
| `carrier_targets` | Not yet supported | **Required:** No. |
| `carrier_action` | Enum - "exclude" or "include" | Action to apply to `carrier_targets`.<br>**Required:** No. |
| `handset_make_targets` | Not yet supported | **Required:** No. |
| `handset_make_action` | Enum - "exclude" or "include" | Action to apply to `handset_make_targets`.<br>**Required:** No. |
| `handset_model_targets` | Not yet supported | **Required:** No. |
| `handset_model_action` | Enum - "exclude" or "include" | Action to apply to `handset_model_targets`.<br>**Required:** No. |
| `location_target_radius` | Not yet supported | **Required:** No. |
| `location_target_latitude` | Not yet supported | **Required:** No. |
| `location_target_longitude` | Not yet supported | **Required:** No. |
| **Other** |  |  |
| `size_targets` | Array of Objects | Array of widths and heights, specifying creative sizes that your bidder will bid on. <br>E.g. `[{"width":300,"height":250},{"width":600,"height":160}]`<br>**Required:** No. |
| **Not Currently Supported** |  |  |
| `language_targets` |  | This field is not currently available. |
| `postal_code_targets` |  | This field is not currently available. |
| `age_targets` |  | This field is not currently available. |
| `daypart_targets` |  | This field is not currently available. |
| `browser_targets` |  | This field is not currently available. |

### Country targets

Each object in the `country_targets` array contains the following fields.

| Field | Type | Description |
|---|---|---|
| `id` | int | The ID of the country. You can use the [Country Service](country-service.md) to retrieve a complete list of country IDs. |
| `name` | string | **Read-only.** The name of the country. |
| `code` | string | **Read-only.** The code for the country. |

#### Country targets: Example

```
{
    "profile": {
        "country_action": "include",
        "country_targets": [
            {
                "id": 233,
                "name": "United States",
                "code": "US"
            }
        ]
    }
}
```

### Region targets

Each object in the `region_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the region. You can use the [Region Service](region-service.md) to retrieve a list of region IDs. |
| `name` | string | **Read-only.** The name of the region. |
| `code` | string | **Read-only.** The code for the region. |
| `country_name` | string | **Read-only.** The name of the country to which the region belongs. |
| `country_code` | string | **Read-only.** The code for the country to which the region belongs. |

#### Region targets: Example

```
{
    "profile": {
        "region_action": "include",
        "region_targets": [
            {
                "id": 1
                                "name": "New York",
                                "code": "NY",
                "country_name": "United States",
                                "country_code": "US"
            }
        ]
    }
}
```

### City targets

Each object in the `city_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the city to target. You can use the [City Service](city-service.md) to retrieve a list of city IDs. |
| `name` | string | **Read-only.** The name of the city to target. |
| `region_name` | string | **Read-only.** The name of the region to which the city belongs. |
| `region_code` | string | **Read-only.** The code of the region to which the city belongs. |
| `country_name` | enum | **Read-only.** The name of the country to which the region belongs. |
| `country_code` | enum | **Read-only.** The code of the country to which the region belongs. |

#### City targets: Example

```
{
    "profile": {
        "city_action": "include",
        "city_targets": [
            {
                "id": 123,
                "name": "Queens",
                "region_name": "New York",
                "region_code": "NY",
                "country_code": "US",
                "country_name": "United States",
            }
        ]
    }
}
```

## Authentication token

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. For more detailed instructions, see [Authentication Service](authentication-service.md).

## Examples

### Add a new profile to bidder 6

The ID of the new profile is 123.

```
$ cat bidder_profile:
    {
    "profile":
        {
        "description": "Only Alberta (NO US can be included)",
        "country_action": "include",
        "country_targets": [{"id": 1},{"ide":2}],
        "region_action": "exclude",
        "region_targets": [{id: 1}],
        "member_targets": [
           {
             "id": "100",
             "action": "exclude"
           },
           {
             "id": "102",
             "action": "exclude",
             "name": "Inventory name 2"
           }
        ],
        "dma_targets": [{"dma":123}, {"dma":124}],
        "dma_action": "exclude",
        "segment_boolean_operator": "and",
        "segment_targets": [
         {
          "id": "16808",
          "name": "Users meeting certain criteria",
          "action": "include",
          "start_minutes": null,
          "expire_minutes": null,
          "other_less": null,
          "other_greater": null,
          "other_equals": null
         },
         {
          "id": "16809",
          "name": "Users that have seen an ad for this campaign and should not be targeted for 2 days",
          "action": "exclude",
          "start_minutes": null,
          "expire_minutes": "2880",
          "other_less": null,
          "other_greater": null,
          "other_equals": null,
         }
        ],
        "size_targets": [{"width":300,"height":250},{"width":600,"height":160}]
        }
    }
    $ curl -b cookies -c cookies -X POST --data-binary @bidder_profile "https://api.adnxs.com/profile/6"
    {
    "response":
       {
         "status":"OK",
         "id":"123"
       }
    }
```

### View all profiles currently associated with bidder 6

```
curl -b cookies -c cookies "https://api.adnxs.com/profile/6"
```

### View profile 123 associated with bidder 6

```
curl -b cookies -c cookies "https://api.adnxs.com/profile/6/123"
```

To activate a profile for your bidder, use the [Bidder Service](bidder-service.md) to set the `profile_id` field on the bidder to the ID of the desired bidder profile.

### Update profile ID 123 on bidder 6

```
$ cat bidder_profile:
    {
    "profile":
        {
        "id": "123",
        "country_action": "include",
        "country_targets": [{"id": 233}]
        }
    }
    $ curl -b cookies -c cookies -X PUT --data-binary @bidder_profile "https://api.adnxs.com/profile/6/123"
```

### Add a domain list to your bidder profile as a "blocklist"

> [!TIP]
> For more information about domain lists, see the [Domain List Service](domain-list-service.md).

```
$ cat domain-list-profile
{
   "profile" : {
      "domain_list_targets" : [
         {
            "id" : 9351
         }
      ],
      "domain_list_action" : "exclude",
      "id" : 431739
   }
}
$ curl -b cookies -c cookies -X PUT --data-binary @domain-list-profile 'https://api.adnxs.com/profile/497/431739'
{
   "response" : {
      "count" : 1,
      "num_elements" : null,
      "id" : "431739",
      "profile" : {
         "supply_type_targets" : null,
         "browser_targets" : null,
         "id" : 431739,
         "dma_targets" : null,
         "screen_size_targets" : null,
         "inventory_attribute_targets" : null,
         "device_type_targets" : null,
         "dma_action" : "exclude",
         "operating_system_targets" : null,
         "domain_list_targets" : [
            {
               "id" : 9351,
               "deleted" : false,
               "type" : "black",
               "description" : "Rich's awesome domain list (blocklist)",
               "name" : "Rich's awesome domain list (blocklist)"
            }
         ],
         "session_freq_type" : "platform",
         "operating_system_family_targets" : null,
         "domain_targets" : null,
         "venue_targets" : null,
         "description" : "Ethical Ad Blocker Test Segment",
         "city_targets" : null,
         "age_targets" : null,
         "domain_action" : "exclude",
         "inventory_action" : "exclude",
         "site_targets" : null,
         "size_targets" : [
            {
               "width" : 300,
               "height" : 50
            },
            {
               "width" : 300,
               "height" : 250
            }
         ],
         "location_target_radius" : null,
         "language_action" : "exclude",
         "ip_targets" : null,
         "segment_targets" : [
            {
               "deleted" : false,
               "other_greater" : null,
               "name" : "ethical ad blocker segment 00",
               "code" : "ethical-adblock-00",
               "other_less" : null,
               "expire_minutes" : null,
               "action" : "include",
               "other_in_list" : null,
               "id" : 110944,
               "other_equals" : null,
               "start_minutes" : null
            }
         ],
         "is_expired" : false,
         "region_action" : "exclude",
         "location_target_latitude" : null,
         "code" : "ethical-adblock-00",
         "inventory_group_targets" : null,
         "country_action" : "exclude",
         "querystring_targets" : null,
         "carrier_targets" : null,
         "member_id" : null,
         "passthrough_percent" : 100,
         "segment_boolean_operator" : "or",
         "intended_audience_targets" : null,
         "operating_system_extended_targets" : null,
         "device_model_action" : "exclude",
         "language_targets" : null,
         "gender_targets" : null,
         "non_audited_url_action" : "include",
         "inventory_network_resold_targets" : null,
         "supply_type_action" : "exclude",
         "daypart_targets" : null,
         "daypart_timezone" : null,
         "postal_code_targets" : null,
         "querystring_boolean_operator" : "and",
         "last_activity" : "2015-03-30 21:25:41",
         "member_targets" : [
            {
               "action" : "include",
               "billing_name" : "unexposed",
               "id" : 4782,
               "third_party_auditor_id" : null
            }
         ],
         "browser_family_targets" : null,
         "screen_size_action" : "exclude",
         "min_session_imps" : null,
         "device_model_targets" : null,
         "querystring_action" : "exclude",
         "segment_group_targets" : null,
         "country_targets" : null,
         "city_action" : "exclude",
         "domain_list_action" : "exclude",
         "location_target_longitude" : null,
         "carrier_action" : "exclude",
         "position_targets" : null,
         "use_inventory_attribute_targets" : false,
         "device_type_action" : "exclude",
         "region_targets" : null,
         "browser_action" : "exclude"
      },
      "start_element" : null,
      "status" : "OK"
   }
}
```

## Related topic

[Bidder Profile - FAQ](./bidder-profile---faq.md)
