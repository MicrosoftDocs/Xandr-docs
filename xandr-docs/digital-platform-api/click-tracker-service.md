---
title: Click Tracker Service
description: In this article, learn about the Click Tracker service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Click Tracker service

The Click Tracker Service gives you a way to track user clicks on creatives served by third-party ad servers (versus those served by Xandr). Here's how it works:

1. You use the Click Tracker Service to create a click tracker. The click tracker specifies the line item and publisher to which the click tracker is associated. Generally, it also specifies the target landing page URL for the creative (see the `redir` parameter below for the alternate case). Optionally, it can include the specific placement or payment rule to which it is associated.
1. You create the URL to the click tracker and ask the ad server to use it as the creative's landing page URL. The click tracker URL must be formatted as `https://ib.adnxs.com/clktr?id=12345`, where 12345 is the click tracker ID.
1. When the ad server serves the creative and someone clicks on it, the call first goes to `ib.adnxs.com`, where Xandr records the click, and is then redirected to the target landing page.

For specific usage examples, see [Examples](#examples).

## Query string parameters

The following parameters can be passed to Xandr in the query string of the click tracker URL:

| Parameter | Description |
|:---|:---|
| `cachebuster` | Prevents the user's browser from caching the click tracker URL. This parameter can be populated by the third-party ad server. |
| `ancost` | The media cost you paid for the external click. The parameter can be populated by the third-party ad server. It can pass a maximum value of "999999.999999". |
| `redir` | The redirect URL. If `click_url` is not set in the click tracker, you must use this parameter to pass the target landing page URL that Xandr will redirect to once the click has been recorded. |

### Example

```
https://ib.adnxs.com/clktrb?id=1234&cachebuster=[CACHEBUSTER]&ancost=[ANCOST]&redir=https://test-landing-page.com
```

### Reporting

You can use the `clicktrackers` [Bulk Reporting Feed](bulk-reporting-feeds.md) to view the data that your external click trackers passed to Xandr, such as click time, the associated Xandr objects, and the amount paid for the external click. For an even deeper view of your external clicks, you can use the `clicktrackers` feed in combination with the [Advertiser Attributed Conversions](advertiser-attributed-conversions.md) report.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/clicktracker?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/clicktracker?advertiser_id=ADVERTISER_ID) | Add a click tracker. |
| `GET` | [https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID](https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID) | View a click tracker. |
| `GET` | [https://api.appnexus.com/clicktracker?id=1,2,3](https://api.appnexus.com/clicktracker?id=1,2,3) | View multiple click trackers by ID using a comma-separated list. |
| `PUT` | [https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID](https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID) | Modify a click tracker. |
| `DELETE` | [https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID](https://api.appnexus.com/clicktracker?id=CLICK_TRACKER_ID) | Delete a click tracker. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the click tracker.<br>- **Default:** Auto-incremented number (i.e., 123).<br> - **Required On:** `PUT`/`DELETE`, in query string. |
| `member_id` | int | The ID of the member to which the advertiser belongs.<br>**Read Only.** |
| `advertiser_id` | int | The ID of the advertiser that owns the click tracker.<br>**Required On:** `POST`, in query string. |
| `name` | string | The name for the click tracker.<br>**Required On:** `POST` |
| `code` | string | The custom code for the click tracker. |
| `state` | enum | The state of the click tracker. Possible values: `"active"` or `"inactive"`.<br>**Default:** `active` |
| `click_url` | string | The target landing page for the creative. Once Xandr has recorded a click on the creative, this is the page that Xandr will redirect to.<br><br>**Tip:** If this field is not set, the target landing page URL must be passed as the "redir" parameter in the query string of the click tracker URL. For more details, see [Query String Parameters](#query-string-parameters) above. |
| `publisher` | object | The publisher to which the click tracker is associated. For more details, see [Publisher](#publisher) below.<br>**Required On:** `POST` |
| `line_item` | object | The advertiser line item to which the click tracker is associated. For more details, see [Line Item](#line-item) below.<br>**Required On:** `POST` |
| `tag` | array | The placement to which the click tracker is associated. For more details, see [Tag](#tag) below. |
| `payment_rule` | array | The payment rule to which the click tracker is associated. For more details, see [Payment Rule](#payment-rule) below. |
| `last_modified` | timestamp | The date and time when the click tracker was last modified.<br>**Read Only.** |

### Publisher

You can use the [Publisher Service](publisher-service.md) to get information about publishers.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the publisher to which the click tracker is associated. |
| `name` | string | The name of the publisher to which the click tracker is associated.<br>**Read Only.** |

### Line Item

You can use the [Line Item Service](line-item-service.md) to get information about line items.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item to which the click tracker is associated. |
| `name` | string | The name of the line item to which the click tracker is associated.<br>**Read Only.** |

### Tag

You can use the [Placement Service](placement-service.md) to get information about placements.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the placement to which the click tracker is associated. |
| `name` | string | The name of the placement to which the click tracker is associated.<br>**Read Only.** |

### Payment rule

You can use the [Payment Rule Service](payment-rule-service.md) to get information about payment rules.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the payment rule to which the click tracker is associated. |
| `name` | string | The name of the payment rule to which the click tracker is associated.<br>**Read Only.** |

## Examples

### Create a new click tracker

```
$ cat clicktracker

{
    "clicktracker": {
        "name": "Test Click Tracker",
        "click_url": "https://test-landing-page.com",
        "publisher": {
            "id": 44449
        },
        "line_item": {
            "id": 74957
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @clicktracker 'https://api.appnexus.com/clicktracker?advertiser_id=37236'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1425,
        "start_element": 0,
        "num_elements": 100,
        "clicktracker": {
            "id": 1425,
            "member_id": 958,
            "advertiser_id": 37236,
            "name": "Test Click Tracker",
            "code": null,
            "state": "active",
            "click_url": "https://test-landing-page.com",
            "last_modified": "2012-01-10 16:02:15",
            "publisher": {
                "id": 44449,
                "name": "November Publisher"
            },
            "tag": null,
            "payment_rule": null,
            "line_item": {
                "id": 74957,
                "name": "Test Line Item"
            }
        }
    }
}
```

### Update a click tracker

In this example, the `PUT` request associates a placement to click tracker 1425.

```
$ cat clicktracker_update
{
    "clicktracker": {
        "tag": {
            "id": 474412
        }
    }
}

$ curl -b cookies -c cookies -X PUT -d @clicktracker_update 'https://api.appnexus.com/clicktracker?id=1425'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "1425",
        "start_element": 0,
        "num_elements": 100,
        "clicktracker": {
            "id": 1425,
            "member_id": 958,
            "advertiser_id": 37236,
            "name": "Test Click Tracker",
            "code": null,
            "state": "active",
            "click_url": "https://test-landing-page.com",
            "last_modified": "2012-01-10 16:10:12",
            "publisher": {
                "id": 44449,
                "name": "November Publisher"
            },
            "tag": {
                "id": 474412,
                "name": "[Demo Publisher] - Default"
            },
            "payment_rule": null,
            "line_item": {
                "id": 74957,
                "name": "Test Line Item"
            }
        }
    }
}
```

### View click tracker 582

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/clicktracker?id=582'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "clicktracker": {
            "id": 582,
            "member_id": 1066,
            "advertiser_id": 35081,
            "name": "Test Click Tracker 1",
            "code": null,
            "state": "active",
            "click_url": "https://test-landing-page.com",
            "last_modified": "2012-02-28 19:06:01",
            "publisher": {
                "id": 89287,
                "name": "Test Publisher 1"
            },
            "tag": null,
            "payment_rule": null,
            "line_item": {
                "id": 31189,
                "name": "Test Line Item 1"
            }
        }
    }
}
```

### View all click trackers for advertiser 35081

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/clicktracker?advertiser_id=35081'

{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "clicktrackers": [
            {
                "id": 582,
                "member_id": 1066,
                "advertiser_id": 35081,
                "name": "Test Click Tracker 1",
                "code": null,
                "state": "active",
                "click_url": "https://test-landing-page.com",
                "last_modified": "2012-02-28 19:06:01",
                "publisher": {
                    "id": 89287,
                    "name": "Test Publisher 1"
                },
                "tag": null,
                "payment_rule": null,
                "line_item": {
                    "id": 31189,
                    "name": "Test Line Item 1"
                }
            },
            {
                "id": 584,
                "member_id": 1066,
                "advertiser_id": 35081,
                "name": "Test Click Tracker 2",
                "code": null,
                "state": "active",
                "click_url": "https://another-landing-page.com",
                "last_modified": "2012-02-28 19:40:48",
                "publisher": {
                    "id": 89288,
                    "name": "Test Publisher 2"
                },
                "tag": null,
                "payment_rule": null,
                "line_item": {
                    "id": 31190,
                    "name": "Test Line Item 2"
                }
            }
        ]
    }
}
```
