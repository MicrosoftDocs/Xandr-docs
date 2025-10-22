---
title: IP Range List Service
description: Explore the IP Range List service, designed for managing lists of IP ranges utilized for targeting by the profile service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# IP Range List service

The IP Range List Service is used to manage lists of IP ranges that can be used for targeting by the [Profile Service](profile-service.md). The functionality provided by this service is similar to the [Domain List Service](domain-list-service.md).

## Intended use case

The intended use case for this service is for mobile buyers who would like to serve ads to users where direct client billing is enabled, i.e., purchases are charged to the carrier and added to the mobile bill. In this scenario, campaigns target the IP ranges of gateways for cell towers that allow direct carrier billing.

To actually target the IP range lists you create and manage here, add them to the `ip_range_list_targets` field in the [Profile Service](profile-service.md).

> [!NOTE]
> **Not Designed for Blocking Inventory (Blocklists)**
>
> This service isn't designed for blocking IPs (like blocklists). For more details, see the [Limitations](#limitations) below.

## Limitations

The following limitations exist for the IP Range List Service:

- You can create up to 100 IP range lists.
- A single `"include"` IP range list (`include` set to `true`) cannot contain more than 3500 ranges.
- A single `"exclude"` IP range list (`include` set to `false`) cannot contain more than 10 ranges.

In addition, the following limitations exist on the [Profile Service](profile-service.md) when targeting IP Range Lists:

