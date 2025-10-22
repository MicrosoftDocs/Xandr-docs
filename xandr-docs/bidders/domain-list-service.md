---
title: Bidders - Domain List Service
description: Explore customizing domain preferences, use a domain list service to create allowlists/blocklists, specify domains for or against user activities.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Domain list service

Domain lists can be used to create an allowlist or a blocklist of domains that should be included or excluded, respectively, from targeting. The domain list IDs are used with the [Enhanced Bidder Profiles](enhanced-bidder-profiles.md) to specify which domains should be included or excluded from targeting. Please be advised that specifying whether a domain list is an "allowlist" or a "blocklist" does not determine whether that list will be included or excluded. Rather, the domain_list_action must be specified in the [Enhanced Bidder Profiles](enhanced-bidder-profiles.md) as "include" for allowlists and "exclude" for blocklists.

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| GET | `https://api.adnxs.com/domain-list` | View all domain lists. |
| GET | `https://api.adnxs.com/domain-list?id=DOMAIN_LIST_ID` | View a specific domain list.<br>**Note**: The api use must have the field, "is_admin" set to true. |
| GET | `https://api.adnxs.com/domain-list/search=SEARCH_TERM` | Search for domain lists with names or descriptions containing certain characters. |
| POST | `https://api.adnxs.com/domain-list` | Add a new domain list. |
| PUT | `https://api.adnxs.com/domain-list/DOMAIN_LIST_ID` | Modify an existing domain list. |
| DELETE | `https://api.adnxs.com/domain-list/DOMAIN_LIST_ID` | Delete an existing domain list. |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `description` | string(100) | A description of the domain list as specified by the user. |
| `domains` | array or strings | The domains included in the domain list. See examples below for format.<br>**Note**: "www" is stripped from domains<br>Domains which begin with `"www"` will have the `"www"`substring stripped out before being stored in our system. For example, `"www.example.org"` will be shortened to `"example.org"`. |
| `id` | int | The internal ID for the domain list.<br> - **Required On**: PUT. |
| `last_modified` | timestamp | **Read-only**. The day and time when the domain list was last changed. |
| `name` | string(100) | The name of the domain list as specified by the user.<br> - **Required On**: POST. |
| `type` | string | The type of domain list. Possible values are `"black"` and `"white"`. This is strictly informational. The value here does not determine whether the list is included or excluded.<br> - **Default**: "white". |

> [!NOTE]
> Only the api user that creates a domain list can see and edit the contents of that domain list.

## Examples

**Add a domain list**

```
$ cat domain-list
{
   "domain-list" : {
      "type" : "black",
      "domains" : [
         "baddomain.com",
         "worsedomain.net",
         "worstdomain.org"
      ],
      "description" : "Rich's awesome domain list (blocklist)",
      "name" : "Rich's awesome domain list (blocklist)"
   }
}
$ curl -b cookies -c cookies -X POST --data-binary @domain-list 'https://api.adnxs.com/domain-list'
{
        "response":{
                "status":"OK",
                "count":1,
                "start_element":null,
                "num_elements":null,
                "id":9351,
                "domain-list":{
                        "id":9351,
                        "name":"Rich's awesome domain list (blocklist)",
                        "description":"Rich's awesome domain list (blocklist)",
                        "type":"black",
                        "last_modified":"2015-03-30 21:14:05",
                        "domains":["baddomain.com","worsedomain.net","worstdomain.org"]
                }
        }
}
```

