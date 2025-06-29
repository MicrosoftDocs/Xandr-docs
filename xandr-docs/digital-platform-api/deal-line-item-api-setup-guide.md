---
title: Deal Line Item API Setup Guide
description: Learn the process of setting up an API implementation of a Deal Line Item to target a deal.
ms.date: 06/30/2025
ms.custom: digital-platform-api
---

# Deal Line Item API setup guide

Setting up an API implementation of a Deal Line Item to target a deal requires configuring a number of different properties on different API objects. This guide will explain the process of creating and configuring a deal line item using our API.

## Overview

Deal line items are a powerful feature that allows network and publisher clients to better support their buyers by providing prepackaged, user-friendly buying tools.

Setting up a deal line item typically involves making requests to the following API service endpoints to access or create the corresponding API objects:

| API Endpoint | API Object | Detailed Reference |
|:---|:---|:---|
| `https://api.appnexus.com/advertiser` | advertiser | [Advertiser Service](./advertiser-service.md) |
| `https://api.appnexus.com/insertion-order` | insertion-order | [Insertion Order Service](./insertion-order-service.md) |
| `https://api.appnexus.com/deal` | deal | [Deal Service](./deal-service.md) |
| `https://api.appnexus.com/profile` | profile | [Profile Service](./profile-service.md) |
| `https://api.appnexus.com/line-item` | line-item (ALI) | [Line Item - ALI Service](./line-item-service---ali.md) |

