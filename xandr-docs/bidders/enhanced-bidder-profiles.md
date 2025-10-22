---
title: Enhanced Bidder Profiles
description: Enhance bidder profiles for targeted traffic. Xandr collaborates to tailor profiles, ensuring alignment with business requirements.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Enhanced Bidder profiles

Bidder profiles filter traffic and allow bidders to apply business rules on objects. This is to ensure specific types of traffic are either received or not received. Xandr will partner with you, and provide the proper tools to ensure you have a profile that matches your business needs.

## High-level changes

For an list of changes from legacy to the current enhanced bidder profiles, please visit the [changelog](changelog-for-enhanced-bidder-profiles.md).

- An impression only needs to meet the requirement of one of the profiles in order to pass.
  - There is no longer a parent/child hierarchy
  - For more information about the change in hierarchy, please see here: [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md).
- Ad type filtering and targeting have been added.
  - You will now be able to block/target native, banner, video, audio
  - For more information about ad type targeting, please see here: [Hierarchy and Ad Type Targeting for Enhanced Bidder  Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- Removal of passthrough percent.
  - You can now set QPS caps per DC.
  - For more information on how to set a QPS cap, please see here: [Bidder Instance Service](bidder-instance-service.md)
- Addition of Exchange targeting
  - We have grouped our inventory in easy-to-understand groups
  - For more information about exchanges, please see here: [Exchange Service](exchange-service.md)

## REST API

| HTTPS Method | Endpoint | Description |
|--|--|--|
| POST | `https://api.adnxs.com/bidder-profile/BIDDER_ID` | Add a new profile |
| PUT | `https://api.adnxs.com/bidder-profile/BIDDER_ID/PROFILE_ID` | Modify an existing profile |
| GET | `https://api.adnxs.com/bidder-profile/BIDDER_ID` | To see all of the profiles attached to your bidder |
| GET | `https://api.adnxs.com/bidder-profile/BIDDER_ID/PROFILE_ID` | To see a specific profile attached to your bidder |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the bidder profile. This is a read-only field. |
| `bidder_id` | int | The ID of the bidder. This is a read-only field. |
| `code` | string | The alternative identifier for the bidder profile, specific to the bidder. |
| `description` | string | Description of the bidder profile. |
| `active` | Boolean | Indicates whether the profile has been activated. If false, this profile does not affect traffic sent to the bidder. |
| `targeting` | object | The targeting rules for this bidder profile. For more details, see [Targeting](enhanced-bidder-profiles.md#targeting) below. |
| `user_not_in_segment_action` | enum | If set to `include`: Impressions for all users are sent to the bidder.<br>If set to `exclud`: Only impressions where the user exists in a segment owned by or shared with the bidder are sent. QPS restrictions will apply to this field. The bidder doesn't have to explicitly state the segment in the segment actions.<br>**Note**: This field will be deprecated in favor of the `unknown_users_action`. |
| `unknown_users_action` | enum | If set to `include`: Impressions for all users are sent to the bidder.<br>If set to `exclude`: Only impressions where the user has an in-house ID mapped in the Xandr cookie are sent. Mapping occurs when the bidder calls the setuid function. |
| `non_audited_url_action` | enum | If set to `exclude`, all inventory that has not been audited by Xandr will be excluded. Otherwise, all inventory will be included. |

## Targeting

The targeting object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `exchanges` | object | Exchanges and seller members included or excluded by this profile. For more details, see [Exchanges](enhanced-bidder-profiles.md#exchanges) below. |
| `countries` | object | Countries or regions included or excluded by this profile. For more details, see [Countries](enhanced-bidder-profiles.md#countries) below. |
| `domain_lists` | object | Domain lists included or excluded by this profile. For more details, see [Domain Lists](enhanced-bidder-profiles.md#domain-lists) below. |
| `ad_types` | object | Ad types (e.g., Banner, Video) included or excluded by this profile. For more details, see [Ad Types](enhanced-bidder-profiles.md#ad-types) below. |
| `supply_types` | object | Supply types (e.g., Desktop, Mobile App) included or excluded by this profile. For more details, see [Supply Types](enhanced-bidder-profiles.md#supply-types) below. |
| `inventory_attributes` | objects | Inventory attributes included or excluded by this profile. For more details, see [Inventory Attributes](enhanced-bidder-profiles.md#inventory-attributes) below. |

## Exchanges

The exchanges object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether the exchanges in the targets array (below) are included or excluded. | `include`, `exclude` |
| `targets` | array of objects | List of exchanges included or excluded by the profile.<br>Refer to the [Exchange Service](exchange-service.md) documentation for more information about exchanges. | `{"id": 1}`, `{"id": 2}`, `{"id": 3}` |
| `excluded_members` | array of objects | List of sellers that the bidder wants to exclude. Refer to the [Platform Member Service](platform-member-service.md) for a list of targetable members. | `{"id": 181}`, `{"id": 459}` |
| `included_members` | array of objects | List of sellers that the bidder wants to include.  Refer to the [Platform Member Service](platform-member-service.md) for a list of targetable members.<br>**Note**: Sellers that belong to Xandr's direct supply (Exchange 1) cannot be individually included. See the [Exchange Service](exchange-service.md) documentation for more information. | `{"id": 181}`, `{"id": 459}` |

## Countries

The countries object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether the countries or regions in the targets array (below) are included or excluded. | `include`, `exclude` |
| `targets` | array of objects | List of countries or regions included or excluded by the profile.. Refer to the [Country Service](country-service.md) for a list of targetable countries or regions. | `{"id": 233}`, `{"id": 80}` |

## Domain lists

The domain lists object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether the domain lists in the targets array (below) are in allowlists or blocklists. | `include`, `exclude` |
| `targets` | array of objects | List of domain lists included or excluded by the profile. The domain list type does not affect how targeting is applied; use action to configure allowlists or blocklists. Refer to the [Domain List Service](domain-list-service.md) for a list of targetable domain lists. | `{"id": 12345}`, `{"id": 34567}` |

## Ad types

The ad types object contains the following fields. For more information on Ad Types: [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `banner` | object | Indicates whether banner-eligible impressions are targeted. Specific ad sizes can be configured. If not explicitly configured, it is assumed to be included. For more details, see [Banner](enhanced-bidder-profiles.md#banner) below. | `{"id": 12345}`, `{"id": 34567}` |
| `video` | object | Indicates whether video-eligible impressions are targeted. If not explicitly configured, it is assumed to be included. For more details, see [Video](enhanced-bidder-profiles.md#video) below. |  |
| `native` | object | Indicates whether native-eligible impressions are targeted. If not explicitly configured, it is assumed to be included. For more details, see [Native](enhanced-bidder-profiles.md#native) below. |  |
| `audio` | object | Indicates whether audio-eligible impressions are targeted. If not explicitly configured, it is assumed to be included. For more details, see [Audio](enhanced-bidder-profiles.md#audio) below. |  |

### Banner

The banner object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether banner-eligible impressions are included or excluded. | `include`, `exclude` |
| `sizes` | array of objects | List of banner ad sizes included in targeting. Creative sizes cannot be excluded. | `{"width": 300, "height": 250}`, `{"width": 728, "height": 90}` |

### Video

The video object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether video-eligible impressions are included or excluded. | `include`, `exclude` |

### Native

The native object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether native-eligible impressions are included or excluded. | `include`, `exclude` |

### Audio

The audio object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether audio-eligible impressions are included or excluded. | `include`, `exclude` |

## Supply types

The supply types object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether the supply types in the targets array (below) are included or excluded. | `include`, `exclude` |
| `targets` | array of strings | List of supply types included or excluded by the profile. | `mobile_app`, `mobile_web`, `web` |

## Inventory attributes

The inventory attributes object contains the following fields.

| Field | Type | Description | Possible Values |
|--|--|--|--|
| `action` | enum | Indicates whether the inventory attributes in the targets array (below) are included. | `include` |
| `targets` | array of objects | List of inventory attributes included or excluded by the profile. Refer to the [Inventory Attribute Service](inventory-attribute-service.md) for a list of targetable inventory attributes.<br> Inventory without an assigned inventory attribute is always targeted. | `{"id": 2}`, `{"id": 16}` |

### Examples

Additional API examples are available here: [API Use Cases for Enhanced Bidder Profiles](api-use-cases-for-enhanced-bidder-profiles.md) Performing a GET call on the API:

 **Exchanges**

```
{
        "response": {
                "status": "OK",
                "count": 1,
                "start_element": 0,
                "num_elements": 100,
                "bidder_profiles": [{
                        "id": 00,
                        "bidder_id": 00,
                        "code": null,
                        "description": null,
                        "targeting": {
                                "exchanges": {
                                        "action": "include",
                                        "targets": [{
                                                "id": 1,
                                                "name": "Direct"
                                        }],
                                        "excluded_members": [{
                                                "id": 5,
                                                "billing_name": "Supply_source"
                                        }],
                                        "included_members": [{
                                                "id": 7,
                                                "billing_name": "Supply_source_two"
                                        }]
                                }
                        },
                        "last_activity": "2018-07-24 17:05:00",
                        "created_on": "2018-07-20 18:16:19",
                        "active": true
                }]
        }
}
```

 **Countries**

```
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 0,
                "code": "my_code",
                "description": "EMEA Profile",
                "targeting": {
                    "countries": {
                        "action": "include",
                        "targets": [
                            {
                                "id": 18,
                                "name": "Australia",
                                "code": "AU",
                                "active": true
                            },
                            {
                                "id": 41,
                                "name": "Canada",
                                "code": "CA",
                                "active": true
                            },
                            {
                                "id": 105,
                                "name": "Ireland",
                                "code": "IE",
                                "active": true
                            },
                            {
                                "id": 173,
                                "name": "New Zealand",
                                "code": "NZ",
                                "active": true
                            },
                            {
                                "id": 80,
                                "name": "United Kingdom",
                                "code": "GB",
                                "active": true
                            },
                            {
                                "id": 233,
                                "name": "United States",
                                "code": "US",
                                "active": true
                            }
                        ]
                    },
                "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                "user_not_in_segment_action": "include"
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

**Domain lists**

```
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 00,
                "code": null,
                "description": null,
                "targeting": {
                    "domain_lists": {
                        "action": "exclude",
                        "targets": [
                            {
                                "id": 140000,
                                "name": "Additional Block List",
                                "description": "Block list",
                                "type": "black"
                            },
                            {
                                "id": 800000,
                                "name": "Domain list (blocklist)",
                                "description": "Domain list (blocklist)",
                                "type": "black"
                            }
                        ]
                    },
                "last_activity": "2018-07-24 17:05:31",
                "created_on": "2018-07-20 18:21:00",
                "active": true
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

**Ad types**

```
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 000,
                "code": "Company_test",
                "description": "Company Parent Test",
                "targeting": {
                    "ad_types": {
                        "banner": {
                            "action": "include",
                            "sizes": [{
                                                                "width": 200,
                                                                "height": 200
                                                        },      {
                                                                "width": 50,
                                                                "height": 50
                            }]
                        },
                        "video": {
                            "action": "exclude"
                                                        "sizes": [{
                                                                "width": 200,
                                                                "height": 200
                                                        },      {
                                                                "width": 50,
                                                                "height": 50
                            }]
                        },                        },
                        "audio": {
                            "action": "exclude"
                        },
                        "native": {
                            "action": "include"
                        }
                    }
                },
                "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                        "non_audited_url_action": "include"           
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

 **Supply types**

```
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": 
[
            {
                "id": 00,
                "bidder_id": 000,
                "code": "my_code",
                "description": "Company Profile",
                "targeting": {
                    "supply_types": {
                        "action": "include",
                        "targets": [
                            "web",
                            "mobile_web",
                            "mobile_app"
                        ]
                    },
                        }
                    }
                },
                "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                "non_audited_url_action": "include"
            }
        ],

        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

**Inventory attributes**

```
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 00,
                "code": null,
                "description": null,
                "targeting": {
                    "inventory_attributes": {
                        "targets": [{
                            {
                                "id": 00,
                                "name": "Streaming Media",
                                "deleted": false
                            }]
                                        }
                                },
                                "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                        "non_audited_url_action": "include"           
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

**Unknown users action**

```
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 00,
                "code": null,
                "description": null,
                "targeting": {
                    "inventory_attributes": {
                        "targets": [{
                            {
                                "id": 00,
                                "name": "Streaming Media",
                                "deleted": false
                            }],
                                                        "action": "include"
                                        }
                                },
                                        "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                        "unknown_users_action": "include"           
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

**Non-audited URL action**

```
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "bidder_profiles": [
            {
                "id": 00,
                "bidder_id": 00,
                "code": null,
                "description": null,
                "targeting": {
                    "inventory_attributes": {
                        "targets": [{
                                "id": 00,
                                "name": "Streaming Media",
                                "deleted": false
                            }],
                                                        "action": "include"
                                        }
                                },
                                "last_activity": "2018-07-24 19:47:54",
                "created_on": "2018-07-24 19:47:49",
                "active": true,
                        "non_audited_url_action": "include"           
            }
        ],
        "dbg": {
            "warnings": [
            ],
            "version": "1.18.701",
            "output_term": "bidder_profiles"
        }
    }
}
```

## Related topics

- [Exchange Service](exchange-service.md)
- [Hierarchy and Ad Type Targeting for Enhanced Bidder Profiles](hierarchy-and-ad-type-targeting-for-enhanced-bidder-profiles.md)
- [API Use Cases for Enhanced Bidder Profiles](api-use-cases-for-enhanced-bidder-profiles.md)
- [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](frequently-asked-questions-faq-for-enhanced-bidder-profiles.md)
- [Changelog for Enhanced Bidder Profiles](changelog-for-enhanced-bidder-profiles.md)
- [Bidder Profile Migration Guide](bidder-profile-migration-guide.md)