**View a domain list**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/domain-list/9'
{
        "response":{
                domain-list":{
                "id":9,
                "name":"Domains to exclude",
                "description":"A list of the domains to target for the parent profile allowlist",
                "type":"black",
                "domains":[
                                "baddomain.com", 
                                "worsedomain.net", 
                                "worstdomain.org"
                        ]
        },
                "status":"OK"
        }
}
```

**Add a domain list to your bidder profile as a "blocklist"**

> [!NOTE]
> This example targets domain lists using the [Enhanced Bidder Profiles](enhanced-bidder-profiles.md).

```
$ cat domain-list-profile
{
   "bidder_profile" : {
                        "domain_lists" : {
                "action" : "exclude",
                                "targets" : [
                                {
                                                "id" : 918698,
                                                }
                                        ]
}}}
$ curl -b cookies -c cookies -X PUT --data-binary @domain-list-profile 'https://api.adnxs.com/bidder-profile/497/431739'
{
   "response" : {
      "profile" : {
         "last_activity" : "2015-03-30 21:25:41",
         "inv_class_targets" : null,
         "inventory_group_targets" : null,
         "session_freq_type" : "platform",
         "age_targets" : null,
         "dma_targets" : null,
         "language_targets" : null,
         "domain_targets" : null,
         "domain_list_targets" : [
            {
               "name" : "Rich's awesome domain list (blocklist)",
               "id" : 9351,
               "description" : "Rich's awesome domain list (blocklist)",
               "type" : "black",
               "deleted" : false
            }
         ],
         "country_targets" : null,
         "operating_system_family_targets" : null,
         "device_type_action" : "exclude",
         "querystring_action" : "exclude",
         "intended_audience_targets" : null,
         "description" : "Ethical Ad Blocker Test Segment",
         "position_targets" : null,
         "city_targets" : null,
         "device_model_targets" : null,
         "carrier_action" : "exclude",
         "device_type_targets" : null,
         "language_action" : "exclude",
         "non_audited_url_action" : "include",
         "location_target_radius" : null,
         "ip_targets" : null,
         "domain_list_action" : "exclude",
         "passthrough_percent" : 100,
         "segment_group_targets" : null,
         "size_targets" : [
            {
               "height" : 50,
               "width" : 300
            },
            {
               "width" : 300,
               "height" : 250
            }
         ],
         "browser_action" : "exclude",
         "city_action" : "exclude",
         "operating_system_extended_targets" : null,
         "browser_family_targets" : null,
         "querystring_targets" : null,
         "querystring_boolean_operator" : "and",
         "screen_size_action" : "exclude",
         "postal_code_targets" : null,
         "region_targets" : null,
         "segment_targets" : [
            {
               "expire_minutes" : null,
               "other_greater" : null,
               "other_less" : null,
               "other_in_list" : null,
               "action" : "include",
               "deleted" : false,
               "start_minutes" : null,
               "name" : "ethical ad blocker segment 00",
               "id" : 110944,
               "code" : "ethical-adblock-00",
               "other_equals" : null
            }
         ],
         "device_model_action" : "exclude",
         "inventory_source_targets" : null,
         "inventory_action" : "exclude",
         "country_action" : "exclude",
         "use_inventory_attribute_targets" : false,
         "segment_boolean_operator" : "or",
         "supply_type_targets" : null,
         "is_expired" : false,
         "carrier_targets" : null,
         "daypart_timezone" : null,
         "code" : "ethical-adblock-00",
         "inventory_attribute_targets" : null,
         "region_action" : "exclude",
         "site_targets" : null,
         "domain_action" : "exclude",
         "browser_targets" : null,
         "gender_targets" : null,
         "min_session_imps" : null,
         "dma_action" : "exclude",
         "venue_targets" : null,
         "id" : 431739,
         "member_targets" : [
            {
               "id" : 4782,
               "billing_name" : "unexposed",
               "action" : "include",
               "third_party_auditor_id" : null
            }
         ],
         "screen_size_targets" : null,
         "inventory_network_resold_targets" : null,
         "member_id" : null,
         "location_target_longitude" : null,
         "supply_type_action" : "exclude",
         "location_target_latitude" : null,
         "daypart_targets" : null,
         "operating_system_targets" : null
      },
      "id" : "431739",
      "num_elements" : null,
      "count" : 1,
      "start_element" : null,
      "status" : "OK"
   }
}
```

**Search for domain lists with names or descriptions containing "Test"**

```
$ curl -b cookies -c cookies "https://api.adnxs.com/domain-list/search=test"
{
        "response": {
                "status": "OK",
                "domain-lists": [
                {
                        "id": 1733,
                        "name": "Add Test",
                        "description": "",
                        "type": "white",
                        "domains": [
                                "amblergazette.com",
                                "facebook.com",
                                "google.com",
                                "zwire.com"
                        ],
                                "last_modified": "2011-03-10 18:03:07"
                        }
                ]
        }
        }
```

## Related topic

[Enhanced Bidder Profiles](enhanced-bidder-profiles.md)