This guide uses cURL examples for all requests. You can use other API request tools (e.g., [Postman](https://www.getpostman.com/)), but you’ll then need to adjust the examples accordingly.

## Prerequisites

Before beginning this setup, be sure to read [API Getting Started](./api-getting-started.md). It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices.

## Order of operations

API objects often have dependencies on other API objects and there is an order you must follow in creating or accessing objects when you create a deal line item. For example, you must provide the IDs of the following API objects: <br> - `advertiser` <br> - `insertion-order` <br> - `deal` <br> - `profile`.
<br><br>To obtain the IDs for these objects, you'll need to either create them or already have access to them. The steps in this guide follow the typical order of operations required to create a deal line item.

## Best practices

For a general list of best practices to follow when working with the API, see [API Best Practices](./api-best-practices.md). The following are some best practices that are specific to a deal line item setup:

- Set the `state` field of the deal line item to `"inactive"` until the line item is fully configured and ready for testing.
- Note the ID of any objects you create. The IDs of objects you create are returned in the response body of requests. You'll often need these IDs later so copying them when they're returned can reduce the number of additional `GET` requests you have to make to obtain them.

## Setup procedure

The following steps will guide you through the process of setting up a deal line item with typical configurations:

- [Step 1 - Obtain an authorization token](#step-1---obtain-an-authorization-token)
- [Step 2 - Create or access an advertiser](#step-2---create-or-access-an-advertiser)
- [Step 3 - Create or access an insertion order](#step-3---create-or-access-an-insertion-order)
- [Step 4 - Create a deal](#step-4---create-a-deal)
- [Step 5 - Create a deal line item profile](#step-5---create-a-deal-line-item-profile)
- [Step 6 - Create a deal line item](#step-6---create-a-deal-line-item)

## Authentication

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

1. Check the response body of your request (see **Example Response** below). If your request was successful, you’ll get a "`status`" of “`OK`” and the "`token`" field will be populated with the authentication token value.
   <br><br> **Example response**

    ```
    {
       "response" : {
          "token" : "authn:225692:2d787d1838283:lax1",
          "status" : "OK"      
       }
    }
    ```

## Advertiser

### Step 2 - Create or access an advertiser

You'll need to create or access an advertiser from which to create a deal line item. For deal line items, advertisers are set up the same way as augmented line items.

#### JSON fields for advertiser (required and useful optional fields)

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the advertiser |
| `timezone` | enum | Optional | The timezone of the advertiser. See [API Timezones](./api-timezones.md) for details and accepted values.  |
| `use_insertion_orders` | boolean | Required | This field must be set to `true` in order to create deal line items. |
  
If you don't already have an advertiser to use, create an advertiser by doing the following (see [Advertiser Service](./advertiser-service.md) for more information):

1. Create an advertiser JSON:

    ```
    $ cat advertiser.json
    {
        "advertiser": {
            "name": "Deal Line Item Example Advertiser",
            "timezone": "US/Pacific"
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/advertiser endpoint` with this advertiser JSON and an appropriate `member_id`.

    ```
    $ curl -b cookies -c cookies -X POST -d @advertiser.json 'https://api.appnexus.com/advertiser?member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.  

1. Note the advertiser ID in the response body so you can use it when you create the deal line item in [Step 6 - Create a deal line item](#step-6---create-a-deal-line-item)

## Insertion order

### Step 3 - Create or access an insertion order

You'll need to create or access an insertion order to create a deal line item. Deal line items require a seamless insertion order (see required fields below).

#### JSON fields for seamless insertion order (required and useful optional fields)

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the advertiser |
| `budget_intervals` | array of objects | Required | In order for an insertion order created via the API to be seamless, you must use the `budget_intervals` field. |
| `budget_type` | enum | Optional | Budget type will translate to all deals below the IO. For example, if you set up an Impression Budget Type IO, you can't put deal line items with a Revenue budget below that IO. |
| `daily_budget` | double | Optional | Field within `budget_intervals` you can use to set daily budgets at the insertion order level for Revenue `budget_type`. |
| `lifetime_budget` | double | Optional | Field within `budget_intervals` you can use to set lifetime budgets at the insertion order level for Revenue `budget_type`. |
| `daily_budget_imps` | int | Optional | Field within `budget_intervals` you can use to set daily budgets at the IO level for Impression `budget_type`. |
| `lifetime_budget_imps` | int | Optional | Field within `budget_intervals` you can use to set lifetime budgets at the IO level for Impression `budget_type`. |

If you don't already have an insertion order to use, create an insertion order by doing the following (see [Insertion Order Service](./insertion-order-service.md) for more information):

1. Create an insertion order JSON (two examples are shown below):
  
   **Example JSON: No end date, no budget**

    ```
    $ cat insertion-order-noenddate.json
    {
        "insertion-order": {
            "name": "Deal Line Item Example IO",
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

    **Example JSON: flights, impression budgets**

    ```
    $ cat insertion-order-flights.json
    {
        "insertion-order": {
            "name": "Deal Line Item Example IO",
            "budget_intervals": [
      
                {
                    "start_date": "2019-10-10 00:00:00",
                    "end_date": "2019-10-12 23:59:59",
                    "daily_budget": null,
                    "daily_budget_imps": 10,
                    "enable_pacing": true,
                    "lifetime_budget": null,
                    "lifetime_budget_imps": 980,
                    "lifetime_pacing": false
                },
                {
                    "start_date": "2019-10-13 00:00:00",
                    "end_date": "2019-10-18 23:59:59",
                    "daily_budget": null,
                    "daily_budget_imps": 10,
                    "enable_pacing": true,
                    "lifetime_budget": null,
                    "lifetime_budget_imps": 100,
                    "lifetime_pacing": false
                }
            "budget_type": "impression"
            ]
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/insertion-order` endpoint with this insertion order JSON and an appropriate `advertiser_id` and `member_id`.  

    **Example request: no end date, no budget**

    ```
    $ curl -b cookies -c cookies -X POST -d @insertion-order-noenddate.json 'https://api.appnexus.com/insertion-order?advertiser_id=2605036&member_id=2378'
    ```

    **Example request: flights, impression budgets**

    ```
    $ curl -b cookies -c cookies -X POST -d @insertion-order-flights.json 'https://api.appnexus.com/insertion-order?advertiser_id=2605036&member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the insertion order ID in the response body so you can use it when you create the deal line item in [Step 6 - Create a deal line item](#step-6---create-a-deal-line-item).

## Deal

### Step 4 - Create a deal

You'll need to create the deal you want to associate with the deal line item.

#### JSON fields for deal

| Field | Type | Required or Optional | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the deal <br>**Note**: The buyer will see this name. |
| `buyer` | object | Required | The buying bidder and member who can target this deal. A deal will only ever use the `buyer` field or the `buyer_seats` field, not both. For more details, see the `"Buyer"` section in the [Deal Service](./deal-service.md). |
| `buyer_seats` | object | Required | The buying bidder and seat who can target this deal. A deal will only ever use the buyer field or the `buyer_seats` field, not both. For more details, see the **Buyer Seats** section in the [Deal Service](./deal-service.md). |
| `version` | int | Required | This field must be set to `"2"` in order to associate the deal to a deal line item. |
| `auction_type` | object | Optional | The auction type of the deal (Standard/Fixed/Market). This value must match what's set on the deal line item (via `revenue_type`/`min_revenue_value`/`revenue_value`).<br><br>**Note**: This field must be set upon creation, but it is not used on deal line items. It will not be updated if the line item is updated and in the auction; only the line item values are considered. |
| `priority` | int | Optional | Setting a priority value is optional; however, if it's specified on the Line Item, the same value must also be set in the Deal object. The priority values assigned to the Deal and the corresponding Line Item must be identical.<br> Possible values: 1 - 20, where 20 is the highest priority. <br>Default: 5. <br>**Note**: This setting alone does not determine the PG deal priority; the priority must also be set appropriately when creating the [Line Item](line-item-service.md). |
| `type` | object | Optional | The ID representing the type of deal. <br> Possible values: <br> `1`: Open auction <br> `2`: Private auction <br> Default: `1` <br> **Note**: This setting alone does not determine whether the deal is private or open. Set the `priority` and `deprioritize_rtb` values appropriately when creating the [Line Item](line-item-service.md).

> [!Note]
> Ensure that "ask_price" and "floor_price" are not set in the deal object. These fields would be automatically populated when the deal is associated with the line item.

#### Useful optional JSON fields

##### JSON fields for allowed creatives  

###### Brand (see [Brand Service](./brand-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `brand_restrict` | boolean | `true`: Deal is restricted only to the listed brands<br>`false`: Other brands are allowed to serve |
| `brands` | array of objects | Array of eligible brands |
| `id` | int | Field within `brands`: ID of the brand that is eligible for the deal |
| `name` | string | Field within `brands`: name of the brand that is eligible for the deal |
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

###### Language (see [Language Service](./language-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `language_restrict` | boolean | - `true`: Deal is restricted only to the listed languages<br> - `false`: Other languages are allowed to serve |
| `languages` | array of objects | Array of eligible languages |
| `id` | int | Field within `languages`: ID of the language that is eligible for the deal |
| `name` | string | Field within `languages`: Name of the language that is eligible for the deal |
| `override` | boolean | Field within `languages`: Set to `true` to allow a specific language to serve for a deal even if the ad quality profile would have blocked it. |

**Language example**

```
"language_restrict": true,
            "languages": [
                {
                    "id": 1,
                    "name": "English",
                    "override": false
                },
                {
                    "id": 2,
                    "name": "Chinese",
                    "override": true
                }
            ]
```

###### Trust level

| Field | Type | Description |
|:---|:---|:---|
| `audit_status_option` | string | Specifies how the deal handles creatives.<br> - `max_trust`: Maximum - no ad profile restrictions will be applied to this deal.<br> - `provisional`: Allow pending creatives - creatives in `"pending"` audit status will serve. Once these creatives are audited, the existing ad quality settings are used.<br> - `none`: Default - creatives use existing ad quality settings. |

**Trust level example**  

```
"audit_status_option": "max_trust" 
```

###### Creative category

| Field | Type | Description |
|:---|:---|:---|
| `category_restrict` | boolean | Specifies whether the deal is restricted only to the categories listed in the categories object (see [Deal Service](./deal-service.md)).<br> - `true`: Deal is restricted only to the listed categories.<br> - `false`: Other categories are also allowed to serve. |
| `categories` | array of objects | The categories that describe the creatives that are eligible for the deal. |
| `id` | int | Field within `categories`: ID of the category that is eligible for the deal. |
| `name` | string | Field within `categories`: Name of the category that is eligible for the deal. |
| `override` | boolean | Field within `categories`: Set to `true` to allow a category to serve for a deal even if the ad quality profile would have blocked it. |

**Creative category example**  

```
"categories": [
                 {
                     "id": 1,
                     "name": "Airlines",
                     "override": false
                 },
                 {
                     "id": 2,
                     "name": "Apparel",
                     "override": true
                 }
             ],
             "category_restrict": true
```

###### Specific creatives

| Field | Type | Description |
|:---|:---|:---|
| `creatives` | array of objects | A list of creatives that are specifically approved or banned for the deal. This list overrides any other ad quality setting.  |
| `id` | int | Field within `creatives`: ID of the creative that is approved or banned for the deal. |
| `status` | string | Field within `creatives`: Specifies how this creative will be handled for this deal. <br> - `approved`: This creative can always serve in this deal, regardless of any other ad quality settings or overrides.<br> - `banned`: This creative can never serve in this deal, regardless of any other ad quality settings or overrides. |

**Specific creatives example**  

```
"creatives": [
                {
                    "id": 161501729,
                    "status": "banned"
                },
                {
                    "id": 161501882,
                    "status": "approved"
                }
            ]
```

###### Media type (see [Media Subtype Service](./media-subtype-service.md) and [Media Type Service](./media-type-service.md))

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

###### Technical Attributes (see [Technical Attribute Service](./technical-attribute-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `technical_attribute_restrict` | boolean | Specifies whether the deal is restricted only to the technical attributes listed in the `technical_attributes` object.<br> - `true`: Deal is restricted only to the listed technical attributes.<br> - `false`: Other technical attributes are also allowed to serve. |
| `technical_attributes` | array of objects | The technical attributes of creatives that are eligible for the deal. |
| `id` | int | Field within `technical_attributes`:The ID of the technical attribute that is eligible for the deal |
| `override` | boolean | Field within `technical_attributes`: Set to true to allow a technical attribute to serve for a deal even if the ad quality profile would have blocked it. |

**Technical attributes example**  

```
"technical_attribute_restrict": false,
             "technical_attributes": [
                 {
                     "id": 1,
                     "name": "Image",
                     "override": true
                 }
             ]
```

##### JSON fields for deal data protection (see [Visibility Profile Service](./visibility-profile-service.md))  

> [!WARNING]
> This beta feature is not available for all clients. Reach out to your account manager to discuss if you have a use case.

###### User ID and device ID

| Field | Type | Description |
|:---|:---|:---|
| `expose_device_id_default` | boolean | If `true`, publisher-provided device IDs are passed in your bid requests. |
| `expose_user_id_default` | boolean | If `true`, publisher-provided user IDs are passed in your bid requests. |
| `name` | string | The name of the visibility profile. |

**Protect user ID and device ID example**

**Step 1: Create a visibility profile**

```
> cat visibility_profile.json
{
    "visibility-profile": {
        "expose_device_id_default": false,
        "expose_user_id_default": false,
        "name": "Deal Visibility Profile"
    }
}
 
 
> curl -b cookies -c cookies -X POST -d @visibility_profile.json 'https://api.appnexus.com/visibility-profile?member_id=2378'
```

**Step 2: Associate the visibility profile to the deal and enable data protection**

```
> cat deal_data_protection.json
{
    "deal": {
        "visibility_profile_id": 29657,
        "data_protected": true
    }
}
 
 
> curl -b cookies -c cookies -X PUT -d @deal_data_protection.json 'https://api.appnexus.com/deal?id=549271'
```

###### IP address

| Field | Type | Description |
|:---|:---|:---|
| `expose_ip_default` | boolean | If `true`, publisher-provided IP addresses are passed in your bid requests. |
| `ip_exposure_default` | enum | The visibility of IP addresses in your bid requests.  |
| `name` | string | The name of the visibility profile. |

**Protect IP address example**  

**Step 1: Create a visibility profile**

```
> cat visibility_profile.json
{
    "visibility-profile": {
        "expose_ip_default": false,
        "ip_exposure_default": "truncated",
        "name": "Deal Visibility Profile - Hidden"
    }
}
 
 
> curl -b cookies -c cookies -X POST -d @visibility_profile.json 'https://api.appnexus.com/visibility-profile?member_id=2378'
```

**Step 2: Associate the visibility profile to the deal and enable data protection**

```
> cat deal_data_protection.json
{
    "deal": {
        "visibility_profile_id": 29657,
        "data_protected": true
    }
}
 
 
> curl -b cookies -c cookies -X PUT -d @deal_data_protection.json 'https://api.appnexus.com/deal?id=549271'
```

###### URL

| Field | Type | Description |
|:---|:---|:---|
| `url_exposure_default` | enum | The visibility of inventory URLs in your bid requests. Possible values:<br> - `full` - Full URLs are passed in your bid requests<br> - `domain` - Only domains of URLs are passed in your bid requests<br> - `hidden` - URLs are not passed in your bid requests |

**Protect domain example**  

**Step 1: Create a visibility profile**

```
> cat visibility_profile.json
{
    "visibility-profile": {
        "name": "Deal Visibility Profile - Hidden",
        "url_exposure_default": "hidden"
    }
}
 
 
> curl -b cookies -c cookies -X POST -d @visibility_profile.json 'https://api.appnexus.com/visibility-profile?member_id=2378'
```

**Step 2: Associate the visibility profile to the deal and enable data protection**

```
> cat deal_data_protection.json
{
    "deal": {
        "visibility_profile_id": 29657,
        "data_protected": true
    }
}
 
 
> curl -b cookies -c cookies -X PUT -d @deal_data_protection.json 'https://api.appnexus.com/deal?id=549271'
```

###### Add to Segment (see [Deal Service](./deal-service.md))

| Field | Type | Description |
|:---|:---|:---|
| `allow_creative_add_on_view` | boolean | Set `false` to disallow buyers from adding users to segments on view |
| `allow_creative_add_on_click` | boolean | Set `false` to disallow buyers from adding users to segments on click |

**Prevent adding to segment on click or view example**  

```
> cat add_segment.json
{
    "deal": {
        "allow_creative_add_on_click": false,
        "allow_creative_add_on_view": false
    }
}
 
 
> curl -b cookies -c cookies -X PUT -d @add_segment.json 'https://api.appnexus.com/deal?id=123456'
```

**To create a deal, do the following (see [Deal Service](./deal-service.md) for more information):**

1. Create a deal JSON:

    ```
    $ cat deal.json
    {
        "deal": {
            "name": "Deal Line Item Example Deal",
            "buyer": {
                "id": 2379
            },
            "version": 2
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/deal` endpoint with this deal JSON and an appropriate `member_id`.

    ```
    $ curl -b cookies -c cookies -X POST -d @deal.json 'https://api.appnexus.com/deal?member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the deal ID in the response body so you can use it when you create the deal line item in [Step 6 - Create a deal line item](#step-6---create-a-deal-line-item).

## Profile

### Step 5 - Create a deal line item profile

Next, create a deal line item profile to use in targeting with the deal line item. Be sure to note the ID for this profile for later use. See [Profile Service](./profile-service.md) for more information.

#### Optional JSON fields for deal line item profile

There are many optional fields available in the deal line item profile for targeting with the deal line item. For example, you can target properties associated with inventory, inventory types, allowlists, blocklists, device types, and so forth. See the [Profile Service](./profile-service.md) for more information on available fields.  

To create a deal line item profile, do the following (see [Profile Service](./profile-service.md) for more information):

1. Create a deal line item profile JSON:

   **Example: Profile creation with country, frequency/recency caps, and view rate/completion rate thresholds**

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
            "max_day_imps": 10,
            "min_minutes_per_imp": 300
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

1. Make a **`POST`** request to the `https://api.appnexus.com/profile` endpoint with this deal profile JSON and an appropriate `advertiser_id`.  

    **Example: Profile creation with country, frequency recency caps, and view rate/completion rate thresholds**

    ```
    > curl -b cookies -c cookies -X POST -d @profile.json 'https://api.appnexus.com/profile?advertiser_id=3410892&member_id=2378'
    ```

    **Example: Profile creation without targeting**

    ```
    > curl -b cookies -c cookies -X POST -d @profile.json 'https://api.appnexus.com/profile?advertiser_id=3410892&member_id=2378'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.  

1. Note the profile ID in the response body so you can use it when you create the deal line item in [Step 6 - Create a deal line item](#step-6---create-a-deal-line-item).

## Line Item

### Step 6 - Create a deal line item

Finally, you'll need to create the deal line item to associate the deal ID and the deal line item profile you created in [Step 5 - Create a deal line item profile](#step-5---create-a-deal-line-item-profile).

#### JSON fields for deal line item

| Field | Type | Description |
|:---|:---|:---|
| `insertion_orders` | array | Array containing the insertion order ID you want to associate this deal line item to. |
| `name` | string | Name of the deal line item <br>**Note**: The buyer will not see this. |
| `ad_types` | array | The type of creative used for this deal line item.  Possible values: <br> - `"banner"`<br> - `"video"` (includes audio types as well)<br> - `"native"` |
| `line_item_type` | enum | Must be set to `"standard_v2"` to create a deal line item. |
| `profile_id` | integer | Profile ID associated with the deal line item ([Step 5 - Create a deal line item profile](#step-5---create-a-deal-line-item-profile)) |
| `budget_intervals` | array of objects | Always include a `start_date`. Leave `end_date` `null` for a no end date deal line item. |
| `deals` | array of objects | The `id` field within deals must be the ID of the deal you created in [Step 4 - Create a deal](#step-4---create-a-deal).|
| `supply_strategies` | object | An object containing several boolean fields used to designate which inventory supply sources you would like to target.<br>For a deal line item, the `managed` field must be set to `true`. The `rtb`, `programmatic_guaranteed`, and `deals` fields must be set to `false`.  |
| `revenue_type` |  enum | `cpm` for Fixed Price (CPM) deal, `vcpm` for Standard Price (Dynamic CPM) and Market Price deal. |
| `revenue_value` |  double | If you set the `revenue_type` to `cpm` (Fixed), set the fixed price using `revenue_value`. If you're using Standard or Market Price, set this value to `null`. |
| `valuation` | object | If you set the `revenue_type` to `vcpm` (Standard), set the floor price using `min_revenue_value` in the valuation object. If you're using `cpm` (Fixed) or Market Price, set the value of `min_revenue_value` `null`. |
| `auction_event` | object | Object for auction event type properties: The `kpi_auction_type_id`, `payment_auction_type_id`, and `revenue_auction_type_id` fields of the `auction_event` object must all be set to `1`. |
| `bid_object_type` | enum | Must be set to `"deal"` for a deal line item. |

#### Useful optional JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `priority` | int | Set the priority of the PG deal. This priority value, in combination with the field `deprioritize_rtb` , determines whether a PG deal is auctioned as open or private. <br> To create an **open PG deal**, set a priority below the Member's Reselling Priority. <br> To create a **private PG deal**, set a priority below the Member's Reselling Priority if the member id is also creating GDALIs (Ad Sever clients); or set a priority above or equal to the Member's Reselling Priority if your member id is not creating GDALIs (SSP clients).|
| `deprioritize_rtb` | boolean | If set to `true`, the PG deal is considered private and always would has priority over open deals and open RTB bids. <br> If set to `false`, the PG deal is considered open and competes on price with open deals at the same priority and open RTB bids. <br> Check the [Auction Logic for Deals](../monetize/deal-auction-mechanics.md) for further details.|
| `budget_intervals` | array of objects | Set a budget on the deal using fields within `budget_intervals` including: `daily_budget`, `daily_budget_imps`, `lifetime_budget`, or `lifetime_budget_imps`. Use the fields with no `imp` if the deal line item has revenue budget type or the fields with `_imp` at the end if the deal line item has revenue type impression. You can either have a daily or lifetime budget, not both. A lifetime budget that sits across flights ends up being broken out across each flight via the API. Remember that if your deal has no end date, it can't have a budget.  |
| `state` | enum | State of the deal line item. Default is `active`, so set to `inactive` if you don't want the deal to go live right away. |


**To create a deal line item, do the following (see [Line Item Service](./line-item-service---ali.md) for more information):**

1. Create a deal line item JSON (you'll need an existing advertiser ID, insertion order ID, deal ID, and profile ID).

    **Example JSON: Deal line item no budget**

    ```
    > cat deal_line_item.json
    {
        "line-item": {
            "ad_types": ["video"],
            "auction_event": {
                "kpi_auction_type_id": 1,
                "payment_auction_type_id": 1,
                "revenue_auction_type_id": 1
            },
            "bid_object_type": "deal",
            "budget_intervals": [{
                "start_date": "2019-10-11 12:00:00"
            }],
            "deals": [{
                "id": 618159
            }],
            "insertion_orders": [{
                "id": 1363850
            }],
            "line_item_type": "standard_v2",
            "name": "Deal Line Item Example Line Item",
            "revenue_type": "vcpm",
            "revenue_value": null,
            "supply_strategies": {
                "managed": true
            },
            "profile_id": 112548354,
            "valuation": {
                "min_revenue_value": 10
            }
        }
    }
    ```

    **Example JSON: Deal line item lifetime impression budget**

    ```
    > cat deal_line_item_lifetime.json
    {
        "line-item": {
            "ad_types": ["video"],
            "auction_event": {
                "kpi_auction_type_id": 1,
                "payment_auction_type_id": 1,
                "revenue_auction_type_id": 1
            },
            "bid_object_type": "deal",
            "budget_intervals": [
                    {
                        "end_date": "2019-10-18 23:59:59",
                        "lifetime_budget_imps": 2586,
                        "start_date": "2019-10-11 12:00:00",
                        "timezone": "US/Pacific"
                    },
                    {
                        "end_date": "2019-10-25 23:59:59",
                        "lifetime_budget_imps": 2414,
                        "start_date": "2019-10-19 00:00:00",
                        "timezone": "US/Pacific"
                    }
                ],
            "deals": [{
                "id": 618159
            }],
            "insertion_orders": [{
                "id": 1363850
            }],
            "line_item_type": "standard_v2",
            "name": "Deal Line Item Example Line Item",
            "revenue_type": "vcpm",
            "revenue_value": null,
            "supply_strategies": {
                "managed": true
            },
            "profile_id": 112548354,
            "valuation": {
                "min_revenue_value": 10
            }
        }
    }
    ```

    **Example JSON: Deal line item daily revenue budget**

    ```
    > cat deal_line_item_daily.json
    {
        "line-item": {
            "ad_types": ["video"],
            "auction_event": {
                "kpi_auction_type_id": 1,
                "payment_auction_type_id": 1,
                "revenue_auction_type_id": 1
            },
            "bid_object_type": "deal",
            "budget_intervals": [
                    {
                        "daily_budget_imps": 270,
                        "end_date": "2019-10-18 23:59:59",
                        "start_date": "2019-10-11 12:00:00",
                        "timezone": "US/Pacific"
                    }
                ],
            "deals": [{
                "id": 618159
            }],
            "insertion_orders": [{
                "id": 1363850
            }],
            "line_item_type": "standard_v2",
            "name": "Deal Line Item Example Line Item",
            "revenue_type": "vcpm",
            "revenue_value": null,
            "supply_strategies": {
                "managed": true
            },
            "profile_id": 112548354,
            "valuation": {
                "min_revenue_value": 10
            }
        }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/line-item` endpoint using this deal line item JSON and an appropriate `advertiser_id` and `member_id`.

     **Example request: Deal line item no budget**

    ```
    > curl -b cookies -c cookies -X POST -d @deal_line_item.json 'https://api.appnexus.com/line-item?member_id=2378&advertiser_id=3410892'
    ```

     **Example request: Deal line item lifetime impression budget**

    ```
    > curl -b cookies -c cookies -X POST -d @deal_line_item_lifetime.json 'https://api.appnexus.com/line-item?member_id=2378&advertiser_id=3410892'
    ```

     **Example request: Deal line item daily revenue budget**

    ```
    > curl -b cookies -c cookies -X POST -d @deal_line_item_daily.json 'https://api.appnexus.com/line-item?member_id=2378&advertiser_id=3410892'
    ```

1. Check the response body of your request. If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

1. Note the line item ID in the response body so you can identify this deal line item later to change its `state` (`active` or `inactive`) or modify it.

## Related topics

- [API Getting Started](./api-getting-started.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
- [Deal Service](./deal-service.md)
- [Line Item Service (ALI)](./line-item-service---ali.md)
- [Profile Service](./profile-service.md)
