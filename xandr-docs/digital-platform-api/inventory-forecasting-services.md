---
title: Inventory Forecasting Services
description: In this article, explore about the Inventory Forecasting services that are designed to help you learn about inventory availability and contention.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Inventory Forecasting services

> [!NOTE]
> Inventory Forecasting Services are available only to Xandr Ad Server customers.

For a publisher to commit to delivering against an advertiser's budget, that publisher needs a way to forecast how much inventory is available for the advertiser to buy. In addition, the publisher needs a way to discover *inventory contention.* Inventory contention occurs when there are multiple guaranteed line items competing for the same inventory. Understanding contention is important so the publisher can make prioritization decisions when conflicts occur.

The API services described on this page are designed to help you learn about inventory availability and contention. [Forecast Inventory-Multi Service](#forecast-inventory-multi-service) and [Forecast Contention-Multi Service](#forecast-contention-multi-service) are fully supported services.

> [!NOTE]
> The Inventory Forecasting Services support both legacy Guaranteed Delivery Line Items (GDLI) and Guaranteed Delivery Augmented Line Items (GDALI). The following will help you make proper forecasting requests for these different line item types:
>
> - **Legacy GDLIs**
>   - Legacy GDLIs support campaigns, but do not support splits.
>   - If you do not have multiple child campaigns, pass an empty array (`campaigns: [ ]`).
>   - For more information, see [Using Multiple Campaigns with a Guaranteed Line Item](../monetize/using-multiple-campaigns-with-a-guaranteed-line-item.md).
> - **GDALIs**
>   - GDALIs support splits, but do not support campaigns.
>   - When you include split details in your request, you can use the query string parameter `split_breakout=true` to return a forecast
>     broken down by individual splits as well as the line item as a whole.
>   - The  GDALI UI uses Inventory Forecasting Services for its **Forecasting Footer**. For more information, see the "Forecasting" section in [Create a Guaranteed Delivery Augmented Line Item](../monetize/create-a-guaranteed-delivery-line-item-gdali.md).

## Forecast inventory-multi service

### REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/forecast-inventory-multi](https://api.appnexus.com/forecast-inventory-multi) | Run an inventory forecast using a hypothetical profile.<br><br>**Note:** The Forecast Inventory-Multi Service only supports `POST` calls. |

#### Query string parameters

Use the query string parameters shown in the table below to tune the output. For Legacy GDLI and GDALI usage, see examples below.

| Field | Description |
|:---|:---|
| `priority` | When passed on the query string in the form `priority=x`, inventory from lower priority line items will be displaced and considered available.<br>**Required:** No |
| `roadblocking_enabled` | This field specifies whether multiple ad sizes are grouped together in a roadblock. When passed as `roadblocking_enabled=true`, two or more ad sizes are required to be passed in the `size_targets` array of the profile. For page-level roadblocking, you must include the master creative sizes in the `roadblock` object under `line_item`. For more information about roadblocking, see [Target Your Inventory with Roadblocking](../monetize/target-your-inventory-with-roadblocking.md).<br>**Required:** No |
| `competitive_exclusions_enabled` | If this field is passed in you must also pass `advertiser_id`, `creative_id`, or both. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No |
| `advertiser_id` | When `competitive_exclusions_enabled=true` is passed, you should also pass in this field with the advertiser ID whose creatives have competing brands or offer categories, and therefore should not be included in the resulting forecast. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No, unless `competitive_exclusions_enabled` is also passed in the query string. |
| `creative_id` | When `competitive_exclusions_enabled=true` is passed, you should also pass in this field with a creative ID that has competing brands or offer categories, and therefore should not be included in the resulting forecast. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No, unless `competitive_exclusions_enabled` is also passed in the query string. |
| `line_item_exclusions` | A comma-separated list of line item IDs to exclude from the forecast.<br>**Required:** No |
| `viewability` | When set to true, the forecast will include only viewable impressions. Viewable impressions are calculated based on historic data. Applies to guaranteed delivery line items with a vCPM revenue type.<br>**Required:** No |
| `dynamic_timeout` | The number of tries (defaults to `1`).<br>**Required:** No |
| `dynamic_attempts` | The amount of time to wait for each trial (default is `2` minutes, minimum in prod is `10` seconds).<br>**Required:** No |
| `split_breakout` | When `split_breakout=true` is passed you should also pass split level details. This will return a forecast broken down by individual splits as well as the line item as a whole.<br><br>**Note:** GDALIs support splits; Legacy GDLIs do not support splits. <br><br>**Required:** No |

### JSON fields

#### General

| Field | Type | Description |
|:---|:---|:---|
| `line_item` | object | The flight dates and profile information associated with the line item against which you want to forecast.<br>**Required:** Yes |
| `campaigns` | array of objects | An array of objects containing campaign information for the line item.<br><br>**Note:** Legacy GDLIs support campaigns; GDALIs do not support campaigns. If your Legacy GDLI does not have multiple child campaigns, pass an empty array (`campaigns: []`).<br><br>**Required:** Yes for Legacy GDLIs, but can be empty. Line items cannot have both campaigns and splits. |
| `splits` | array of objects |  An array of objects containing split information for the line item.<br><br>**Note:** GDALIs support splits; Legacy GDLIs do not support splits. If your GDALI does not have splits, pass an empty array (`splits: []`). For more information, see [Splits Service](splits-service.md).<br><br>**Required:** Yes for GDALIs, but can be empty. Line items cannot have both campaigns and splits. |

#### Line item

| Field | Type | Description |
|:---|:---|:---|
| `start_date` | string  | The starting flight date.<br>**Required:** Yes |
| `end_date` | string  | The end date of the flight. <br>**Required:** Yes |
| `timezone` | enum | The timezone for which the line item is active. For details and accepted values, see [API Timezones](api-timezones.md).<br>**Required:** No, If not specified, member default timezone will be used. |
| `profile` | object  | An instance of the profile object. Use this object to define your targeting for the line item. For a list of available fields see, [Profile Service](profile-service.md). For profile settings that are specific to forecasting, see [Forecasting Profiles](#forecasting-profiles) below.<br>This field is required, but you can pass an empty object. However, passing an empty profile means you're forecasting without applying any targeting to your line item.<br>**Required:** Yes |
| `roadblock` | object | The roadblock settings for the line item.<br>**Required:** Yes, only if `roadblocking_enabled = true`. |
| `creatives` | array of objects | The creatives associated with the campaign. If you include creatives you must include at least the creative ID. For a list and descriptions of available fields, see [Creative Service](creative-service.md).<br>**Required:** No |

#### Roadblock

Roadblocks can be set on either the line item level or the campaign level, but not both. If a roadblock has been set on a campaign, it can't be set on the parent line item. Roadblocks can be applied only for managed inventory and can't be enabled when you're working with third-party inventory.

| Field | Type | Description |
|:---|:---|:---|
| `type` | enum | The type of roadblock. If you include the roadblock object, this field is required. Possible values include:<br> - `null`: There is no roadblocking set at the line item level. (GDALI only)<br> - `no_roadblock`: There is no roadblocking set at the line item level. (Legacy GDLI only)<br> - `normal_roadblock`: The line item serves if the number of creatives is greater than or equal to the number of ad slots available. (Legacy GDLI only)<br> - `partial_roadblock`: The line item serves when at least one creative of each size fits an eligible ad slot. (GDALI & Legacy GDLI)<br> - `exact_roadblock`: The line item serves when the number of creatives is equal to the number of ad slots available. (Legacy GDLI only)<br><br>**Note:** For GDALIs, this value must be either `null` or `partial_roadblock`. |
| `master_width` | int | The width of the master creative. Set this value only when using page-level roadblocking. For standard roadblocking, omit this field or set the value to `0`. (Do not set the value to `null`.) |
| `master_height` | int | The height of the master creative. Set this value only when using page-level roadblocking. For standard roadblocking, omit this field or set the value to `0`. (Do not set the value to `null`.) |

##### Master creative

The master creative is the creative with a size matching the `master_height` and `master_width` specified in the roadblock object. If more than one creative matches that size, the system will choose one as the master.

The master creative is used for page-level roadblocking, where one impression is recorded for the full set of creatives delivered for the roadblock. That recorded impression is based on the master creative. This means that if the master creative doesn't serve, no impression will be recorded. If you want to use creative-level roadblocking, where each creative delivered is counted as an impression, leave the `master_width` and `master_height` values blank.

For more on roadblocking, see [Target Your Inventory with Roadblocking](../monetize/target-your-inventory-with-roadblocking.md).

#### Campaigns

> [!NOTE]
> Legacy GDLIs support campaigns; GDALIs do not support campaigns.

| Field | Type | Description |
|:---|:---|:---|
| `name` | string  | The name of the campaign. You can forecast on multiple campaigns within a single line item, so the name must be unique within each line item.<br>**Required:** Yes |
| `profile` | object  | An instance of the profile object. Use this object to define your targeting for the campaign. For a list and descriptions of available fields, see [Profile Service](profile-service.md). For profile settings that are specific to forecasting, see [Forecasting Profiles](#forecasting-profiles) below.<br>**Required:** Yes |
| `start_date`  | string  | The starting date of the campaign.<br>**Required:** No |
| `end_date` | string | The ending date of the campaign.<br>**Required:** No |
| `timezone` | enum | The timezone for which the line item is active. For details and accepted values, see [API Timezones](api-timezones.md).<br>**Required:** No, If not specified, member default timezone will be used. |
| `creatives` | array of objects | The creatives associated with the campaign. If you include creatives you must include at least the creative ID. For a list and descriptions of available fields, see [Creative Service](creative-service.md).<br>**Required:** No |

### Forecasting profiles

You can define the targeting requirements for your forecast by using the [Profile Service](profile-service.md) on the line item and the campaign. However, there are some differences in how you need to define some of the fields for forecasting as opposed to other types of targeting specifications.

#### `postal_code_targets`

The fields for the `postal_code_targets` object in the `profile` service are defined in the [Postal Code Service](postal-code-service.md). If you want to forecast based on postal codes, you *must* provide the following information:

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | The postal code can be an alphanumeric string of up to 14 characters and can contain a space or hyphen. |
| `country_id` | string | The [ISO code](https://www.maxmind.com/en/iso3166) for the country/region to which the city belongs. You can use the [Country Service](country-service.md) to retrieve a complete list of country codes. |

##### Example

###### Expand source

```
"postal_code_targets":[  
        {
                "code": "02692",
                "country_id": "59"
        },
        {
                "code": "83712",
                "country_id": "233"
        }
]
```

#### Legacy GDLI example - Check inventory availability for legacy GDLIs with multiple campaigns

To see an inventory availability forecast across multiple child campaigns based on proposed targeting, create a JSON file in the format shown here:

```
{
  "line_item": {
    "start_date": "2019-02-10",
    "end_date": "2019-03-01",
    "profile": {
      "country_targets": [
        {
          "id": 169
        }
      ],
      "country_action": "include"
    }
  },
  "campaigns": [
    {
      "name": "foo",
      "start_date": "2019-02-11",
      "end_date": "2019-02-15",
      "profile": {
        "daypart_targets": [
          {
            "day": "tuesday",
            "start_hour": 8,
            "end_hour": 20
          }
        ]
      }
    },
    {
      "name": "bar",
      "start_date": "2019-02-20",
      "end_date": "2019-02-28",
      "profile": {
        "browser_targets": [
          {
            "id": 11
          }
        ],
        "browser_action": "include"
      }
    }
  ]
}
```

If you do not have multiple campaigns, simply pass in an empty array for campaigns:

```
{
  "line_item": {
    "start_date": "2019-02-10",
    "end_date": "2019-03-01",
    "profile": {
      "country_targets": [
        {
          "id": 169
        }
      ],
      "country_action": "include"
    }
  },
  "campaigns": [
  ]
}
```

Then `POST` it to the service as follows:

```
curl --silent  -b cookies -X POST -d '@/tmp/forecast-inventory-multi.json' "https://api.appnexus.com/forecast-inventory-multi"
```

You'll get back JSON in the following format:

```
{
   "response" : {
      "start_element" : 0,
      "inventory" : [
         {
            "daily_detail" : [
               {
                  "end_date" : "2019-02-11",
                  "available" : 0,
                  "capacity" : 0,
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-11"
               },
               {
                  "available" : 0,
                  "capacity" : 0,
                  "end_date" : "2019-02-12",
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-12"
               },
               {
                  "end_date" : "2019-02-13",
                  "available" : 0,
                  "capacity" : 0,
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-13"
               },
               {
                  "end_date" : "2019-02-14",
                  "capacity" : 0,
                  "available" : 0,
                  "start_date" : "2019-02-14",
                  "days_in_forecast" : 0
               },
               {
                  "available" : 118759,
                  "capacity" : 126738,
                  "end_date" : "2019-02-15",
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-15"
               },
               {
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-20",
                  "end_date" : "2019-02-20",
                  "available" : 163474200,
                  "capacity" : 176586394
               },
               {
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-21",
                  "end_date" : "2019-02-21",
                  "available" : 256485594,
                  "capacity" : 274037191
               },
               {
                  "capacity" : 212467438,
                  "available" : 199091285,
                  "end_date" : "2019-02-22",
                  "start_date" : "2019-02-22",
                  "days_in_forecast" : 0
               },
               {
                  "capacity" : 189452983,
                  "available" : 177450785,
                  "end_date" : "2019-02-23",
                  "start_date" : "2019-02-23",
                  "days_in_forecast" : 0
               },
               {
                  "start_date" : "2019-02-24",
                  "days_in_forecast" : 0,
                  "capacity" : 180309046,
                  "available" : 168589468,
                  "end_date" : "2019-02-24"
               },
               {
                  "start_date" : "2019-02-25",
                  "days_in_forecast" : 0,
                  "capacity" : 182850122,
                  "available" : 171364216,
                  "end_date" : "2019-02-25"
               },
               {
                  "end_date" : "2019-02-26",
                  "available" : 129049282,
                  "capacity" : 139962276,
                  "days_in_forecast" : 0,
                  "start_date" : "2019-02-26"
               },
               {
                  "start_date" : "2019-02-27",
                  "days_in_forecast" : 0,
                  "capacity" : 171623425,
                  "available" : 158879752,
                  "end_date" : "2019-02-27"
               },
               {
                  "end_date" : "2019-02-28",
                  "capacity" : 268133170,
                  "available" : 250959715,
                  "start_date" : "2019-02-28",
                  "days_in_forecast" : 0
               }
            ],
            "summary" : {
               "days_in_forecast" : 14,
               "start_date" : "2019-02-10",
               "available" : 1675463056,
               "capacity" : 1795548783,
               "end_date" : "2019-03-01"
            }
         }
      ],
      "num_elements" : 1,
      "count" : 1,
      "status" : "OK"
   }
}
```

#### GDALI example - Check inventory availability for GDALIs with splits

To see an inventory availability forecast across splits based on proposed targeting, create a JSON file in the format shown here:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-04-28 00:00:00",
        "end_date": "2022-05-01 23:59:59",
        "profile": {
            "country_targets": [
                {
                    "id": 123,
                    "action": "include",
                }
            ],
            "size_targets": {
                "width": 190,
                "height": 213
            },
            {
                "width": 728,
                "height": 90
            },
            "id": null,
            "advertiser_id": 5878213,
            "graph_id": null
        },
        "creatives": [],
        "roadblock": null
    },
    "splits": [
        {
            "id": 111111111,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 1,
            "name": "Name1",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 222222222,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 2,
            "name": "Name2",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 333333333,
            "is_default": true,
            "active": false,
            "order": 5,
            "name": "Default",
            "allocation_strategy": "unconstrained",
            "creatives": []
        }
    ]
}
```

If you do not have splits, simply pass in an empty array for splits:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-04-28 00:00:00",
        "end_date": "2022-05-01 23:59:59",
        "profile": {
            "country_targets": [
                {
                    "id": 123,
                    "action": "include",
                }
            ],
            "size_targets": {
                "width": 190,
                "height": 213
            },
            {
                "width": 728,
                "height": 90
            },
            "id": null,
            "advertiser_id": 5878213,
            "graph_id": null
        },
        "creatives": [],
        "roadblock": null
    },
    "splits": [        
    ]
}
```

Then `POST` it to the service either without any additional queries or with the `split_breakout` query:

##### `POST` without additional queries

```
curl --silent  -b cookies -X POST -d '@/tmp/forecast-inventory-multi.json' "https://api.appnexus.com/forecast-inventory-multi"
```

You'll get back JSON in the following format:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-04-28 00:00:00",
        "end_date": "2022-05-01 23:59:59",
        "profile": {
            "country_targets": [
                {
                    "id": 123,
                    "action": "include",
                }
            ],
            "size_targets": {
                "width": 190,
                "height": 213
            },
            {
                "width": 728,
                "height": 90
            },
            "id": null,
            "advertiser_id": 5878213,
            "graph_id": null
        },
        "creatives": [],
        "roadblock": null
    },
    "splits": [
        {
            "id": 111111111,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 1,
            "name": "Name1",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 222222222,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 2,
            "name": "Name2",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 333333333,
            "is_default": true,
            "active": false,
            "order": 5,
            "name": "Default",
            "allocation_strategy": "unconstrained",
            "creatives": []
        }
    ]
}
```

##### `POST` with `split_breakout` query

```
curl --silent  -b cookies -X POST -d '@/tmp/forecast-inventory-multi.json' "https://api.appnexus.com/forecast-inventory-multi?split_breakout=true"
```

You'll get back JSON in the following format:

```
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "inventory": [
            {
                "split_breakout": [
                    {
                        "name": "split 1",
                        "id": 111111111,
                        "daily_detail": [
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-13",
                                "end_date": "2022-12-13"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-14",
                                "end_date": "2022-12-14"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-15",
                                "end_date": "2022-12-15"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-16",
                                "end_date": "2022-12-16"
                            }
                        ],
                        "summary": {
                            "available": 0,
                            "capacity": 0,
                            "days_in_forecast": 4,
                            "start_date": "2022-12-13",
                            "end_date": "2022-12-16"
                        }
                    },
                    {
                        "name": "split 2",
                        "id": 222222222,
                        "daily_detail": [
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-13",
                                "end_date": "2022-12-13"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-14",
                                "end_date": "2022-12-14"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-15",
                                "end_date": "2022-12-15"
                            },
                            {
                                "available": 0,
                                "capacity": 0,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-16",
                                "end_date": "2022-12-16"
                            }
                        ],
                        "summary": {
                            "available": 0,
                            "capacity": 0,
                            "days_in_forecast": 4,
                            "start_date": "2022-12-13",
                            "end_date": "2022-12-16"
                        }
                    },
                    {
                        "name": "Default",
                        "id": 000000000,
                        "daily_detail": [
                            {
                                "available": 14076857,
                                "capacity": 19714967,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-13",
                                "end_date": "2022-12-13"
                            },
                            {
                                "available": 17695775,
                                "capacity": 18459811,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-14",
                                "end_date": "2022-12-14"
                            },
                            {
                                "available": 18542490,
                                "capacity": 19292381,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-15",
                                "end_date": "2022-12-15"
                            },
                            {
                                "available": 18106140,
                                "capacity": 18859887,
                                "days_in_forecast": 0,
                                "start_date": "2022-12-16",
                                "end_date": "2022-12-16"
                            }
                        ],
                        "summary": {
                            "available": 68421262,
                            "capacity": 76327046,
                            "days_in_forecast": 4,
                            "start_date": "2022-12-13",
                            "end_date": "2022-12-16"
                        }
                    }
                ],
                "daily_detail": [
                    {
                        "available": 14076857,
                        "capacity": 19714967,
                        "days_in_forecast": 0,
                        "start_date": "2022-12-13",
                        "end_date": "2022-12-13"
                    },
                    {
                        "available": 17695775,
                        "capacity": 18459811,
                        "days_in_forecast": 0,
                        "start_date": "2022-12-14",
                        "end_date": "2022-12-14"
                    },
                    {
                        "available": 18542490,
                        "capacity": 19292381,
                        "days_in_forecast": 0,
                        "start_date": "2022-12-15",
                        "end_date": "2022-12-15"
                    },
                    {
                        "available": 18106140,
                        "capacity": 18859887,
                        "days_in_forecast": 0,
                        "start_date": "2022-12-16",
                        "end_date": "2022-12-16"
                    }
                ],
                "summary": {
                    "available": 68421262,
                    "capacity": 76327046,
                    "days_in_forecast": 4,
                    "start_date": "2022-12-13",
                    "end_date": "2022-12-16"
                }
            }
        ]
    }
}
```

#### Legacy GDLI example - Check inventory availability for legacy GDLIs with a roadblock

To run an inventory availability forecast given a roadblock with several creative sizes, you'll need to:

- Modify your profile to include the `size_targets` array.
- Pass `roadblocking_enabled=true` on the query string of the request.

It's possible to define size targets and also add creatives to your line item or campaigns. When you do this, all sizes will be used in the forecast. When you enable roadblocking, the size with the smallest number of available impressions will be used as the forecasted capacity.

> [!NOTE]
> In this example, the `size_targets` and creative sizes will all be considered when determining forecasting.

Here's an example of the JSON you would send in your query:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-05-16 00:00:00",
        "end_date": "2022-06-12 23:59:59",
        "timezone": "Europe/Brussels",
        "profile": {},
        "creatives": [],
        "roadblock": {
            "type": "partial_roadblock",
            "master_width": 320,
            "master_height": 101
        }
    },
    "campaigns": [],
}       
```

