---
title: Impression Tracker Service
description: Learn about the Impression Tracker service, its JSON fields, and methods for tracking impressions with third-party ad servers, along with detailed examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Impression Tracker service

The Impression Tracker Service gives you a way to track impressions for creatives served by third-party ad servers (rather than by AppNexus).

Here's how it works:

1. You use the Impression Tracker Service to create an impression tracker. The impression tracker specifies the line item and publisher to which it is associated. Optionally, it can include the specific placement or payment rule to which it is associated.
1. You create an image or JavaScript tag with the URL to the impression tracker and ask the ad server to use it as a piggyback pixel for the creative. The impression tracker URL must be formatted as [https://ib.adnxs.com/imptr?id=12345&t=2](https://ib.adnxs.com/imptr?id=12345), where 12345 is the impression tracker ID and "t" represents the pixel type (where t=1 is for javascript and t=2 is for image).
1. When the ad server serves the creative, the tracker calls `ib.adnxs.com`, and AppNexus records the impression.

## Query string parameters

The following parameters can be passed to AppNexus in the query string of the impression tracker URL:

| Parameter | Description |
|:---|:---|
| `cachebuster` | Prevents the user's browser from caching the impression tracker URL. This parameter can be populated by the third-party ad server. |
| `ancost` | The media cost you paid for the impression. The parameter can be populated by the third-party ad server. |
| `redir` | The redirect URL that AppNexus will redirect to once the impression has been recorded. |

### Image tag example

```
<!-- Imp Tracker - Test Impression Tracker - DO NOT MODIFY -->
<img src="media/imptr?id=531&cachebuster=[CACHEBUSTER]&ancost=[ANCOST]" width="1" height="1" />
<!-- End of Imp Tracker -->
```

### JavaScript tag example

```
<!-- Imp Tracker - Test Impression Tracker - DO NOT MODIFY -->
<script src="https://ib.adnxs.net/imptr?id=531&cachebuster=[CACHEBUSTER]&ancost=[ANCOST]" type="text/javascript"></script>
<!-- End of Imp Tracker -->
```

## Reporting

You can report on your external impressions using the [Network Analytics](network-analytics.md), [Network Publisher Analytics](network-publisher-analytics.md), and [Publisher Analytics](publisher-analytics.md) reports.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/imptracker?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/imptracker?advertiser_id=ADVERTISER_ID)<br>(imptracker JSON) | Add an impression tracker. |
| `PUT` | [https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID](https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID)<br>(imptracker JSON) | Modify an impression tracker. |
| `GET` | [https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID](https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID) | View an impression tracker. |
| `GET` | [https://api.appnexus.com/imptracker?id=1,2,3](https://api.appnexus.com/imptracker?id=1,2,3) | View multiple impression trackers by ID using a comma-separated list. |
| `DELETE` | [https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID](https://api.appnexus.com/imptracker?id=IMP_TRACKER_ID) | Delete an impression tracker. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the impression tracker.<br>**Default:** Auto-incremented number (i.e., 123).<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `member_id` | int | The ID of the member to which the advertiser belongs.<br>**Read Only.** |
| `advertiser_id` | int | The ID of the advertiser that owns the impression tracker.<br>**Required On:** `POST`, in query string. |
| `name` | string | The name for the impression tracker.<br>**Required On:** `POST` |
| `code` | string | The custom code for the impression tracker. |
| `state` | enum | The state of the impression tracker. <br>Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `publisher` | object | The publisher to which the impression tracker is associated. For more details, see [Publisher](#publisher) below.<br>**Required On:** `POST` |
| `tag` | array | The placement to which the impression tracker is associated. For more details, see [Tag](#tag) below. |
| `payment_rule` | object | The payment rule to which the impression tracker is associated. For more details, see [Payment Rule](#payment-rule) below. |
| `line_item` | object | The advertiser line item to which the impression tracker is associated. For more details, see [Line Item](#line-item) below.<br>**Required On:** `POST` |
| `clicktracker` | object | Not currently in use. |
| `last_modified` | timestamp | The date and time when the impression tracker was last modified.<br>**Read Only.** |

### Publisher

You can use the [Publisher Service](publisher-service.md) to get information about publishers.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the publisher to which the impression tracker is associated. |
| `name` | string | The name of the publisher to which the impression tracker is associated.<br>**Read Only.** |

### Tag

You can use the [Placement Service](placement-service.md) to get information about placements.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the placement to which the impression tracker is associated. |
| `name` | string | The name of the placement to which the impression tracker is associated.<br>**Read Only.** |

### Payment rule

You can use the [Payment Rule Service](payment-rule-service.md) to get information about payment rules.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the payment rule to which the impression tracker is associated. |
| `name` | string | The name of the payment rule to which the impression tracker is associated.<br>**Read Only.** |

### Line item

You can use the [Line Item Service](line-item-service.md) to get information about line items.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item to which the impression tracker is associated. |
| `name` | string | The name of the line item to which the impression tracker is associated.<br>**Read Only.** |

## Examples

### Create a new impression tracker

```
$ cat imptracker

{
    "imptracker": {
        "name": "Test Impression Tracker",
        "publisher": {
            "id": 44449
        },
        "line_item": {
            "id": 74957
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @imptracker 'https://api.appnexus.com/imptracker?advertiser_id=37236'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1425,
        "start_element": 0,
        "num_elements": 100,
        "imptracker": {
            "id": 1425,
            "member_id": 958,
            "advertiser_id": 37236,
            "name": "Test Impression Tracker",
            "code": null,
            "state": "active",
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

### Update an impression tracker

In this example, the `PUT` request associates a placement to impression tracker 1425.

```
$ cat imptracker_update
{
    "imptracker": {
        "tag": {
            "id": 474412
        }
    }
}

$ curl -b cookies -c cookies -X PUT -d @imptracker_update 'https://api.appnexus.com/imptracker?id=1425'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "1425",
        "start_element": 0,
        "num_elements": 100,
        "imptracker": {
            "id": 1425,
            "member_id": 958,
            "advertiser_id": 37236,
            "name": "Test Impression Tracker",
            "code": null,
            "state": "active",
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

### View impression tracker 582

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/imptracker?id=582'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "imptracker": {
            "id": 582,
            "member_id": 1066,
            "advertiser_id": 35081,
            "name": "Test Impression Tracker 1",
            "code": null,
            "state": "active",
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

### View all impression trackers for advertiser 35081

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/imptracker?advertiser_id=35081'

{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "imptrackers": [
            {
                "id": 582,
                "member_id": 1066,
                "advertiser_id": 35081,
                "name": "Test Impression Tracker 1",
                "code": null,
                "state": "active",
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
                "name": "Test Impression Tracker 2",
                "code": null,
                "state": "active",
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