Per profile, you can target up to 10 `"include"` IP range lists (`include` set to `true`) and no more than 1 `"exclude"` IP range list (`include` set to `false`). The excluded IP ranges must be a subset of the included IP ranges.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/ip-range-list](https://api.appnexus.com/ip-range-list) | View all of your IP range lists. |
| `GET` | [https://api.appnexus.com/ip-range-list?id=LIST_ID](https://api.appnexus.com/ip-range-list?id=LIST_ID) | View a specific IP range list. |
| `GET` | [https://api.appnexus.com/ip-range-list/meta](https://api.appnexus.com/ip-range-list/meta) | Find out which fields you can filter and sort by. |
| `POST` | [https://api.appnexus.com/ip-range-list](https://api.appnexus.com/ip-range-list) | Add a new IP range list. |
| `PUT` | [https://api.appnexus.com/ip-range-list?id=LIST_ID](https://api.appnexus.com/ip-range-list?id=LIST_ID) | Modify an existing IP range list. |
| `DELETE` | [https://api.appnexus.com/ip-range-list?id=LIST_ID](https://api.appnexus.com/ip-range-list?id=LIST_ID) | Delete an IP range list. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `description` | string | An optional description of this IP range list.<br>**Default:** `null` |
| `id` | int | The unique ID of this IP range list.<br>**Required On:** `PUT` |
| `include` | boolean | Whether to include the IP ranges in this list in campaign targeting using the [Profile Service](profile-service.md).<br>**Default:** `false` |
| `ip_ranges` | array of objects | This array holds ranges of IP addresses. For details on the object fields, see the [IP Ranges](#ip-ranges) table below.<br>**Required On:** `POST` and `PUT` |
| `last_modified` | date | When this object was last updated.<br>**Read Only.** |
| `name` | string | The name of the IP range list.<br>**Required On:** `POST` and `PUT` |
| `num_ip_ranges` | int | The current number of IP ranges in this list.<br>**Read Only.** |

### IP ranges

Each object in the `ip_ranges` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `from_ip` | string | The starting IP address. If no following `to_ip` field is included, this is treated as the only address to include or exclude. This string must be in valid IPV4 address format, i.e., `"198.2.1.1"`.<br>**Required On:** `POST`, `PUT` |
| `to_ip` | string | The (optional) ending IP address. If this field is not included, the IP address in the `from_ip` field will be used alone. If this field is included, the addresses between the fields form a range. Ranges must be listed in **ascending** order, e.g., `{"from_ip":"192.168.2.1",`<br> `"to_ip":"192.168.2.100"}`. |

## Examples

### View an IP range list

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/ip-range-list?id=2'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "ip-range-list": {
            "id": 2,
            "name": "Sky IPs 1",
            "description": "Targeted Sky IP Addresses",
            "include": true,
            "last_modified": "2014-02-19 15:04:36",
            "ip_ranges": [
        {
            "from_ip": "2.120.0.0",
                    "to_ip": "2.120.0.0"
            },
            {
                "from_ip": "2.216.0.0",
                    "to_ip": "2.216.0.0"
            },
                {
                    "from_ip": "5.64.0.0",
                    "to_ip": "5.64.0.0"
            },
                {
                    "from_ip": "90.192.0.0",
                    "to_ip": "90.192.0.0"
            },
                {
                    "from_ip": "94.0.0.0",
                    "to_ip": "94.0.0.0"
                },
                {
                    "from_ip": "151.224.0.0",
                    "to_ip": "151.224.0.0"
                },
                {
                    "from_ip": "176.24.0.0",
                    "to_ip": "176.24.0.0"
                },
                {
                    "from_ip": "176.248.0.0",
                    "to_ip": "176.248.0.0"
                }
            ],
            "num_ip_ranges": 8
    }
}
```

### Create an IP range list

```
$ cat ip-range-list.json

{
    "ip-range-list": {
        "ip_ranges": [
            {
                "to_ip": "168.100.1.105",
                "from_ip": "168.100.1.100"
            },
            {
                "from_ip": "168.109.109.100"
            }
        ],
        "include": true,
        "description": "Yet another nice little IP range list for testing.",
        "name": "Rich's Second Ever IP range list"
    }
}
 
$ curl -b cookies -X POST -d @ip-range-list.json 'https://api.appnexus.com/ip-range-list'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 3,
        "start_element": 0,
        "num_elements": 100,
        "ip-range-list": {
            "id": 3,
            "name": "Rich's Second Ever IP range list",
            "description": "Yet another nice little IP range list for testing.",
            "include": true,
            "last_modified": "2014-02-25 20:21:12",
            "ip_ranges": [
            {
                    "from_ip": "168.100.1.100",
                    "to_ip": "168.100.1.105"
            },
            {
                    "from_ip": "168.109.109.100",
                    "to_ip": "168.109.109.100"
            }
            ],
            "num_ip_ranges": 2
        }
    }
}
```

### Update an IP range list

```
$ cat update-ip-range-list.json

{
    "ip-range-list": {
        "ip_ranges": [
            {
                "to_ip": "168.100.1.105",
                "from_ip": "168.100.1.100"
            },
            {
                "to_ip": "192.168.1.100",
                "from_ip": "192.168.1.1"
            },
            {
                "from_ip": "168.109.109.100"
            }
        ]
}
 
$ curl -b cookies -X PUT -d @update-ip-range-list.json 'https://api.appnexus.com/ip-range-list?id=3'
 
{
  "response": 
    "status": "OK",
    "count": 1,
    "id": "3",
    "start_element": 0,
    "num_elements": 100,
    "ip-range-list": {
      "id": 3,
      "name": "Rich's First IP range list, now with updates!",
      "description": "Just a nice little IP range list for testing. Recently updated.",
      "include": true,
      "last_modified": "2014-12-10 18:49:00",
      "ip_ranges": [
        {
          "from_ip": "168.100.1.100",
          "to_ip": "168.100.1.105"
        },
        {
          "from_ip": "168.109.109.100",
          "to_ip": "168.109.109.100"
        },
        {
          "from_ip": "192.168.1.1",
          "to_ip": "192.168.1.100"
        }
      ],
      "num_ip_ranges": 3
    }
  }
}
```

### Add an IP range list to your profile

```
$ cat profile-update.json
 
{
    "profile": {
        "ip_range_list_targets": [
            {
                "id":5
            }
        ]
    }
}
 
$ curl -b cookies -X PUT -d @profile-update.json 'https://api.appnexus.com/profile?id=294641&advertiser_id=41884'
 
{
    "response":{
         "num_elements":100,
         "start_element":0,
         "id":"294641",
         "count":1,
         "status":"OK"
         "profile":{
             "exelate_targets":null,
             "segment_targets":null,
             "publisher_targets":null,
             "platform_publisher_targets":null,
             "platform_placement_targets":null,
             "platform_content_category_targets":null,
             "placement_targets":null,
             "deal_targets":null,
             "content_category_targets":null,
             "mobile_app_instance_list_targets":null,
             "mobile_app_instance_targets":null,
             "ip_range_list_targets": [
                {
                    "id": 5
                    "include": false,
                    "description": "Test IP range list",
                    "name": "Test IP range list",
                }
            ],
             "operating_system_extended_targets":null,
             "venue_targets":null,
             "site_targets":null,
             "position_targets":null,
             "operating_system_family_targets":null,
             "operating_system_targets":null,
             "ip_targets":null,
             "inventory_network_resold_targets":null,
             "inventory_group_targets":null,
             "intended_audience_targets":null,
             "gender_targets":null,
             "querystring_targets":null,
             "device_model_targets":null,
             "screen_size_targets":null,
             "device_type_targets":null,
             "supply_type_targets":null,
             "carrier_targets":null,
             "segment_group_targets":null,
             "member_targets":null,
             "postal_code_targets":null,
             "size_targets":null,
             "language_targets":null,
             "domain_list_targets":null,
             "domain_targets":null,
             "dma_targets":null,
             "browser_family_targets":null,
             "browser_targets":null,
             "daypart_targets":null,
             "age_targets":null,
             "inventory_attribute_targets":null,
             "inventory_source_targets":null,
             "inv_class_targets":null,
             "city_targets":null,
             "region_targets":null,
             "country_targets":null,
             "user_group_targets":null,
             "mobile_app_instance_list_action_include":false,
             "mobile_app_instance_action_include":false,
             "use_operating_system_extended_targeting":false,
             "operating_system_family_action":"exclude",
             "created_on":"2013-09-16 17:22:30",
             "is_template":false,
             "allow_unaudited":false,
             "trust":"seller",
             "require_cookie_for_freq_cap":true,
             "operating_system_action":"exclude",
             "venue_action":"exclude",
             "min_minutes_per_imp":null,
             "max_page_imps":null,
             "max_lifetime_imps":null,
             "max_day_imps":null,
             "max_session_imps":null,
             "publisher_id":null,
             "advertiser_id":41884,
             "daypart_bitmap":null,
             "non_audited_url_action":"include",
             "is_expired":false,
             "querystring_boolean_operator":"and",
             "querystring_action":"exclude",
             "location_target_longitude":null,
             "location_target_latitude":null,
             "location_target_radius":null,
             "device_model_action":"exclude",
             "screen_size_action":"exclude",
             "device_type_action":"exclude",
             "supply_type_action":"exclude",
             "carrier_action":"exclude",
             "session_freq_type":"platform",
             "min_session_imps":null,
             "segment_boolean_operator":"and",
             "language_action":"exclude",
             "inventory_action":"exclude",
             "domain_list_action":"exclude",
             "domain_action":"exclude",
             "dma_action":"exclude",
             "daypart_timezone":null,
             "last_modified":"2014-02-05 19:52:32",
             "use_inventory_attribute_targets":false,
             "browser_action":"exclude",
             "city_action":"exclude",
             "region_action":"exclude",
             "country_action":"exclude",
             "description":null,
             "code":null,
             "id":294641
        }
    }
}
```

## Related topics

- [Profile Service](profile-service.md)
- [API Semantics](api-semantics.md)
- [API Best Practices](api-best-practices.md)
