---
title: Curated Deal Line Item API Setup Guide
description: Learn the process of setting up an API implementation of a curated deal line item to target a deal.
ms.date: 7/3/2025
ms.custom: digital-platform-api
---

# Curated Deal Line Item API setup guide

Setting up an API implementation of a Curated Deal Line Item to target a deal requires configuring a number of different properties on different API objects. This guide will explain the process of creating and configuring a curated deal line item using our API.

## Overview

Curated deals represent a negotiated agreement between a buyer and a curator that combines a curator’s proprietary assets with Xandr Marketplace supply. These proprietary assets can include audience data, preferred inventory access, specially negotiated rates, optimization talent, investment strategy, and other features that enhance the deal supply and create a unique offering. Deal curators have their own member seat on the Xandr Platform, which they use to package supply and their own assets into curated deal IDs for buyers. Any DSP integrated to the Xandr exchange can buy curated deals.

Setting up a curated deal line item typically involves making requests to the following API service endpoints to access or create the corresponding API objects:

| API Endpoint | API Object | Detailed Reference |
|:---|:---|:---|
| `https://api.appnexus.com/advertiser` | advertiser | [Advertiser Service](./advertiser-service.md) |
| `https://api.appnexus.com/insertion-order` | insertion-order | [Insertion Order Service](./insertion-order-service.md) |
| `https://api.appnexus.com/deal` | deal | [Deal Service](./deal-service.md) |
| `https://api.appnexus.com/profile` | profile | [Profile Service](./profile-service.md) |
| `https://api.appnexus.com/line-item` | line-item (ALI) | [Line Item - ALI Service](./line-item-service---ali.md) |