#### GDALI example - Check inventory availability for GDALIs with a roadblock

To run an inventory availability forecast on GDALIs given a roadblock with several creative sizes, you'll need to:

- Modify your profile to include the `size_targets` array.
- Pass `roadblocking_enabled=true` on the query string of the request.

It's possible to define size targets and also add creatives to your line item. When you do this, all sizes will be used in the forecast. When you enable roadblocking, the size with the smallest number of available impressions will be used as the forecasted capacity.

> [!NOTE]
> In this example, the `size_targets` and creative sizes will all be considered when determining forecasting.

Here's an example of the JSON you would send in your query:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-05-16 00:00:00",
        "end_date": "2022-06-12 23:59:59",
        "timezone": "Europe/Brussels",
        "profile": {
            "country_targets": [
                {
                    "id": 123,
                    "action": "include",
                }
            ],
            size_targets": {
                "width": 320,
            "height": 101
        },
        {
            "width": 320,
            "height": 252
        },
        "id": null,
        "advertiser_id": 7777777,
        "graph_id": null
    },
    "creatives": [],
    "roadblock": {
        "type": "partial_roadblock",
        "master_width": 320,
        "master_height": 101
    },
    "splits": [
        {
            "id": 111111111
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 1,
            "name": "Name1",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 222222222,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 2,
            "name": "Name2",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 333333333,
            "is_default": true,
            "active": false,
            "order": 7,
            "name": "Default",
            "allocation_strategy": "unconstrained",
            "creatives": []
        }
    ]
}
```

## Forecast contention-multi service

### Forecast contention-multi service: REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/forecast-contention-multi](https://api.appnexus.com/forecast-contention-multi) | Run an inventory contention forecast using a hypothetical targeting profile.<br><br>**Tip:** The Forecast Contention-Multi Service only supports `POST` calls. |

#### Query string parameters for forecast contention-multi service

Use the query string parameters shown in the table below to tune the output. For Legacy GDLI and GDALI usage, see examples below.

| Field | Description |
|:---|:---|
| `priority` | When passed on the query string in the form `priority=x`, inventory from lower priority line items will be displaced and considered available.<br>**Required:** No |
| `competitive_exclusions_enabled` | If this field is passed in you must also pass `advertiser_id`, `creative_id`, or both. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No |
| `advertiser_id` | When `competitive_exclusions_enabled=true` is passed, you should also pass in this field with the advertiser ID whose creatives have competing brands or offer categories, and therefore should not be included in the resulting forecast. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No, unless `competitive_exclusions_enabled` is also passed in the query string. |
| `creative_id` | When `competitive_exclusions_enabled=true` is passed, you should also pass in this field with a creative ID that has competing brands or offer categories, and therefore should not be included in the resulting forecast. For more information about competitive exclusions, see [Competitive Exclusions](../monetize/competitive-exclusions.md).<br>**Required:** No, unless `competitive_exclusions_enabled` is also passed in the query string. |
| `line_item_exclusions` | A comma-separated list of line item IDs to exclude from the forecast.<br>**Required:** No |
| `dynamic_timeout` | The number of tries (defaults to 1)<br>**Required:** No |
| `dynamic_attempts` | The amount of time to wait for each trial (default is 2 minutes, minimum in prod is 10 seconds)<br>**Required:** No |
| `split_breakout` | When `split_breakout=true` is passed you should also pass split level details. This will return a forecast, broken down by individual splits as well as the line item as a whole.<br><br>**Note:** GDALIs support splits; Legacy GDLIs do not support splits.<br><br>**Required:** No |

### Forecast contention-multi service: JSON fields

#### Forecast contention-multi service: General

| Field | Type | Description |
|:---|:---|:---|
| `line_item` | object | The flight dates and profile information associated with the line item against which you want to forecast.<br>**Required:** Yes  |
| `campaigns` | array of objects | An array of objects containing campaign information for the line item.<br><br>**Note:** Legacy GDLIs support campaigns; GDALIs do not support campaigns. If your Legacy GDLI does not have multiple child campaigns, pass an empty array (`campaigns: []`).<br><br>**Required:** Yes for Legacy GDLIs, but can be empty. Line items cannot have both campaigns and splits. |
| `splits` | array of objects | An array of objects containing split information for the line item.<br><br>**Note:** GDALIs support splits; Legacy GDLIs do not support splits. If your GDALI does not have splits, pass an empty array (`splits: []`). For more information, see [Splits Service](splits-service.md). <br><br>**Required:** Yes for GDALIs, but can be empty. Line items cannot have both campaigns and splits. |

#### Forecast contention-multi service: Line item

| Field | Type | Description |
|:---|:---|:---|
| `start_date` | string  | The starting flight date.<br>**Required:** Yes  |
| `end_date` | string  | The end date of the flight.<br>**Required:** Yes   |
| `timezone` | enum | The timezone for which the line item is active. For details and accepted values, see [API Timezones](api-timezones.md).<br>**Required:** No. If not specified, member default timezone will be used. |
| `profile` | object  | An instance of the profile object. Use this object to define your targeting for the line item. For a list and descriptions of available fields, see [Profile Service](profile-service.md). For profile settings that are specific to forecasting, see [Forecasting Profiles](#forecasting-profiles) above.<br>This field is required, but you can pass an empty object. However, passing an empty profile means you're forecasting without applying any targeting to your line item.<br>**Required:** Yes  |

#### Forecast contention-multi service: Campaigns

> [!NOTE]
> Legacy GDLIs support campaigns; GDALIs do not support campaigns.

| Field | Type | Description |
|:---|:---|:---|
| `name` | string  | The name of the campaign. You can forecast on multiple campaigns within a single line item, so the name must be unique within each line item.<br>**Required:** Yes  |
| `profile` | object  |  An instance of the profile object. Use this object to define your targeting for the line item. For a list and descriptions of available fields, see [Profile Service](profile-service.md). For profile settings that are specific to forecasting, see [Forecasting Profiles](#forecasting-profiles) above.<br>**Required:** Yes  |
| `start_date`  | string  | The starting date of the campaign. <br>**Required:** No |
| `end_date` | string | The ending date of the campaign.<br>**Required:** No |
| `timezone` | enum | The timezone for which the line item is active. For details and accepted values, see [API Timezones](api-timezones.md).<br>**Required:** No. If not specified, member default timezone will be used. |
| `creatives` | array of objects | The creatives associated with the campaign. If you include creatives you must include at least the creative ID. For a list and descriptions of available fields, see [Creative Service](creative-service.md).<br>**Required:** No |

#### Legacy GDLI example - Check inventory contention for legacy GDLIs with multiple campaigns

To see an inventory contention forecast across multiple child campaigns based on your proposed targeting settings, create a JSON file in the format shown below:

```
{
  "line_item": {
    "start_date": "2019-02-10",
    "end_date": "2019-03-01",
    "profile": {
      "country_targets": [
        {
          "id": 169
        }
      ],
      "country_action": "include"
    }
  },
  "campaigns": [
    {
      "name": "foo",
      "start_date": "2019-02-11",
      "end_date": "2019-02-15",
      "profile": {
        "daypart_targets": [
          {
            "day": "tuesday",
            "start_hour": 8,
            "end_hour": 20
          }
        ]
      }
    },
    {
      "name": "bar",
      "start_date": "2019-02-20",
      "end_date": "2019-02-28",
      "profile": {
        "browser_targets": [
          {
            "id": 11
          }
        ],
        "browser_action": "include"
      }
    }
  ]
}      
```

If you do not have multiple campaigns, simply pass in an empty array for campaigns:

```
{
  "line_item": {
    "start_date": "2019-02-10",
    "end_date": "2019-03-01",
    "profile": {
      "country_targets": [
        {
          "id": 169
        }
      ],
      "country_action": "include"
    }
  },
  "campaigns": [
  ]
}
```

Then `POST` it to the service as follows:

```
curl --silent  -b cookies -X POST -d '/tmp/forecast-contention-multi.json' "https://api.appnexus.com/forecast-contention-multi"
      
