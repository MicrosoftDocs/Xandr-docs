---
title: Config Service
description: In this article, learn about the Config service, their REST API, parameters, JSON requests, and responses with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Config service

The Config Service enables the retrieval, creation, and editing of Prebid Server Premium (PSP) configurations. PSP configurations are objects used to facilitate PSP spend on a particular Xandr Targeting Object (placement, placement group, publisher). Each config has an array of demand partner parameters attached to it, as a way to indicate which of the external PSP demand partners should facilitate spend for that config.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/prebid/config](https://api.appnexus.com/prebid/config) | Return all of the Prebid configs. |
| `GET` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Return a specific Prebid config. |
| `POST` | [https://api.appnexus.com/prebid/config](https://api.appnexus.com/prebid/config) | Add a new Prebid config. |
| `PUT` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Update an existing Prebid config. |
| `PATCH` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Update a portion of an existing Prebid config. |
| `DELETE` | [https://api.appnexus.com/prebid/config/{prebidSettingsId}](https://api.appnexus.com/prebid/config/{prebidSettingsId}) | Delete an existing Prebid config. |

## `GET`

Returns all Prebid configurations for the caller's member. Results are returned as JSON.

### Parameters

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `status_filter` | string | Optional | Filter results based on whether a config is enabled or disabled. Pass the `status_filter` argument in the query and set the value to either *enabled* or *disabled*. |

### Example call using curl with status filter arguments

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/config?status_filter=enabled
```

### Example call using curl to return a specific config

Append the config id as the last component of the URL.

```
curl --header "Content-Type: application/json"https://api.appnexus.com/prebid/config/{id}
```

### Responses

A successful response will return JSON containing all the Prebid configs for the member or the requested Prebid config.

| Property | Type | Description |
|:---|:---|:---|
| `bidder_timeout_ms` | integer | The timeout in milliseconds. |
| `configs` | array | Container with the configs objects for the member or a specific config object. For items contained in a config object, see the [config properties](#config-properties) table below. |
| `deleted` | boolean | If `true`, indicates that the config object is not available for use but its data is still viewable. |
| `demand_partner_settings` | array | The demand partner properties. For the items contained in the `demand_partner_settings` object, see the [demand partner settings](#demand-partner-settings) table below. |
| `id` | integer | A unique identifier for the config object being returned. This id is then referred to as `prebid_settings_id` in other endpoints of this API. |
| `last_modified` | string | The most recent modification date of the config object. |
| `member_id` | integer | The caller's member id. |
| `price_granularity` | object | The price bucket granularity setting that will be used for this member. For items contained in a price_granularity object, see the [price granularity](#price-granularity) properties table below. |
| `total_configs` | integer | The number of configs returned. |

### Demand partner settings

| Property | Type | Description |
|:---|:---|:---|
| `bid_cpm_adjustment` | float | Multiplier value applied to the Demand Partner's CPM bid price to adjust how the bids compete in auction. |
| `enabled` | boolean | Indicates if the demand partner has been enabled or disabled. |
| `id` | integer | The id for the demand partner settings. |
| `name` | string | The name of the demand partner. |

### Config properties

| Property | Type | Description |
|:---|:---|:---|
| `demand_partner_config_params` | array | Container with the demand partners' config parameters. For items contained in a demand_partner_config_params object, see the [demand partner configs properties](#demand-partner-configs-properties) table below. |
| `enabled` | boolean | Indicates if the config is enabled or disabled. |
| `id` | integer | The id of the config. |
| `last_modified` | string | The most recent modification date of the config. Formatted as date-time. |
| `media_types` | object | The media types associated with the config. For items contained in a media_types object, see the [media types](#media-types) properties table below. |
| `member_id` | integer | The member_id associated with the config. |
| `name` | string | The name of the config. |
| `targeting_level_code` | integer | The rank of the type of object in the targeting hierarchy. Placement has `targeting_level_code` 0, placement group is 1, publisher is 2. |
| `targeting_id` | integer | The id of the object the configuration is associated with. Requests will be sent to Demand Partners when that object or an object matching the criteria is in the request. |
| `targeting_level_name` | string | The name of the level (example: publisher) |
| `deleted` | boolean | If `true`, indicates that the config object is not available for use but its data is still viewable. |
| `last_modified_by` | string | The person who made the last modifications to the demand partner params. |
| `targeting_metadata` | object | Includes modifiers for the targeting object. For items contained in the `targeting_metadata` object, see the [Targeting Metadata Properties](#targeting-metadata-properties) table below. |

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

### Demand partner configs properties

| Property | Type | Description |
|:---|:---|:---|
| `enabled` | boolean | Indicates if the Demand Partner has been enabled or disabled. For more information, see the [Demand Partner Service](demand-partner-service.md). |
| `deleted` | boolean | If `true`, indicates that the config object is not available for use but its data is still viewable. |
| `id` | integer | The id of the parameter mappings for the specific demand partner. |
| `last_modified` | string | The most recent modification date of the `demand_partner_config`. |
| `last_modified_by` | string | The person who made the last modifications to the `demand_partner_config`. |
| `member_id` | integer | The member_id associated with the `demand_partner_config`. |
| `name` | string | The [Prebid bidder name](../monetize/prebid-server-premium-demand-partner-integrations.md) for the Demand Partner. |
| `params` | object | The partner-specific parameters and mapped values. For more information, see the [Demand Partner Service](demand-partner-service.md). |
| `prebid_settings_id` | integer | The ID of the config which can contain multiple demand partner parameter mappings. |

### Price granularity

Price granularity defines the CPM price buckets into which demand partner bids will be grouped. This is defined in the [Cross-Partner Settings Service](cross-partner-settings-service.md).

| Property | Type | Description |
|:---|:---|:---|
| `label` | string | The name of the default Prebid price bucket tier. For more information, see [Price Granularity](https://docs.prebid.org/adops/price-granularity.html).|
| `ranges` | object | Container object describing the price granularity range. |
| `ranges.max` | integer | The maximum length of the range. |
| `ranges.increment` | float | The amount to increment through the range. |
| `precision` | integer | The number of decimal places in the price granularity ranges. |
| `currency_code` | string | The currency of the price buckets. |

### Pagination

The number of responses can be limited by passing the `num_elements` argument. Which element to start viewing can be set through the `start_element` argument.

| Field | Type | Description |
|:---|:---|:---|
| `start_element` | int | The number at which to start counting. |
| `num_elements` | int | How many elements to return. For example, start at object # 4 and return 3 objects, or # 4, 5, 6. |

#### Example call to limit to fifteen results and to start the results at the tenth element

The elements returned will be indexed from the 10th through the twenty-fifth.

```
GET https://api.appnexus.com/prebid/config?num_element=15&start_element=10
```

### Click to view a sample JSON response

```
{
   "bidder_timeout_ms":750,
   "configs":[
      {
         "deleted":false,
         "demand_partner_config_params":[
            {
               "deleted":false,
               "enabled":true,
               "id":24682,
               "last_modified":"2020-02-20T15:48:36Z",
               "last_modified_by":"auser@9325",
               "member_id":9325,
               "name":"appnexus",
               "params":{
                  "invCode":null,
                  "inv_code":null,
                  "keywords":null,
                  "member":null,
                  "placementId":null,
                  "placement_id":null,
                  "position":null,
                  "private_sizes":null,
                  "reserve":null,
                  "targetingId":4887810,
                  "trafficSourceCode":null,
                  "traffic_source_code":null,
                  "use_pmt_rule":null
               },
               "prebid_settings_id":5084
            },
            {
               "deleted":false,
               "enabled":true,
               "id":24681,
               "last_modified":"2020-02-20T15:48:36Z",
               "last_modified_by":"auser@9325",
               "member_id":9325,
               "name":"pubmatic",
               "params":{
                  "adSlot":null,
                  "keywords":null,
                  "publisherId":"test123",
                  "wrapper":null
               },
               "prebid_settings_id":5084
            }
         ],
         "enabled":true,
         "id":5084,
         "last_modified":"2020-02-20T15:48:36Z",
         "last_modified_by":"auser@9325",
         "media_types":{
            "sizes":[
               {
                  "height":150,
                  "is_standard":false,
                  "width":180
               },
               {
                  "height":250,
                  "is_standard":false,
                  "width":300
               }
            ],
            "type":"banner"
         },
         "member_id":9325,
         "name":"Targeting Test",
         "targeting_id":4887810,
         "targeting_level_code":1,
         "targeting_level_name":"site",
         "targeting_metadata":{
            "os_family_ids":[
               ""
            ]
         }
      },
      {
         "deleted":false,
         "demand_partner_config_params":[
            {
               "deleted":false,
               "enabled":true,
               "id":14370,
               "last_modified":"2020-02-14T15:17:53Z",
               "last_modified_by":"auser@9325",
               "member_id":9325,
               "name":"pubmatic",
               "params":{
                  "adSlot":"Test Slot",
                  "keywords":null,
                  "publisherId":"9325",
                  "wrapper":null
               },
               "prebid_settings_id":1930
            },
            {
               "deleted":false,
               "enabled":true,
               "id":14371,
               "last_modified":"2020-02-14T15:17:53Z",
               "last_modified_by":"auser@9325",
               "member_id":9325,
               "name":"appnexus",
               "params":{
                  "invCode":null,
                  "inv_code":null,
                  "keywords":null,
                  "member":null,
                  "placementId":null,
                  "placement_id":null,
                  "position":null,
                  "private_sizes":null,
                  "reserve":null,
                  "targetingId":3589320,
                  "trafficSourceCode":null,
                  "traffic_source_code":null,
                  "use_pmt_rule":null
               },
               "prebid_settings_id":1930
            }
         ],
         "enabled":true,
         "id":1930,
         "last_modified":"2020-02-14T15:17:53Z",
         "last_modified_by":"auser@9325",
         "media_types":{
            "sizes":[
               {
                  "height":600,
                  "width":160
               }
            ],
            "type":"banner"
         },
         "member_id":9325,
         "name":"Test - Harish",
         "targeting_id":3589320,
         "targeting_level_code":1,
         "targeting_level_name":"site",
         "targeting_metadata":{
            "os_family_ids":[
               4
            ]
         }
      }
   ],
   "deleted":false,
   "demand_partner_settings":{
      "adform":{
         "bid_cpm_adjustment":2,
         "enabled":true,
         "id":102
      },
      "appnexus":{
         "bid_cpm_adjustment":1,
         "enabled":true,
         "id":65
      },
      "appnexus-video":{
         "bid_cpm_adjustment":4,
         "enabled":true,
         "id":118
      },
      "triplelift_native":{
         "bid_cpm_adjustment":1,
         "enabled":true,
         "id":320
      },
      "verizonmedia":{
         "bid_cpm_adjustment":1,
         "enabled":true,
         "id":240
      }
   },
   "id":2,
   "last_modified":"2020-02-12T18:06:33Z",
   "member_id":9325,
   "price_granularity":{
      "label":"Medium",
      "precision":2,
      "ranges":[
         {
            "increment":0.1,
            "max":20
         }
      ]
   },
   "total_configs":36
}               
            
```

## `POST`

Enables the creation of a new config object.

### Example call using curl

```
curl -d @config.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/config'
```

### `POST`: Parameters

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the configuration. |
| `enabled` | boolean | Required | Indicates if the config is enabled or disabled. |
| `demand_partner_config_params` | array | Required | An array containing demand_partner_config_params objects. For items contained in a `demand_partner_config_params` object, see the [demand partner configs properties](#post-demand-partner-configs-properties) table below. |
| `media_types` | object | Required | The media_types associated with the config. For items contained in a `media_type` object, see the [media type](#post-media-types) properties table below. |
| `targeting_id` | integer | Required | The id of the object the configuration is associated with. Requests will be sent to Demand Partners when that object or an object matching the criteria is in the request. |
| `targeting_level_code` | integer | Required | The rank of the type of object in the targeting hierarchy. Placement has `targeting_level_code` 0, placement group is 1, publisher is 2. |
| `targeting_metadata` | object | Optional | Includes modifiers for the targeting object. For items contained in the `targeting_metadata` object, see the [Targeting Metadata Properties](#post-targeting-metadata-properties) table below. |

### `POST`: Demand partner configs properties

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `deleted` | boolean | Required | If `true`, indicates that the config object is not available for use but its data is still viewable. |
| `member_id` | integer | Required | The member_id associated with the `demand_partner_config`. |
| `name` | string | Required | The [Prebid bidder name](../monetize/prebid-server-premium-demand-partner-integrations.md) for the Demand Partner. |
| `params` | object | Required | The partner-specific parameters and mapped values. For more information, see the [Demand Partner Service](demand-partner-service.md). |
| `prebid_settings_id` | integer | Required | The ID of the config which can contain multiple demand partner parameter mappings. |

### `POST`: Media types

The media type object determines which formats (currently banner, native, and video) and ad sizes are included in the requests to demand partners.

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `sizes` | object | Optional | Demand Partners will only receive requests for this configuration where these ad sizes are present. |
| `sizes.width` | integer | Optional | Width of the unit. For Example, 300. |
| `sizes.height` | integer | Optional | Height of the unit. For Example, 250. |
| `sizes.is_standard` | boolean | Optional | Denotes whether the size has been defined as standard by the member. |
| `types` | array | Required | Includes the media type(s) eligible for the configuration. Only these types will be passed to demand partners in requests. Values are banner, native, video. |

### `POST`: Targeting metadata properties

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `os_family_ids` | array | Optional | Demand Partners will only receive requests for this configuration where these operating systems are present. Operating systems represented by integer ids from the [Operating System-Families Service](operating-system-families-service.md). |

### Click to view a sample JSON request

```
{
   "name":"test_configuration",
   "enabled":false,
   "demand_partner_config_params":[
      {
         "deleted":false,
         "enabled":true,
         "id":7466,
         "member_id":9325,
         "name":"rubicon",
         "params":{
            "accountId":1001,
            "inventory":null,
            "siteId":113932,
            "video":null,
            "visitor":null,
            "zoneId":535510
         }
      }
   ],
   "media_types":{
      "sizes":[
         {
            "height":600,
            "width":160
         }
      ],
      "type":"banner"
   }
}            
            
```

### Response

A successful response will return the new config object.

### `POST`: Click to view a sample JSON response

```
[
   {
      "deleted":false,
      "demand_partner_config_params":[
         {
            "deleted":false,
            "enabled":true,
            "id":24679,
            "last_modified":"2020-02-19T17:53:36.674Z",
            "last_modified_by":"azacarias@9325",
            "member_id":9325,
            "name":"rubicon",
            "params":{
               "accountId":1001,
               "inventory":null,
               "siteId":113932,
               "video":null,
               "visitor":null,
               "zoneId":535510
            },
            "prebid_settings_id":5083
         },
         {
            "deleted":false,
            "enabled":true,
            "id":24680,
            "last_modified":"2020-02-19T17:53:36.674Z",
            "last_modified_by":"azacarias@9325",
            "member_id":9325,
            "name":"appnexus",
            "params":{
               
            },
            "prebid_settings_id":5083
         }
      ],
      "enabled":false,
      "id":5083,
      "last_modified":"2020-02-19T17:53:36.674Z",
      "last_modified_by":"azacarias@9325",
      "media_types":{
         "sizes":[
            {
               "height":600,
               "width":160
            }
         ],
         "type":"banner"
      },
      "member_id":9325,
      "name":"test_configuration",
      "targeting_id":null,
      "targeting_level_code":null,
      "targeting_metadata":null
   }
]                
                
```

## `PUT`

Updates an existing Prebid config. Include the `prebidSettingsId` as the last component of the URL path. Pass the update information as JSON in the body of the request.

### `PUT`: Example call using curl

```
curl -d @config-update.json -X PUT --header "Content-Type: application/json https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

### `PUT`: Response

Returns a Prebid config object.

## `PATCH`

Partially update an existing Prebid config. Include the `prebidSettingsId` as the last component of the path. Pass the update information as JSON in the body of the request.

### `PATCH`: Example call using curl

```
curl -d @config-update.json -X PATCH --header "Content-Type: application/json https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

### `PATCH`: Response

Returns a Prebid config object.

## `DELETE`

Delete an existing Prebid config. Include the `prebidSettingsId` as the last component of the path.

### `DELETE`: Example call using curl

```
curl -X DELETE https://api.appnexus.com/prebid/config/{prebidSettingsId}
```

### `DELETE`: Response

On success, the config indicated will be returned as a JSON object with the deleted property set to `true`. It will no longer be available within the system. All sub-objects will also be deleted.

## Related topics

- [Demand Partner Schema Service](demand-partner-schema-service.md)
- [Demand Partner Service](demand-partner-service.md)
- [Prebid Demand Partner Params Service](prebid-demand-partner-params-service.md)
- [Ad Sizes Service](ad-sizes-service.md)
- [Media Type Service](media-type-service.md)
- [Add, Edit, or Delete a PSP Configuration](../monetize/add-edit-or-delete-a-psp-configuration.md)
