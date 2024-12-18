---
title: Config Service
description: In this article, learn about the Configuration service, their REST API, parameters, JSON requests, and responses with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Configuration service

Once inventory has been [Integrated with Prebid Server Premium (PSP)](../monetize/integrate-with-psp.md), [Cross-Partner Settings](../digital-platform-api/cross-partner-settings-service.md) have been reviewed, and [Demand partners](../digital-platform-api/demand-partner-service.md) have been enabled, inventory must be mapped to demand partners via PSP configurations. These mappings allow PSP to send bid requests with demand partners’ parameters so the partners can identify the inventory and better represent it to their buyers, increasing yield and honoring publisher settings such as floors and ad quality.

- Each configuration targets a portion of publisher inventory in Monetize, either by a set of flexible targeting (geography, inventory type, key value, etc.) or by explicitly specifying Monetize objects (placement, placement group, publisher)
- Each configuration includes one or more demand partners the publisher would like to bid on the inventory
- Each demand partner specifies the required and optional parameters they want to receive in their [open-source Prebid Server Go adapter](https://docs.prebid.org/dev-docs/pbs-bidders.html), which are surfaced in PSP. These allow the partner to match the bid request to objects in their platform
- Publishers fill out demand partner parameters with values mapped to objects in each partner’s platform, typically another supply-side platform (SSP)

## Demand partner requirements

All demand partners the publisher would like to bid on the inventory defined in a PSP configuration must be added to the same configuration. Before creating the first set of configurations, review requirements with each of the planned PSP demand partners to determine a mapping strategy. Some partners pull information dynamically from the bid request (ad size, geographic location, language, etc.) while others may require separate parameter mappings, and in turn, PSP configurations. If a demand partner requires very granular mapping to objects in their platform, that will determine how other partners are mapped and how many configurations are required. The better a demand partner can identify the inventory (either through the bid request or static Prebid parameters), the more information they can provide to their buyers, increasing publisher revenue.

Demand partner parameters can be found:

- In the PSP configuration UI, as detailed below
- On the Prebid site with full context and details
- In the PSP demand partner schema service

The documentation below describes how to create and manage configurations via API. Configurations can also be managed [through the UI](../monetize/add-edit-or-delete-a-psp-configuration.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/prebid/config](https://api.appnexus.com/prebid/config) | Return all of the Prebid configurations. |
| `GET` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Return specific Prebid configurations. |
| `POST` | [https://api.appnexus.com/prebid/config](https://api.appnexus.com/prebid/config) | Add a new Prebid configuration. |
| `PUT` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Update an existing Prebid configuration. |
| `PATCH` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Update a portion of the existing Prebid configurations. |
| `DELETE` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Delete an existing Prebid configuration. |

### GET

Returns all Prebid configurations for the caller's member. Results are returned as JSON.

#### Parameters

| Property | Scope | Type | Description |
|:---|:---|:---|:---|
| `status_filter` | string | Optional | Filter results based on whether a configuration is enabled or disabled. Pass the `status_filter` argument in the query and set the value to either *enabled* or *disabled*. |

#### Example call using curl with status filter arguments

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/config?status_filter=enabled
```

#### Example call using curl to return a specific configuration

Append the configuration ID as the last component of the URL.

```
curl --header "Content-Type: application/json"https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

#### Responses

A successful response will return JSON containing the member's cross-partner settings and all of their PSP configurations. Including a specific `prebidSettingsId` in the query string will lead to a response containing only that configuration.

| Property | Type | Description |
|:---|:---|:---|
| `bidder_timeout_ms` | integer | This is defined in the [cross-partner-settings service](cross-partner-settings-service.md). |
| `configs` | array | Container with the configs objects for the member or a specific configuration object. For items contained in a configuration object, see the [configuration properties](#config-properties) table below. |
| `deleted` | boolean | If `true`, indicates that the config object is not available for use but its data is still viewable. |
| `demand_partner_settings` | array | The demand partner properties. For the items contained in the `demand_partner_settings` object, see the [demand partner settings](#demand-partner-settings) table below. |
| `id` | integer |  - When the request does not specify a `prebidSettingsId`, the first ID in the response represents the unique [cross-partner settings ID](cross-partner-settings-service.md) for the member. The [configs object](#config-properties) includes the id values of each configuration. <br> - When the request specifies a `prebidSettingsId`, that will be the unique identifier in the response. This id is referred to as prebid_settings_id in other endpoints of this API. |
| `last_modified` | string | The most recent modification date of the configuration object. |
| `last_modified_by` | string | The user who made the last modification to the configuration object. |
| `member_id` | integer | The ID of the member associated with the configurations. |
| `price_granularity` | object | Defines the CPM price buckets into which demand partner bids will be grouped in the ad server. See the [price granularity](#price-granularity) table below. Object is managed via the [cross-partner-settings service](cross-partner-settings-service.md).|
| `total_configs` | integer | The number of configurations returned. |

### Demand partner settings

| Property | Type | Description |
|:---|:---|:---|
| `bid_cpm_adjustment` | float | A multiplier value applied to the Demand Partner's CPM bid price to adjust how the bids compete in the auction. See the [Demand Partner Service](demand-partner-service.md) for more information. |
| `enabled` | boolean | Indicates if the demand partner has been enabled or disabled. |
| `id` | integer | The id for the demand partner settings. |
| `name` | string | The name of the demand partner. See the [Demand Partner Service](demand-partner-service.md) for more information.|

### Config properties

| Property | Type | Description |
|:---|:---|:---|
| `deleted` | boolean | If `true`, indicates that the configuration object is not available for use but its data is still viewable. |
| `demand_partner_config_params` | array | A container with the demand partner's adapter parameters and the values they will receive in bid requests from PSP. For items contained in the `demand_partner_config_params` object, see the [demand partner configs properties](#demand-partner-configs-properties) table below. |
| `enabled` | boolean | Indicates if the configuration is enabled or disabled. |
| `id` | integer | This ID is referred to as `prebid_settings_id` in other endpoints of the API.|
| `last_modified` | string | The most recent modification date of the configuration. Formatted as date-time. |
| `last_modified_by` | string | The user who made the last modification to the configuration object.|
| `media_types` | object | The media types associated with the configurations. For items contained in a media_types object, see the [media types](#media-types) properties table below. |
| `member_id` | integer | The ID of the member associated with the configurations.|
| `name` | string | The name of the configuration. |
| `targeting_level_code` | integer | The type of object associated with the configuration: <br> - `1` placement  <br> - `2` placement group/site <br> - `3` publisher <br> - `4` line item/targeting profile|
| `targeting_id` | integer | The identifier of the object with which the configuration is associated (e.g., line item, placement, placement group, publisher). Requests will be sent to demand partners when the bid request specifies the same object or matches the targeting of the line item/profile. If a line item ID is used, it must be a "psp" subtype line item attached to a profile. When creating configurations in the [PSP UI](../monetize/add-edit-or-delete-a-psp-configuration.md), these objects are created and linked automatically.|
| `targeting_level_name` | string | The name of the level (example: publisher). |
| `targeting_metadata` | object | Includes modifiers for the targeting object. See the [Targeting Metadata Properties](#targeting-metadata-properties) table for items contained in the `targeting_metadata` object. **When the `targeting_id` is a line item ID, `targeting_metadata.priority` is required.** |

### Media types

The media type object determines which formats (currently banner, native, and video) and ad sizes are included in the requests to demand partners.

| Property | Type | Description |
|:---|:---|:---|
| `sizes` | object | Demand Partners will only receive requests for this configuration where these ad sizes are present. |
| `sizes.width` | integer | Width of the unit. For Example, 300. |
| `sizes.height` | integer | Height of the unit. For Example, 250. |
| `sizes.is_standard` | boolean | Denotes whether the size has been defined as standard by the member. |
| `types` | array | Includes the media type(s) eligible for the configuration. Only these types will be passed to demand partners in requests. Values are banner, native, video. |

### Targeting metadata properties

| Property | Type | Description |
|:---|:---|:---|
| `os_family_ids` | array | Demand Partners will only receive requests for this configuration where these operating systems are present. Operating systems represented by integer ids from the [Operating System-Families Service](operating-system-families-service.md). |
| `priority` | integer | The rank of the configuration is used only when it is tied to a line item. This rank instructs Monetize which configuration to use when the targeting of multiple line items is eligible for the same bid request. The scale ranges from 1 to 20, with 20 being the highest. **This ranking is required when the `targeting_id` is a line item ID** and does not apply to placement, placement group, or publisher configurations. When multiple line item configurations have the same priority, the configuration with the higher (more recent) ID will be used in the auction. |

### Demand partner configs properties

| Property | Type | Description |
|:---|:---|:---|
| `deleted` | boolean | If `true`, indicates that the configuration object is not available for use but its data is still viewable. |
| `enabled` | boolean | Indicates if the Demand Partner has been enabled or disabled. For more information, see the [Demand Partner Service](demand-partner-service.md). |
| `id` | integer | The id of the parameter mappings for the specific demand partner. |
| `last_modified` | string | The most recent modification date of the `demand_partner_config`. |
| `last_modified_by` | string | The person who made the last modifications to the `demand_partner_config`. |
| `member_id` | integer | The member_id associated with the `demand_partner_config`. |
| `name` | string | The [Prebid bidder name](../monetize/prebid-server-premium-demand-partner-integrations.md) for the Demand Partner. |
| `params` | object | The partner-specific parameters and mapped values. For more information, see the [Demand Partner Params Service](prebid-demand-partner-params-service.md). |
| `prebid_settings_id` | integer | The ID of the configuration which can contain multiple demand partner parameter mappings. |

### Price granularity

Price granularity defines the CPM price buckets into which demand partner bids will be grouped in the ad server. This is defined in the [Cross-Partner Settings Service](cross-partner-settings-service.md).

| Property | Type | Description |
|:---|:---|:---|
| `currency_code` | string | A string containing the desired currency code for price bucket calculations. It must be part of the [Microsoft-approved list of currencies](../monetize/currency-support.md). |
| `label` | string | The type of scale as defined in [Prebid documentation](https://docs.prebid.org/adops/price-granularity.html) (low, medium, high, auto, dense, custom). See the [cross-partner-settings service](cross-partner-settings-service.md).|
| `precision` | integer | The number of decimal places to which the price is rounded. The default is two decimal places, so a price of 2.1234 would be rounded to 2.12. |
| `ranges` | object | Container object describing the price granularity range. |
| `ranges.max` | integer | The maximum length of the range. |
| `ranges.increment` | float | The amount to increment through the range. |

### Pagination

The number of responses can be limited by passing the `num_elements` argument. Which element to start viewing can be set through the `start_element` argument.

| Property | Type | Description |
|:---|:---|:---|
| `num_elements` | int | How many elements to return. For example, start at object # 4 and return 3 objects, or # 4, 5, 6. |
| `start_element` | int | The number at which to start counting. |

#### Example call to limit to fifteen results and to start the results at the tenth element

The elements returned will be indexed from the 10th through the twenty-fifth.

```
GET https://api.appnexus.com/prebid/config?num_element=15&start_element=10
```

#### Example response

```

{
  "id": 450,
  "member_id": 13859,
  "bidder_timeout_ms": 500,
  "price_granularity": {
    "label": "Auto",
    "currency_code": "USD",
    "precision": 2,
    "ranges": [
      {
        "max": 5,
        "increment": 0.05
      },
      {
        "max": 10,
        "increment": 0.1
      },
      {
        "max": 20,
        "increment": 0.5
      }
    ]
  },
  "deleted": 0,
  "last_modified_by": "user123",
  "last_modified": "2024-08-21T16:37:24.000Z",
  "demand_partner_settings": {
    "appnexus": {
      "id": 2045,
      "bid_cpm_adjustment": 0.7,
      "enabled": 1
    },
    "openx": {
      "id": 2065,
      "bid_cpm_adjustment": 1,
      "enabled": 0
    },
    "ix": {
      "id": 2106,
      "bid_cpm_adjustment": 0.9,
      "enabled": 1
    },
    "adform": {
      "id": 2110,
      "bid_cpm_adjustment": 1,
      "enabled": 1
    }
  },
  "total_configs": 2,
  "configs": [
    {
      "id": 87053,
      "member_id": 13859,
      "name": "ConfigName1",
      "targeting_level_code": 1,
      "targeting_id": 25172737,
      "enabled": 1,
      "media_types": {
        "sizes": [],
        "types": [
          "video"
        ]
      },
      "targeting_metadata": {
        "os_family_ids": []
      },
      "deleted": 0,
      "last_modified_by": "user123",
      "last_modified": "2024-07-17T18:17:56.000Z",
      "targeting_level_name": "placement",
      "demand_partner_config_params": [
        {
          "id": 619584,
          "member_id": 13859,
          "prebid_settings_id": 87053,
          "name": "ix",
          "params": {
            "size": null,
            "siteId": "yyy.com"
          },
          "enabled": 1,
          "deleted": 0,
          "last_modified_by": "user123",
          "last_modified": "2024-07-17T18:36:40.000Z"
        }
      ]
    },
    {
      "id": 87784,
      "member_id": 13859,
      "name": "ConfigName2",
      "targeting_level_code": 1,
      "targeting_id": 25175861,
      "enabled": 1,
      "media_types": {
        "sizes": [],
        "types": [
          "banner",
          "video",
          "native"
        ]
      },
      "targeting_metadata": {
        "os_family_ids": []
      },
      "deleted": 0,
      "last_modified_by": "user123",
      "last_modified": "2024-07-31T21:34:34.000Z",
      "targeting_level_name": "placement",
      "demand_partner_config_params": [
        {
          "id": 619080,
          "member_id": 13859,
          "prebid_settings_id": 87784,
          "name": "openx",
          "params": {
            "unit": "3456",
            "platform": null,
            "delDomain": "abc.com",
            "customFloor": null,
            "customParams": null
          },
          "enabled": 0,
          "deleted": 0,
          "last_modified_by": "user123",
          "last_modified": "2024-08-21T21:10:28.000Z"
        },
        {
          "id": 619081,
          "member_id": 13859,
          "prebid_settings_id": 87784,
          "name": "ix",
          "params": {
            "size": null,
            "siteId": "abc.com"
          },
          "enabled": 1,
          "deleted": 0,
          "last_modified_by": "user123",
          "last_modified": "2024-07-17T18:36:06.000Z"
        },
        {
          "id": 625915,
          "member_id": 13859,
          "prebid_settings_id": 87784,
          "name": "adform",
          "params": {
            "inv": null,
            "mid": "1414158",
            "mname": null,
            "priceType": null
          },
          "enabled": 1,
          "deleted": 0,
          "last_modified_by": "user123",
          "last_modified": "2024-07-17T18:36:09.000Z"
        }
      ]
    }
  ]
}

       
```

### POST

Enables the creation of a new configurations object.

#### Example call using curl

```
curl -d @config.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/config'
```

#### POST: Parameters

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `demand_partner_config_params` | array | Required | A container with the demand partner's adapter parameters and the values they will receive in bid requests from PSP. For items contained in the `demand_partner_config_params` object, see the [demand partner configs properties](#post-demand-partner-configs-properties) table below.|
| `enabled` | boolean | Required | Indicates whether the configuration is enabled or disabled. |
| `media_types` | object | Required | The media_types associated with the configuration. For items contained in a `media_type` object, see the [media type](#post-media-types) properties table below. |
| `name` | string | Required | The name of the configuration. |
| `targeting_id` | integer | Required | The identifier of the object with which the configuration is associated (e.g., line item, placement, placement group, publisher). Requests will be sent to demand partners when the bid request specifies the same object or matches the targeting of the line item/profile. If a line item ID is used, it must be a "psp" subtype line item attached to a profile. When creating configurations [in the PSP UI](../monetize/add-edit-or-delete-a-psp-configuration.md), these objects are created and linked automatically. |
| `targeting_level_code` | integer | Required | The type of object associated with the configuration: <br> - `1` placement <br> - `2` placement group/site <br> - `3` publisher <br> - `4` line item/targeting profile |
| `targeting_metadata` | object | Optional | Includes modifiers for the targeting object. See the [Targeting Metadata Properties](#post-targeting-metadata-properties) table for items contained in the targeting_metadata object. **When the `targeting_id` is a line item ID, `targeting_metadata.priority` is required**. |

#### POST: Demand partner configs properties

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The [Prebid bidder name](../monetize/prebid-server-premium-demand-partner-integrations.md) for the Demand Partner. |
| `params` | object | Required | The partner-specific parameters and mapped values. For more information, see the [Demand Partner Params Service](prebid-demand-partner-params-service.md). |

#### POST: Media types

The media type object determines which formats (currently banner, native, and video) and ad sizes are included in the requests to demand partners.

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `sizes` | object | Optional | Demand Partners will only receive requests for this configuration where these ad sizes are present. |
| `sizes.width` | integer | Optional | Width of the unit. For Example, 300. |
| `sizes.height` | integer | Optional | Height of the unit. For Example, 250. |
| `sizes.is_standard` | boolean | Optional | Denotes whether the size has been defined as standard by the member. |
| `types` | array | Required | Includes the media type(s) eligible for the configuration. Only these types will be passed to demand partners in requests. Values are banner, native, video. |

#### POST: Targeting metadata properties

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `os_family_ids` | array | Optional | Demand Partners will only receive requests for this configuration where these operating systems are present. Operating systems represented by integer ids from the [Operating System-Families Service](operating-system-families-service.md). |
| `priority` | integer | Optional | The rank of the configuration is used only when it is tied to a line item. This rank instructs Monetize which configuration to use when the targeting of multiple line items is eligible for the same bid request. The scale ranges from 1 to 20, with 20 being the highest. **This ranking is required when the targeting_id is a line item ID** and does not apply to placement, placement group, or publisher configurations. When multiple line item configurations have the same priority, the configuration with the higher (more recent) ID will be used in the auction. |

#### Example JSON request

```
{
    "name": "ConfigName1",
    "targeting_level_code": 4,
    "targeting_id": 25401118,
    "enabled": true,
    "media_types": {
        "sizes": [
            {
                "height": 300,
                "width": 250
            }
        ],
        "types": [
            "banner",
            "video",
            "native"
        ]
    },
    "targeting_metadata": {
        "priority": 20
    },
    "demand_partner_config_params": [
        {
            "name": "appnexus",
            "params": {
                "placement_id": 123456
            }
        }
    ]
}           
            
```

#### Response

A successful response will return the new configuration object.

#### POST: Example JSON response

```
[
  {
    "id": 196038,
    "member_id": 13859,
    "name": "ConfigName1",
    "targeting_level_code": 4,
    "targeting_id": 22378872,
    "enabled": 1,
    "media_types": {
      "sizes": [
        {
          "height": 300,
          "width": 250
        }
      ],
      "types": [
        "banner",
        "native",
        "video"
      ]
    },
    "targeting_metadata": {
      "priority": 20
    },
    "deleted": 0,
    "last_modified_by": "user123",
    "last_modified": "2024-08-22T21:24:40.000Z",
    "demand_partner_config_params": [
      {
        "id": 1718542,
        "member_id": 13859,
        "prebid_settings_id": 196038,
        "name": "appnexus",
        "params": {
          "placement_id": 123456
        },
        "enabled": 1,
        "deleted": 0,
        "last_modified_by": "user123",
        "last_modified": "2024-08-22T21:24:40.000Z"
      }
    ]
  }
]          
                
```

### PUT

Overwrite an existing Prebid configuration. Include the `prebidSettingsId` as the last component of the URL path. Pass the update information as JSON in the body of the request.

#### PUT: Example call using curl

```
curl -d @config-update.json -X PUT --header "Content-Type: application/json https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

#### PUT: Example JSON request

```
{
    "name": "ConfigName1",
    "targeting_level_code": 4,
    "targeting_id": 22378872,
    "enabled": 0,
    "media_types": {
        "sizes": [
            {
                "height": 300,
                "width": 250
            }
        ],
        "types": [
            "banner",
            "native",
            "video"
        ]
    },
    "targeting_metadata": {
        "priority": 20
    },
    "demand_partner_config_params": [
        {
            "id": 1718542,
            "member_id": 13859,
            "prebid_settings_id": 196038,
            "name": "appnexus",
            "params": {
                "placement_id": 123456
            },
            "enabled": 1
        }
    ]
}
```

#### PUT: Response

Returns a Prebid configuration object.

### PATCH

Partially update an existing Prebid configuration. Include the `prebidSettingsId` as the last component of the path. Pass the update information as JSON in the body of the request. The request must include a top-level `config` object that contains the other elements to be updated.

#### PATCH: Example call using curl

```
curl -d @config-update.json -X PATCH --header "Content-Type: application/json https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

#### PATCH: Example JSON request

```
{
    "config": {
        "enabled": 0,
        "media_types": {
            "types": [
                "banner"
            ]
        }
    }
}
```

#### PATCH: Response

Returns a Prebid configuration object.

### DELETE

Delete an existing Prebid configuration. Include the `prebidSettingsId` as the last component of the path.

#### DELETE: Example call using curl

```
curl -X DELETE https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

#### DELETE: Response

On success, the configuration indicated will be returned as a JSON object with the deleted property set to `true`. It will no longer be available within the system. All sub-objects will also be deleted.

## Related topics

- [PSP Campaign Objects Service](https://microsoftapc.sharepoint.com/teams/TechComm/SitePages/Prebid-Server-Premium-(PSP)---Flexible-Configurations---PSP-campaign-objects-service.aspx?ga=1)
- [Demand Partner Schema Service](demand-partner-schema-service.md)
- [Demand Partner Service](demand-partner-service.md)
- [Prebid Demand Partner Params Service](prebid-demand-partner-params-service.md)
- [Ad Sizes Service](ad-sizes-service.md)
- [Media Type Service](media-type-service.md)
- [Cross-Partner Settings Service](../digital-platform-api/cross-partner-settings-service.md)
- [Create a New PSP Configuration](../monetize/create-a-psp-configuration.md)
- [Prebid Server Premium Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md)
- [Common Issues and Best Practices](../monetize/psp-common-issues-and-best-practices.md)