```

You'll get back JSON in the following format:

```
{
   "response" : {
      "num_elements" : 100,
      "count" : 2,
      "start_element" : 0,
      "status" : "OK",
      "contention" : [
         {
            "competing_impressions" : 25083480,
            "line_item" : {
               "status" : "live",
               "advertiser_id" : 123456,
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "profile_id" : 50058150,
               "member_id" : 1234,
               "name" : "carrot juice airplane",
               "delivery_goal" : {
                  "reserved" : true,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true,
                  "percentage" : 100
               },
               "id" : 123457,
               "revenue_value" : 0,
               "currency" : "EUR",
               "priority" : 19,
               "state" : "active",
               "end_date" : "2019-12-31 23:59:59"
            }
         },
         {
            "line_item" : {
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "status" : "live",
               "advertiser_id" : 123456,
               "delivery_goal" : {
                  "reserved" : true,
                  "percentage" : 100,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true
               },
               "currency" : "EUR",
               "revenue_value" : 0,
               "id" : 123456,
               "state" : "active",
               "priority" : 19,
               "end_date" : "2019-12-31 23:59:59",
               "profile_id" : 6,
               "name" : "lightning battery horse staple",
               "member_id" : 1234
            },
            "competing_impressions" : 88514063
         }
      ]
   }
}
```

```
{
   "response" : {
      "num_elements" : 100,
      "count" : 2,
      "start_element" : 0,
      "status" : "OK",
      "contention" : [
         {
            "competing_impressions" : 25083480,
            "line_item" : {
               "status" : "live",
               "advertiser_id" : 123456,
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "profile_id" : 50058150,
               "member_id" : 1234,
               "name" : "carrot juice airplane",
               "delivery_goal" : {
                  "reserved" : true,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true,
                  "percentage" : 100
               },
               "id" : 123457,
               "revenue_value" : 0,
               "currency" : "EUR",
               "priority" : 19,
               "state" : "active",
               "end_date" : "2019-12-31 23:59:59"
            }
         },
         {
            "line_item" : {
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "status" : "live",
               "advertiser_id" : 123456,
               "delivery_goal" : {
                  "reserved" : true,
                  "percentage" : 100,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true
               },
               "currency" : "EUR",
               "revenue_value" : 0,
               "id" : 123456,
               "state" : "active",
               "priority" : 19,
               "end_date" : "2019-12-31 23:59:59",
               "profile_id" : 6,
               "name" : "lightning battery horse staple",
               "member_id" : 1234
            },
            "competing_impressions" : 88514063
         }
      ]
   }
}
```

#### GDALI example - Check inventory contention for GDALIs with splits

To see an inventory contention forecast across splits based on your proposed targeting settings, create a JSON file in the format shown below:

```
{
    "line_item": {
        "ad_types": [
            "banner"
        ],
        "start_date": "2022-04-28 00:00:00",
        "end_date": "2022-05-01 23:59:59",
        "profile": {
            "country_targets": [
                {
                    "id": 123,
                    "action": "include",
                }
            ],
            "size_targets": {
                "width": 190,
                "height": 213
            },
            {
                "width": 728,
                "height": 90
            },
            "id": null,
            "advertiser_id": 5878213,
            "graph_id": null
        },
        "creatives": [],
        "roadblock": null
    },
    "splits": [
        {
            "id": 111111111,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 1,
            "name": "Name1",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 222222222,
            "conditions": []
            "is_default": false,
            "active": true,
            "order": 2,
            "name": "Name2",
            "allocation_strategy": "unconstrained",
            "creatives": []
        },
        {
            "id": 333333333,
            "is_default": true,
            "active": false,
            "order": 5,
            "name": "Default",
            "allocation_strategy": "unconstrained",
            "creatives": []
        }
    ]
}
```

Then `POST` it to the service as follows:

```
curl --silent  -b cookies -X POST -d '/tmp/forecast-contention-multi.json' "https://api.appnexus.com/forecast-contention-multi"
      