This guide uses cURL examples for all requests. You can use other API request tools (e.g., [Postman](https://www.getpostman.com/)), but you’ll then need to adjust the examples accordingly.

## Prerequisites

Before beginning this setup, be sure to read [API Getting Started](./api-getting-started.md). It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices.

## Order of operations

API objects often have dependencies on other API objects and there is an order you must follow in creating or accessing objects when you create a curated deal line item. For example, you must provide the IDs of the following API objects: `advertiser`, `insertion-order`, `deal`, and `profile`. To obtain the IDs for these objects, you'll need to either create them or already have access to them. The steps in this guide follow the typical order of operations required to create a curated deal line item.

## Best practices

For a general list of best practices to follow when working with the API, see [API Best Practices](./api-best-practices.md). The following are some best practices that are specific to a curated deal line item setup:

- Set the `state` field of the curated deal line item to `"inactive"` until the line item is fully configured and ready for testing.
- Note the ID of any objects you create. The IDs of objects you create are returned in the response body of requests. You'll often need these IDs later so copying them when they're returned can reduce the number of additional `GET` requests you have to make to obtain them.

## Setup procedure

> [!WARNING]
> While setting up a curated deal line item, you should not set a priority. If it is required to set a priority, set it to the default 5.

The following steps will guide you through the process of setting up a curated deal line item with typical configurations:

- [Step 1 - Obtain an authorization token](#step-1---obtain-an-authorization-token)
- [Step 2 - Create or access an advertiser](#step-2---create-or-access-an-advertiser)
- [Step 3 - Create or access an insertion order](#step-3---create-or-access-an-insertion-order)
- [Step 4 - Create a deal](#step-4---create-a-deal)
- [Step 5 - Create a curated deal line item profile](#step-5---create-a-curated-deal-line-item-profile)
- [Step 6 - Create a curated deal line item](#step-6---create-a-curated-deal-line-item)

### Step 1 - Obtain an authorization token

First, you’ll need to obtain an authorization token. You must then include this authorization token in all subsequent requests (see [Authentication Service](./authentication-service.md) for more information). To obtain an authorization token, do the following:

1. Create a JSON file containing your username and password.

    ```
    {
        "auth": {
            "username" : "USERNAME",
            "password" : "PASSWORD"
        }
    }
    ```

1. Make a `POST` request to the `/auth` endpoint with this JSON file in the request body (see [Authentication Service](./authentication-service.md) for more information). In the cURL request below, the authorization token returned is stored in the “`cookies`” file.

    ```
    curl -c cookies -X POST -d @authentication.json 'https://api.appnexus.com/auth'
    ```

1. Check the response body of your request (see **Example Response** below). If your request was successful, you’ll get a "`status`" of “`OK`” and the "`token`" field will be populated with the authentication token value. <br><br>**Example response**

    ```
    {
       "response" : {
          "token" : "authn:225692:2d787d1838283:lax1",
          "status" : "OK"      
       }
    }
    ```

### Step 2 - Create or access an advertiser

You'll need to create or access an advertiser from which to create a curated deal line item. You set up advertisers for curated deal line items the same way you would for augmented line items.

If you don't already have an advertiser to use, create an advertiser by doing the following (see [Advertiser Service](./advertiser-service.md) for more information):

1. Create an advertiser JSON:

    ```
    $ cat advertiser.json
    {
        "advertiser": {
            "name": "Curated Deal Line Item Example Advertiser",
            "timezone": "US/Pacific"
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/advertiser` endpoint with this advertiser JSON and an appropriate `member_id`.

    ```
    $ curl -b cookies -c cookies -X POST -d @advertiser.json 'https://api.appnexus.com/advertiser?member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the advertiser ID in the response body so you can use it when you create the curated deal line item in [Step 6 - Create a curated deal line item](#step-6---create-a-curated-deal-line-item).

#### JSON fields for advertiser (required and useful optional fields)

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the advertiser |
| `timezone` | enum | Optional | The timezone of the advertiser. See [API Timezones](./api-timezones.md) for details and accepted values.  |
| `use_insertion_orders` | boolean | Required | This field must be set to `true` in order to create curated deal line items. |
  
### Step 3 - Create or access an insertion order

You'll need to create or access an insertion order to create a curated deal line item. Curated deal line items require a seamless insertion order (see **required** fields below).

If you don't already have an insertion order to use, create an insertion order by doing the following (see [Insertion Order Service](./insertion-order-service.md) for more
information):

1. Create an insertion order JSON:

    **Example JSON: No end date, no budget**

    ```
    $ cat insertion-order-noenddate.json
    {
        "insertion-order": {
            "name": "Curated Deal Line Item Example IO",
            "budget_intervals": [{
                "start_date": "2019-10-10 00:00:00",
                "end_date": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "enable_pacing": true,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "lifetime_pacing": false
            }],
            "budget_type": "impression"
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/insertion-order` endpoint with this insertion order JSON and an appropriate `advertiser_id` and `member_id`.

    **Example request: No end date, no budget**

    ```
    $ curl -b cookies -c cookies -X POST -d @insertion-order-noenddate.json 'https://api..com/insertion-order?advertiser_id=2605036&member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the insertion order ID in the response body so you can use it when you create the curated deal line item in [Step 6 - Create a curated deal line item](#step-6---create-a-curated-deal-line-item).

#### JSON fields for seamless insertion order

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `budget_intervals` | array of objects | Required | In order for an insertion order created via the API to be seamless, you must use the `budget_intervals` field. |
| `name` | string | Required | The name of the advertiser |

### Step 4 - Create a deal

You'll need to create the deal you want to associate with the curated deal line item.

To create a deal, do the following (see [Deal Service](./deal-service.md) for more information):

1. Create a deal JSON:

    ```
    $ cat deal.json
    {
        "deal": {
            "name": "Curated Deal",
            "buyer": {
                "id": 2379
            },
            "type": {
                "id": 5,
                "name": "Curated"
            },
            "version": 2
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/deal` endpoint with this deal JSON and an appropriate `member_id`.

    ```
    $ curl -b cookies -c cookies -X POST -d @deal.json 'https://api.appnexus.com/deal?member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the deal ID in the response body so you can use it when you create the deal line item in [Step 6 - Create a curated deal line item](#step-6---create-a-curated-deal-line-item).

#### JSON fields for deal

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `auction_type` | object | Optional | The auction type of the deal (Standard/Fixed/Market). This value must match what's set on the curated deal line item (via `revenue_type`/`min_revenue_value`/`revenue_value`). |
| `buyer` | string | Required | The buyer member ID of the deal. This field cannot be changed after creation. |
| `name` | string | Required | The name of the deal. <br>**Note**: The buyer will see this name. |
| `type` | object | Required | The type of deal. This field must be set to `"5"` for curated deals. |
| `version` | int | Required | This field must be set to `"2"` in order to associate the deal to a curated deal line item. |

#### Useful optional JSON fields

##### JSON fields for allowed creatives

###### Brand (see [Brand Service](./brand-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `brand_restrict` | boolean | - `True`: Deal is restricted only to the listed brands<br> - `False`: Other brands are allowed to serve |
| `brands` | array of objects | Array of eligible brands |
| `id` | int | Field within `brands`: ID of the brand that is eligible for the deal |
| `name` | string | Field within `brands`: Name of the brand that is eligible for the deal |
| `override` | boolean | Field within `brands`: Set to `true` to allow a specific brand to serve for a deal even if the ad quality profile would have blocked it. |

**Brand example**

```
"brand_restrict": true,
            "brands": [
                {
                    "id": 2,
                    "name": "1800Flowers",
                    "override": true
                },
                {
                    "id": 4,
                    "name": "Acura",
                    "override": false
                }
            ] 
```

###### Media type (see [Media Subtype Service](media-subtype-service.md) and [Media Type Service](media-type-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `allowed_media_subtypes` | array of objects | The media subtypes allowed for the deal. |
| `id` | int | Field within `allowed_media_subtypes`: The ID of the media subtype allowed for the deal |
| `allowed_media_types` | array of objects | The media types allowed for the deal |
| `id` | int | Field within `allowed_media_types`: The ID of the media type allowed for the deal |

**Media type example**

```
"allowed_media_subtypes": [
                 {
                     "id": 2,
                     "last_modified": "2015-09-17 19:19:21",
                     "media_type": {
                         "id": 2,
                         "media_type_group_id": 2,
                         "name": "Pop",
                         "uses_sizes": "sometimes"
                     },
                     "name": "Popup",
                     "native_assets": null,
                     "permitted_sizes": null
                 }
             ],
 "allowed_media_types": [
                 {
                     "id": 1,
                     "last_modified": "2012-03-16 21:36:10",
                     "media_type_group_id": 1,
                     "name": "Banner",
                     "uses_sizes": "always"
                 },
                 {
                     "id": 4,
                     "last_modified": "2016-08-22 16:23:12",
                     "media_type_group_id": 1,
                     "name": "Video",
                     "uses_sizes": "never"
                 }
             ]
```

### Step 5 - Create a curated deal line item profile

Next, create a curated deal line item profile to use in targeting with the curated deal line item. Be sure to note the ID for this profile for later use. See [Profile Service](./profile-service.md) for more information.

> [!NOTE]
> You can target sellers' publishers, placements, and categories with a curated deal line item by using following arrays:
>
> - `platform_publisher_targets`
> - `platform_placement_targets`
> - `platform_content_category_targets`.
>
> You cannot use `placement_targets`, `publisher_targets`, or `content_category_targets` with a curated deal line item. See [Profile Service](./profile-service.md) for more information.

To create a curated deal line item profile, do the following (see [Profile Service](./profile-service.md) for more information):

1. Create a curated deal line item profile JSON:

    **Example: Profile creation with country and view rate completion rate thresholds**

    ```
    $ cat profile.json
     
    {
            "profile": {
                    "country_action": "include",
                    "country_targets": [{
                            "active": true,
                            "code": "US",
                            "id": 233,
                            "name": "United States"
                    }],
                    "engagement_rate_targets": [{
                                    "engagement_rate_pct": 25,
                                    "engagement_rate_type": "video_completion"
                            },
                            {
                                    "engagement_rate_pct": 50,
                                    "engagement_rate_type": "predicted_iab_video_view_rate"
                            }
                    ],
                    "platform_publisher_targets": [{
                            "action": "include",
                            "deleted": false,
                            "id": 1238721,
                            "name": "test_publisher"
                    }],
                    "platform_placement_targets": [{
                                    "action": "include",
                                    "deleted": false,
                                    "id": 5126395
                            },
                            {
                                    "action": "include",
                                    "deleted": false,
                                    "id": 5301719
                            }
                    ],
                    "platform_content_category_targets": [{
                            "action": "include",
                            "deleted": false,
                            "id": 19062,
                            "is_system": false,
                            "name": "1"
                    }]
            }
    }
    ```

    **Example: Profile creation without targeting**

    ```
    > cat profile.json
     
    {
        "profile": {
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/profile` endpoint with this curated deal profile JSON and an appropriate `advertiser_id`.

    **Example: Profile creation with country and view rate completion rate thresholds**

    ```
    > curl -b cookies -c cookies -X POST -d @profile.json 'https://api.appnexus.com/profile?advertiser_id=3410892&member_id=2378'
    ```

    **Example: Profile creation without targeting**

    ```
    > curl -b cookies -c cookies -X POST -d @profile.json 'https://api.appnexus.com/profile?advertiser_id=3410892&member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the profile ID in the response body so you can use it when you create the curated deal line item in [Step 6 - Create a curated deal line item](#step-6---create-a-curated-deal-line-item).

#### Optional JSON fields for deal line item profile

There are many optional fields available in the curated deal line item profile for targeting with the curated deal line item. For example, you can target properties associated with inventory, inventory types, allowlists, blocklists, device types, and so forth. See the [Profile Service](./profile-service.md) for more information on available fields.  

### Step 6 - Create a curated deal line item

Finally, you'll need to create the curated deal line item to associate the deal ID and the curated deal line item profile you created in [Step 5 - Create a curated deal line item profile](#step-5---create-a-curated-deal-line-item-profile).

To create a curated deal line item, do the following (see [Line Item Service](./line-item-service---ali.md) for more information):

1. Create a curated deal line item JSON (you'll need an existing advertiser ID, insertion order ID, deal ID, and profile ID).

    **Example JSON: Curated deal line item no budget**

    ```
    > cat curated_deal_line_item.json
    {
            "line-item": {
                    "ad_types": ["video"],
                    "auction_event": {
                            "kpi_auction_type_id": 1,
                            "payment_auction_type_id": 1,
                            "revenue_auction_type_id": 1
                    },
                    "budget_intervals": [{
                            "start_date": "2019-10-11 12:00:00"
                    }],
                    "deals": [{
                            "id": 628539
                    }],
                    "insertion_orders": [{
                            "id": 1363850
                    }],
                    "line_item_subtype": "standard_curated",
                    "name": "Curated Deal Line Item Example Line Item",
                    "revenue_type": "vcpm",
                    "revenue_value": null,
                    "supply_strategies": {
                            "managed": false,
                            "deals": true,
                            "rtb": false
                    },
                    "profile_id": 113067333,
                    "valuation": {
                            "min_revenue_value": 10
                    }
            }
    }
    ```

    **Example JSON: Curated deal line item daily revenue budget**

    ```
    > cat curated_deal_line_item_daily.json
    {
            "line-item": {
                    "ad_types": ["video"],
                    "auction_event": {
                            "kpi_auction_type_id": 1,
                            "payment_auction_type_id": 1,
                            "revenue_auction_type_id": 1
                    },
                    "budget_intervals": [{
                            "daily_budget_imps": 270,
                            "end_date": "2019-10-18 23:59:59",
                            "start_date": "2019-10-11 12:00:00",
                            "timezone": "US/Pacific"
                    }],
                    "deals": [{
                            "id": 618159
                    }],
                    "insertion_orders": [{
                            "id": 1363850
                    }],
                    "line_item_subtype": "standard_curated",
                    "name": "Curated Deal Line Item Example Line Item",
                    "revenue_type": "vcpm",
                    "revenue_value": null,
                    "supply_strategies": {
                            "managed": true,
                            "deals": true,
                            "rtb": false
                    },
                    "profile_id": 113067333,
                    "valuation": {
                            "min_revenue_value": 10
                    }
            }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/line-item` endpoint using this deal line item JSON and an appropriate `advertiser_id`.

    **Example request: Curated deal line item no budget**

    ```
    > curl -b cookies -c cookies -X POST -d @curated_deal_line_item.json 'https://api.appnexus.com/line-item?member_id=2378&advertiser_id=3410892'
    ```

    **Example request: Curated deal line item daily revenue budget**

    ```
    > curl -b cookies -c cookies -X POST -d @curated_deal_line_item_daily.json 'https://api.appnexus.com/line-item?member_id=2378&advertiser_id=3410892'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the line item ID in the response body so you can identify this curated deal line item later to change its `state` (`active` or `inactive`) or modify it.  

#### JSON fields for curated deal line item

| Field | Type | Description |
|:---|:---|:---|
| `insertion_orders` | array | Array containing the insertion order ID you want to associate this curated deal line item to |
| `name` | string | Name of the curated deal line item (Note: the buyer will not see this) |
| `ad_types` | array | The type of creative used for this curated deal line item. Possible values: <br> - `"banner"`<br> - `"video"` (includes audio types as well)<br> - `"native"` |
| `line_item_subtype` | enum | The line item subtype. For curated deal line items, the value for this field must be `"standard_curated"`. See [note for this field](#note-for-line_item_subtype-field). |
| `profile_id` | integer | Profile ID associated with the curated deal line item (see [Step 5 - Create a curated deal line item profile](#step-5---create-a-curated-deal-line-item-profile)) |
| `budget_intervals` | array of objects | Always include a `start_date`. Leave `end_date` `null` for a no end date deal line item. |
| `deals` | array of objects | The `id` field within deals must be the ID of the deal you created in [Step 4 - Create a deal](#step-4---create-a-deal). |
| `supply_strategies` | object | An object containing several boolean fields used to designate which inventory supply sources you would like to target.<br><br>For a curated deal line item, the `managed` field must be set to `false` (this value is assigned when the `"line_item_subtype"` is set to `"standard_curated"`)<br><br>**Note**: The `rtb` and/or `deals` fields must be set to `true` (these fields are not assigned when `"line_item_subtype"` is set to `"standard_curated"`), so you will need to assign these values accordingly.<br><br>**Terminology Note**:<br> - `rtb` refers to Open Exchange Inventory Aggregation<br> - `deals` refers to Rollup Deals |
| `revenue_type` |  enum | `cpm` for Fixed Price (CPM) deal, `vcpm` for Standard Price (Dynamic CPM) deal. |
| `revenue_value` |  double | If you set the `revenue_type` to `cpm` (Fixed), set the fixed price using `revenue_value`. If you're using Standard, set this value to `null`. |
| `valuation` | object | For curated deals, use the following valuation object fields:<br> - `min_revenue_value` <br> - If you set the `revenue_type` to `vcpm` (Standard), set the floor price in `min_revenue_value`.<br> - If you set the `revenue_type` to `cpm` (Fixed), set the value of `min_revenue_value` to `null`. <br><br> - `min_margin_cpm` - Set the margin value in `min_margin_cpm` when using CPM as a margin type.<br><br> - `min_margin_pct` - Set the margin value in `min_margin_pct` when using percentage as a margin type.<br><br>**Note**: The `min_margin_cpm` and `min_margin_pct` fields cannot both be set at the same time. If one is set, the other must be `null`.  |
| `auction_event` | object | Object for auction event type properties: The `kpi_auction_type_id`, `payment_auction_type_id`, and `revenue_auction_type_id` fields of the auction_event object must all be set to `1`. |

##### Note for `line_item_subtype` field

Setting `line_item_subtype` field to `"standard_curated"` will automatically assign the following values to these related fields.

```
"line_item_type": "standard_v2",
"bid_object_type": "deal",
"delivery_model_type": "standard",
"supply_strategies": {
"managed": false,
"programmatic_guaranteed": false
}
```

The `line_item_subtype` field (and associated fields/arrays) cannot be changed after the line item is created.

##### Useful optional JSON fields for curated deal line item

| Field | Type | Description |
|:---|:---|:---|
| `budget_intervals` | array of objects | Set a budget on the deal using fields within `budget_intervals` including: `daily_budget`, `daily_budget_imps`, `lifetime_budget`, or `lifetime_budget_imps`. Use the fields with no imp if the curated deal line item has revenue budget type or the fields with `_imp` at the end if the deal line item has revenue type impression. You can either have a daily or lifetime budget, not both. A lifetime budget that sits across flights ends up being broken out across each flight via the API. Remember that if your deal has no end date, it can't have a budget.  |
| `state` | enum | State of the curated deal line item. Default is `active`, so set to `inactive` if you don't want the deal to go live right away. |

## Related topics

- [API Getting Started](./api-getting-started.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
- [Deal Service](./deal-service.md)
- [Line Item Service (ALI)](./line-item-service---ali.md)
- [Profile Service](./profile-service.md)
