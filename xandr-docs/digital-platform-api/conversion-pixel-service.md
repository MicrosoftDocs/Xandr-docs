---
title: Conversion Pixel Service
description: In this article, learn about the Conversion Pixel service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Conversion Pixel service

The Pixel Service can be used to create **conversion pixels** to place on advertiser pages to track both view and click-based conversions.

> [!NOTE]
> Once you have a conversion pixel ID, the basic format of an image conversion pixel is `<img src="media/px?id=37&t=2" width="1" height="1" />`.
> [!TIP]
> Segment pixels are created separately via the [Segment Service](segment-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/pixel](https://api.appnexus.com/pixel) | View all conversion pixels. |
| `GET` | [https://api.appnexus.com/pixel?id=123,456,789](https://api.appnexus.com/pixel?id=123,456,789) | View an array of specific conversion pixels. |
| `GET` | [https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID) | View all conversion pixels for one of your advertisers. |
| `GET` | [https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE) | View all conversion pixels for one of your advertisers. |
| `GET` | [https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID](https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID) | View a particular conversion pixel for one of your advertisers. |
| `GET` | [https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE&code=PIXEL_CODE](https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE&code=PIXEL_CODE) | View a particular conversion pixel for one of your advertisers. |
| `GET` | [https://api.appnexus.com/pixel/meta](https://api.appnexus.com/pixel/meta) | Find out which fields you can filter and sort by. |
| `POST` | [https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID) | Add a new conversion pixel to one of your advertisers. |
| `POST` | [https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE) | Add a new conversion pixel to one of your advertisers. |
| `PUT` | [https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID](https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID) | Modify an existing conversion pixel. |
| `PUT` | [https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE&code=PIXEL_CODE](https://api.appnexus.com/pixel?advertiser_code=ADVERTISER_CODE&code=PIXEL_CODE) | Modify an existing conversion pixel. |
| `DELETE` | [https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID](https://api.appnexus.com/pixel?advertiser_id=ADVERTISER_ID&id=PIXEL_ID) | Delete an existing conversion pixel.<br><br>**Note:** You cannot delete a pixel that is used by one or more line items. You must [edit the line item](line-item-service.md) to remove the conversion pixel first. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser that owns the pixel.<br>**Required On:** `POST` |
| `campaigns` | array | The campaigns with which the pixel is associated. For details about the fields in this array, see [Campaigns](#campaigns) below. <br>**Read Only.** |
| `code` | string | The custom code for the pixel. |
| `created_on` | timestamp | The date and time when the pixel was created.<br>**Read Only.** |
| `id` | int | The internal ID associated with the pixel.<br>**Required On:** `PUT` |
| `name` | string | The name of the pixel.<br>**Required On:** `POST` |
| `last_modified` | timestamp | The date and time when the pixel was last modified.<br>**Read Only.** |
| `line_items` | array | The line items with which the pixel is associated. For details about the fields in this array, see [Line Items](#line-items) below.<br>**Read Only.** |
| `min_minutes_per_conv` | int | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br> - If set to `0`: count all conversions.<br> - If set to `null` (default): Count one per user.<br>**Default:** `null` |
| `piggyback_pixels` | array of objects | The URLs of the pixels you want us to fire when the conversion pixel fires. For details, see [Piggyback Pixels](#piggyback-pixels) below. |
| `pixel_conversion_event` | array | The pixel conversion event category with which the pixel is associated. For details, see [Pixel Conversion Event](#pixel-conversion-event) below.<br>**Read Only.** |
| `pixel_conversion_event_id` | enum | Optional. The ID of the conversion event associated with the pixel. Setting an event category will not affect our optimization algorithms immediately. Instead, it provides our optimization team with valuable data for prediction that we can start to test and incorporate. If you don't see a good match for your type of conversion event, leave this field blank.<br>Possible values are:<br> - `null`: No category selected.<br> - `2`: **Visit landing page** - A user visits your website after being served an ad.<br> - `3`: **Item view** - A user visits a page on your website that displays one or more products or services.<br> - `4`: **Add to cart** - A user adds one or more of your products or services to their shopping cart.<br> - `5`: **Initiate checkout** - A user begins the checkout process.<br> - `6`: **Add payment info** - A user adds payment information, such as a credit card number, during the checkout process.<br> - `7`: **Purchase** - A confirmed sale of your product or service.<br> - `8`: **Generate lead** - Collect lead information, such as email addresses or zip codes, from people interested in your business. |
| `post_click_expire_mins` | int | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `129600` (90 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_click_value` | double | The value you attribute to a conversion after a click. |
| `post_view_expire_mins` | int | The interval (in minutes) from impression time allowed for a view conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | double | The value you attribute to a conversion after a view. |
| `state` | enum | The state of the pixel. <br>Possible values: `"active"` or `"inactive"`. |
| `trigger_type` | enum | The type of event required for a valid (attributed) conversion. Possible values: `view`, `click`, or `hybrid`.<br>**Default:** `click` |

### Campaigns

This array shows you the campaign associations. To associate a pixel to a campaign, use the [Campaign Service](campaign-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | The ID of the campaign.<br>**Read Only.** |

### Line items

This array shows you the line item associations. To associate a pixel to a line item, use the [Line Item Service](line-item-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | The ID of the line item.<br>**Read Only.** |
| `name` | string | The name of the line item.<br>**Read Only.** |
| `state` | enum | The state of the line item. <br>Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |

### Piggyback pixels

Each object in the `piggyback_pixels` array contains the following fields.

When adding piggyback pixels, keep the following in mind:

- Image pixels can only piggyback off other image pixels, and JavaScript pixels can only piggyback other JavaScript pixels.
- Image pixels can only have one piggyback pixel. If you need to piggyback multiple pixels, be sure to use a JavaScript pixel.
- There are no character limits to piggybacked pixels in AppNexus, but browser/server URL limits may apply.

| Field | Type (length) | Description |
|:---|:---|:---|
| `pixel_type` | enum | The type of the pixel to piggyback. <br>Possible values: `"js"` or `"img"`. |
| `url` | string (255) | The URL of the pixel to piggyback. |

### Pixel conversion event

| Field | Type | Description |
|:---|:---|:---|
| `id` | enum | The ID of the conversion event optionally associated with this pixel. Possible values are integers between 2 and 8, which are associated with the `name` values below.<br> - `null`: No category selected.<br> - `2`: **LandingPage** - A user visits your website after being served an ad.<br> - `3`: **ItemView** - A user visits a page on your website that displays one or more products or services.<br> - `4`: **AddToCart** - A user adds one or more of your products or services to their shopping cart.<br> - `5`: **InitiateCheckout** - A user begins the checkout process.<br> - `6`: **AddPaymentInfo** - A user adds payment information, such as a credit card number, during the checkout process.<br> - `7`: **Purchase** - A confirmed sale of your product or service.<br> - `8`: **Lead** - Collect lead information, such as email addresses or zip codes, from people interested in your business.<br>**Read Only.** |
| `name` | enum | The name of the conversion event optionally associated with this pixel. Possible values are associated with the `id` values above:<br> - `null`: No category selected.<br> - `2`: **LandingPage** - A user visits your website after being served an ad.<br> - `3`: **ItemView** - A user visits a page on your website that displays one or more products or services.<br> - `4`: **AddToCart** - A user adds one or more of your products or services to their shopping cart.<br> - `5`: **InitiateCheckout** - A user begins the checkout process.<br> - `6`: **AddPaymentInfo** - A user adds payment information, such as a credit card number, during the checkout process.<br> - `7`: **Purchase** - A confirmed sale of your product or service.<br> - `8`: **Lead** - Collect lead information, such as email addresses or zip codes, from people interested in your business.<br>**Read Only.** |

## Examples

### Add a conversion pixel for advertiser 2

```
$ cat pixel

{
    "pixel": {
        "min_minutes_per_conv": 120,
        "name": "ProStarr Post View Pixel 2",
        "piggyback_pixels": [
            {
                "pixel_type": "img",
                "url": "https://www.testing.com"
            }
        ],
        "post_view_expire_mins": 3600,
        "post_view_value": 1,
        "state": "active",
        "trigger_type": "view"
    }
}

$ curl -b cookies -c cookies -X POST -d @pixel 'https://api.appnexus.com/pixel?advertiser_id=2'

{
   "response":{
      "status":"OK",
      "id":17
   }
}
```

### View conversion pixel 17 for advertiser 2

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/pixel?id=17&advertiser_id=2'

{
    "response": {
        "status": "OK",
        "pixels": [
            {
                "id": 17,
                "code": null,
                "name": "ProStarr Hybrid Pixel",
                "state": "active",
                "campaigns": [
                    {
                        "id": "17607"
                    }
                ],
               "line_items": [
                    {
                        "id": 382,
                        "name": "Line Item",
                        "state": "active"
                    }
                ],
                "trigger_type": "hybrid",
                "min_minutes_per_conv": null,
                "post_view_expire_mins": null,
                "post_click_expire_mins": null,
                "post_click_value": 10,
                "post_view_value": 1,
                "piggyback_pixels": [
                    {
                        "url": "https://www.testing.com",
                        "pixel_type": "img"
                    }
                ],
                "created_on": "2010-01-01 19:24:20",
                "last_modified": "2010-01-15 21:41:40",
                "advertiser_id": 2
            }
        ]
    }
}
```

### View conversion pixels for all advertisers

> [!NOTE]
> `"advertiser_id"` field tells you the advertiser to which the pixel belongs.

```
$ curl -b cookies -c cookies -X POST -d @pixel 'https://api.appnexus.com/pixel'

{
    "response": {
        "status": "OK",
        "pixels": [
            {
                "id": 5,
                "code": null,
                "name": "Sample Pixel 1",
                "state": "active",
                "campaigns": [
                    {
                        "id": "17883"
                    },
                    {
                        "id": "34091"
                    }
                ],
                "line_items": [
                    {
                        "id": 67729,
                        "name": "5556",
                        "state": "active"
                    },
                    {
                        "id": 67734,
                        "name": "7017",
                        "state": "active"
                    },
                    {
                        "id": 67733,
                        "name": "8302",
                        "state": "active"
                    }
                ],
                "trigger_type": "view",
                "min_minutes_per_conv": 32767,
                "post_view_expire_mins": 1440,
                "post_click_expire_mins": null,
                "post_click_value": null,
                "post_view_value": 0,
                "piggyback_pixels": [
                    {
                        "url": "https://test.com/test",
                        "pixel_type": "img"
                    }
                ],
                "created_on": "2011-08-12 18:11:13",
                "last_modified": "2011-09-12 19:55:21",
                "advertiser_id": 8
            },
            {
                "id": 6,
                "code": null,
                "name": "blargh2",
                "state": "active",
                "campaigns": [
                    {
                        "id": "17775"
                    },
                    {
                        "id": "17776"
                    }
                ],
                "line_items": [
                    {
                        "id": 67895,
                        "name": "7082",
                        "state": "active"
                    },
                    {
                        "id": 67477,
                        "name": "3468",
                        "state": "active"
                    },
                    {
                        "id": 67679,
                        "name": "7870",
                        "state": "active"
                    }
                ],
                "trigger_type": "click",
                "min_minutes_per_conv": 1,
                "post_view_expire_mins": null,
                "post_click_expire_mins": 20160,
                "post_click_value": 0,
                "post_view_value": null,
                "piggyback_pixels": null,
                "created_on": "2011-05-07 18:11:13",
                "last_modified": "2011-06-07 20:23:08",
                "advertiser_id": 10
            },
            ...
        ],
        "count": 10,
        "start_element": null,
        "num_elements": null
    }
}
```

### Add a conversion event category to a pixel

This example adds conversion pixel 1017110 to event category 3 (viewing an item).

```
$ cat pixel-category

{
    "pixel": 
        {"pixel_conversion_event_id": 3
        }
}

$ curl -b cookies -c cookies -X PUT -s -d @pixel-category "https://api.appnexus.com/pixel?id=1017110&advertiser_id=57992"  

{
    "response": {
        "count": 1,
        "dbg_info": {
            "output_term": "pixel",
            "version": "1.18.651",
            "warnings": []
        },
        "id": "1017110",
        "num_elements": 100,
        "pixel": {
            "advertiser_id": 57992,
            "campaigns": null,
            "code": null,
            "created_on": "2018-07-25 18:39:30",
            "id": 1017110,
            "last_modified": "2018-07-27 20:55:31",
            "line_items": null,
            "member_id": 1370,
            "min_minutes_per_conv": 0,
            "name": "Confirmation Page",
            "piggyback_pixels": null,
            "pixel_conversion_event": {
                "id": 3,
                "name": "ItemView"
            },
            "pixel_conversion_event_id": 3,
            "post_click_expire_mins": 20160,
            "post_click_value": null,
            "post_view_expire_mins": 10080,
            "post_view_value": null,
            "state": "active",
            "trigger_type": "hybrid"
        },
        "start_element": 0,
        "status": "OK"
    }
}
```