```

You'll get back JSON in the following format:

```
{
   "response" : {
      "num_elements" : 100,
      "count" : 2,
      "start_element" : 0,
      "status" : "OK",
      "contention" : [
         {
            "competing_impressions" : 25083480,
            "line_item" : {
               "status" : "live",
               "advertiser_id" : 123456,
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "profile_id" : 50058150,
               "member_id" : 1234,
               "name" : "carrot juice airplane",
               "delivery_goal" : {
                  "reserved" : true,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true,
                  "percentage" : 100
               },
               "id" : 123457,
               "revenue_value" : 0,
               "currency" : "EUR",
               "priority" : 19,
               "state" : "active",
               "end_date" : "2019-12-31 23:59:59"
            }
         },
         {
            "line_item" : {
               "start_date" : "2019-01-19 00:00:00",
               "revenue_type" : "cpm",
               "status" : "live",
               "advertiser_id" : 123456,
               "delivery_goal" : {
                  "reserved" : true,
                  "percentage" : 100,
                  "type" : "percentage",
                  "disallow_non_guaranteed" : true
               },
               "currency" : "EUR",
               "revenue_value" : 0,
               "id" : 123456,
               "state" : "active",
               "priority" : 19,
               "end_date" : "2019-12-31 23:59:59",
               "profile_id" : 6,
               "name" : "lightning battery horse staple",
               "member_id" : 1234
            },
            "competing_impressions" : 88514063
         }
      ]
   }
}
```

## Related topics

- [Reference](reference.md)
- [Profile Service](profile-service.md)
- [Guaranteed Delivery](../monetize/guaranteed-delivery.md)
- [Competitive Exclusions](../monetize/competitive-exclusions.md)
