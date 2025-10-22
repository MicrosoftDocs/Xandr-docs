---
title: Lookup Service
description: Explore the read-only Lookup service, enabling you to fetch the ID, name, code, state, and, in some cases, descriptions of objects within your account.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Lookup service

This read-only service allows you to retrieve the ID, name, code, state, and in some cases, descriptions of the following types of objects in your account. It also returns hierarchical information about these objects, for example, publisher ID for a placement or advertiser ID for a line item. In cases where you have limited information about objects, this service gives you an easy way to map to other relevant data. [Bulk Reporting Feeds](bulk-reporting-feeds.md), for example, returns data grouped by object IDs. You can use the Lookup Service to match these IDs with names, codes, and so on.

- Advertisers
- Insertion Orders
- Line Items
- Campaigns
- Creatives
- Segment Pixels
- Conversion Pixels
- Publishers
- Payment Rules
- Sites
- Placements
- Labels

> [!NOTE]
>
> - The Lookup Service is different from the [Search Service](search-service.md) because it returns all objects of a certain type in your account. The Search Service allows you to search for objects with a specific name, code, or ID.
> - The Lookup Service can return a maximum of 50,000 objects.
> - The Lookup Service is based on data that is cached and updated once every 8 minutes.

## REST API

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/lookup](https://api.appnexus.com/lookup) | View information about all objects in your system. |
| `GET` | [https://api.appnexus.com/lookup?type=OBJECT_TYPE](https://api.appnexus.com/lookup?type=OBJECT_TYPE) | View information about all objects of a specific type.<br><br>**Note:**<br>You can get information about the following object types: `advertiser`, `insertion_order`, `line_item`, `campaign`, `budget_splitter`, `creative`, `segment_pixel`, `conversion_pixel`, `publisher`, `payment_rule`, `placement`, `site`, and `label`. |
| `GET` | [https://api.appnexus.com/lookup?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/lookup?advertiser_id=ADVERTISER_ID) | View information about all objects belonging to a specific advertiser. |

## JSON fields

Fields returned for all object types:

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | The custom code for the object (not applicable to all object types). |
| `id` | int | The internal ID associated with the object. |
| `last_modified` | timestamp | The date and time when the object was last modified. |
| `name` | string | The name of the object. |
| `state` | enum | The state of the object. <br>Possible values: `"active"` or `"inactive"`. |

## Object-specific JSON fields

Additional fields returned for specific object types.

### Advertiser

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | int | The ID of the member to which the advertiser belongs. |

### Insertion order

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser to which the insertion order belongs. |

### Line item

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser to which the line item belongs. |

### Campaign

| Field | Type | Description |
|:---|:---|:---|
| `line_item_id` | int | The ID of the line item to which the campaign belongs. |

### Budget splitter

| Field | Type | Description |
|:---|:---|:---|
| `line_item_id` | int | The ID of the line item to which the budget splits belong. |
| `name` | string | The name of the budget split. |
| `id` | int | The ID of the budget split. |
| `state` | string | The state of the budget split.<br>Permitted values are:<br>- `active`<br>- `inactive` |
| `last_modified` | date | The timestamp when the split was last modified. |

### Creative

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser to which the creative belongs. |
| `brand_id` | int | The ID of the brand associated to the creative. |
| `description` | string | The description of the creative. |
| `landing_page_url` | string | The URL of the landing page associated with this creative. |
| `publisher_id` | int | The ID of the publisher to which the creative is associated. |

### Segment pixel

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser to which the segment pixel is associated. |
| `member_id` | int | The ID of the member to which the segment pixel belongs. |

### Conversion pixel

| Field | Type | Description |
|:---|:---|:---|
| `advertiser_id` | int | The ID of the advertiser to which the conversion pixel belongs. |

### Publisher

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | int | The ID of the member to which the publisher belongs. |

### Payment rule

| Field | Type | Description |
|:---|:---|:---|
| `description` | string | The description of the payment rule. |
| `publisher_id` | int | The ID of the publisher to which the payment rule belongs. |

### Placement

| Field | Type | Description |
|:---|:---|:---|
| `publisher_id` | int | The ID of the publisher to which the placement belongs. |

### Site

| Field | Type | Description |
|:---|:---|:---|
| `publisher_id` | int | The ID of the publisher to which the site belongs. |

### Label

| Field | Type | Description |
|:---|:---|:---|
| `label_id` | int | The ID of the label. |
| `member_id` | int | The ID of the member to which the label belongs. |
| `object_id` | int | The ID of the object to which the label can be applied. |
| `object_type` | enum | The type of object to which the label can be applied. <br>Possible values: `"advertiser"`, `"insertion_order"`, `"line_item"`, `"campaign"`, or `"publisher"`. |
| `value` | string | The label text. |

## Examples

### Look up all of your campaigns

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/lookup?type=campaign'
{
    "response": {
        "status": "OK",
        "num_elements": 2,
        "start_element": 0,
        "results": {
            "campaign": {
                "results": [
                    {
                        "id": "58990",
                        "name": "Car Donations",
                        "line_item_id": "31189",
                        "state": "active",
                        "code": "cdon",
                        "last_modified": "2011-10-18 17:25:00"
                    },
                    {
                        "id": "58991",
                        "name": "Bucket Builders",
                        "line_item_id": "31189",
                        "state": "active",
                        "code": "bb",
                        "last_modified": "2011-10-12 22:08:04"
                    }
                ],
                "num_elements": "2"
            }
        }
    }
}
```

### Look up all objects accessible to this service

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/lookup'
{
    "response": {
        "status": "OK",
        "num_elements": 24,
        "start_element": 0,
        "results": {
            "advertiser": {
                "results": [
                    {
                        "id": "35081",
                        "name": "Bucketeer",
                        "code": "bucket",
                        "member_id": "1066",
                        "state": "active",
                        "last_modified": "2011-10-18 17:25:00"
                    }
                ],
                "num_elements": "1"
            },
            "insertion_order": {
                "results": null,
                "num_elements": 0
            },
            "line_item": {
                "results": [
                    {
                        "id": "31189",
                        "name": "bucket line 1",
                        "code": "bk1",
                        "advertiser_id": "35081",
                        "state": "active",
                        "last_modified": "2011-10-18 17:25:00"
                    }
                ],
                "num_elements": "1"
            },
            "campaign": {
                "results": [
                    {
                        "id": "58990",
                        "name": "Car Donations",
                        "line_item_id": "31189",
                        "state": "active",
                        "code": "cdon",
                        "last_modified": "2011-10-18 17:25:00"
                    },
                    {
                        "id": "58991",
                        "name": "Bucket Builders",
                        "line_item_id": "31189",
                        "state": "active",
                        "code": "bb",
                        "last_modified": "2011-10-17 13:24:00"
                    }
                ],
                "num_elements": "2"
            },
            "budget_splitter":{
               "results": [
                   {
                         "line_item_id": 1,
                         "name": "Split 1",
                         "id": 1,
                         "state": "active",
                         "last_modified": "2023-04-18 17:25:00"
                    },
                    {
                    "line_item_id": 1,
                    "name": "Split 2",
                    "id": 2,
                    "state": "active",
                    "last_modified": "2023-04-19 17:25:00"
                    },
                ],
                "num_elements": "2"
            },
            "creative": {
                "results": [
                    {
                        "id": "445832",
                        "code": null,
                        "description": "Donate car.png",
                        "advertiser_id": "35081",
                        "publisher_id": "0",
                        "state": "active",
                        "brand_id": 1,
                        "landing_page_url": "www.cardonations.com/donate",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "445833",
                        "code": null,
                        "description": "bucketbuilders.png",
                        "advertiser_id": "35081",
                        "publisher_id": "0",
                        "state": "active",
                        "brand_id": 3,
                        "landing_page_url": "www.buckets.com/build",
                        "last_modified": "2011-10-17 13:24:00"
                    }
                ],
                "num_elements": "2"
            },
            "segment_pixel": {
                "results": null,
                "num_elements": 0
            },
            "payment_rule": {
                "results": [
                    {
                        "id": "91345",
                        "name": "",
                        "publisher_id": "89286",
                        "state": "active",
                        "description": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "91346",
                        "name": "Default",
                        "publisher_id": "89287",
                        "state": "active",
                        "description": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "91375",
                        "name": "Base Payment Rule",
                        "publisher_id": "89314",
                        "state": "active",
                        "description": "",
                        "last_modified": "2011-10-17 13:24:00"
                    }
                ],
                "num_elements": "3"
            },
            "conversion_pixel": {
                "results": null,
                "num_elements": 0
            },
            "publisher": {
                "results": [
                    {
                        "id": "89286",
                        "name": "Default Real Time",
                        "member_id": "1066",
                        "state": "inactive",
                        "code": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "89287",
                        "name": "Wide Road",
                        "member_id": "1066",
                        "state": "active",
                        "code": "bb",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "89314",
                        "name": "Radio Live",
                        "member_id": "1066",
                        "state": "active",
                        "code": "rlive",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    ...
                ],
                "num_elements": "5"
            },
            "placement": {
                "results": [
                    {
                        "id": "594594",
                        "name": "[Default Real Time] - Default",
                        "publisher_id": "89286",
                        "state": "active",
                        "code": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "594595",
                        "name": "[Wide Road] - Placement 1",
                        "publisher_id": "89287",
                        "state": "active",
                        "code": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "594641",
                        "name": "[Radio Live] - Default",
                        "publisher_id": "89314",
                        "state": "active",
                        "code": "",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    ...
                ],
                "num_elements": "5"
            },
            "site": {
                "results": [
                    {
                        "id": "188039",
                        "code": "",
                        "name": "[Default Real Time] - ROS",
                        "publisher_id": "89286",
                        "state": "active",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "188040",
                        "code": "",
                        "name": "[Wide Road] - ROS",
                        "publisher_id": "89287",
                        "state": "active",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    {
                        "id": "188070",
                        "code": "",
                        "name": "[Radio Live] - ROS",
                        "publisher_id": "89314",
                        "state": "active",
                        "last_modified": "2011-10-17 13:24:00"
                    },
                    ...
                ],
                "num_elements": "5"
            },
        }
    }
}
```
