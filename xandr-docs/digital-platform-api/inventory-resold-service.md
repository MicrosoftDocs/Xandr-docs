---
title: Inventory Resold Service
description: Explore the Inventory Resold service, providing visibility into inventory exposed for resale by networks on the platform.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Inventory Resold service

This read-only service allows you to view inventory that has been exposed for resale by networks on the platform. This includes inventory exposed by your network and other networks.

- To enable your inventory for resale, use the [Site Service](site-service.md).
- To expose your inventory for resale:
  - For inventory categories, use the [Visibility Profile Service](visibility-profile-service.md).
  - For publishers, use the [Publisher Service](publisher-service.md).
  - For whole networks, use the [Member Service](member-service.md).
- To control the inventory data that platform members and external bidders see in your bid requests, use the [Visibility Profile Service](visibility-profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/inventory-resold](https://api.appnexus.com/inventory-resold) | View all publishers, content categories, and members exposed for resale. |
| `GET` | [https://api.appnexus.com/inventory-resold?type=publisher](https://api.appnexus.com/inventory-resold?type=publisher) | View all publishers exposed for resale. |
| `GET` | [https://api.appnexus.com/inventory-resold?type=publisher&id=1,2,3,etc](https://api.appnexus.com/inventory-resold?type=publisher&id=1,2,3,etc) | View specific publishers exposed for resale (using a comma-separated list of IDs). |
| `GET` | [https://api.appnexus.com/inventory-resold?type=content_category&category_type=standard](https://api.appnexus.com/inventory-resold?type=content_category&category_type=standard) | View all content categories exposed for resale. |
| `GET` | [https://api.appnexus.com/inventory-resold?type=content_category&id=1,2,3,etc](https://api.appnexus.com/inventory-resold?type=content_category&id=1,2,3,etc) | View specific content categories exposed for resale (using a comma-separated list of IDs). |
| `GET` | [https://api.appnexus.com/inventory-resold?type=member](https://api.appnexus.com/inventory-resold?type=member) | View all members exposed for resale.|
| `GET` | [https://api.appnexus.com/inventory-resold?type=member&id=1,2,3,etc](https://api.appnexus.com/inventory-resold?type=member&id=1,2,3,etc) | View specific members exposed for resale (using a comma-separated list of IDs). |
| `GET` | [https://api.appnexus.com/inventory-resold/meta](https://api.appnexus.com/inventory-resold/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `daily_volume` | int | The average daily impressions from last 7 days. |
| `description` | string(255) | The description of the object. |
| `id` | int | The internal ID assigned to the object (`publisher`, `member` or `content_category`). |
| `member_id` | int | The ID of the owning member. |
| `member_name` | string | The name of the owning member. |
| `name` | string(255) | The name of the object. |
| `reselling_exposed_on` | timestamp | The date and time when the publisher or member was exposed for reselling. <br><br>**Note:** As of version 1.13, this field is not available for content categories. |
| `stats` | array of objects | The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `type` | enum | The type of object. Possible values: `"publisher"`, `"member"`, or `"content_category"`. |

## Examples

### View all publishers, content categories, and members exposed for resale

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/inventory-resold'
{
    "response": {
        "status": "OK",
        "inventory-resold": [
            {
                "id": 88,
                "name": "Kitara Media",
                "description": null,
                "member_id": 88,
                "member_name": "Kitara Media",
                "type": "member",
                "reselling_exposed_on": "2010-06-07 21:29:56",
                "daily_volume": "67119880"
            },
            {
                "id": 95,
                "name": "Matomy Media (formerly Xtend Media)",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "member",
                "reselling_exposed_on": "2011-05-04 08:51:51",
                "daily_volume": "20578570"
            },
            {
                "id": 231,
                "name": "Morning Falls",
                "description": null,
                "member_id": 231,
                "member_name": "Morning Falls",
                "type": "member",
                "reselling_exposed_on": "2010-08-23 20:44:51",
                "daily_volume": "24"
            },
            {
                "id": 311,
                "name": "Collective Exchange",
                "description": null,
                "member_id": 311,
                "member_name": "Collective Exchange",
                "type": "member",
                "reselling_exposed_on": "2010-11-19 22:55:15",
                "daily_volume": "97485150"
            },
            ...
            {
                "id": 537,
                "name": "Fun & Trivia",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 538,
                "name": "Autos & Vehicles",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 539,
                "name": "Beauty & Personal Care",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 540,
                "name": "Business & Industry",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 541,
                "name": "Computers & Electronics",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 541,
                "name": "CPXInteractive",
                "description": null,
                "member_id": 541,
                "member_name": "CPXInteractive",
                "type": "member",
                "reselling_exposed_on": "2011-01-05 17:22:19",
                "daily_volume": "1067491726"
            },
            {
                "id": 542,
                "name": "Arts & Entertainment",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 543,
                "name": "Finance",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 544,
                "name": "Food & Drink",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 545,
                "name": "Games",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 546,
                "name": "Health",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            ...
            {
                "id": 563,
                "name": "X-Taringa.org",
                "description": "",
                "member_id": 332,
                "member_name": "D'Arriens",
                "type": "publisher",
                "reselling_exposed_on": "2012-03-21 18:55:47",
                "daily_volume": null
            },
            {
                "id": 564,
                "name": "Collective Exchange (UK)",
                "description": null,
                "member_id": 564,
                "member_name": "Collective Exchange (UK)",
                "type": "member",
                "reselling_exposed_on": "2010-12-15 16:09:48",
                "daily_volume": "4322501"
            },
            {
                "id": 564,
                "name": "MessengerAdictos",
                "description": "",
                "member_id": 332,
                "member_name": "D'Arriens",
                "type": "publisher",
                "reselling_exposed_on": "2012-03-21 18:55:47",
                "daily_volume": null
            },
            {
                "id": 568,
                "name": "Httpool",
                "description": null,
                "member_id": 568,
                "member_name": "Httpool",
                "type": "member",
                "reselling_exposed_on": "2011-02-24 15:49:52",
                "daily_volume": "159637"
            },
            {
                "id": 576,
                "name": "Nextperience",
                "description": null,
                "member_id": 576,
                "member_name": "Nextperience",
                "type": "member",
                "reselling_exposed_on": "2010-10-29 20:46:08",
                "daily_volume": "3359929"
            },
            {
                "id": 576,
                "name": "Grooveshark",
                "description": "",
                "member_id": 332,
                "member_name": "D'Arriens",
                "type": "publisher",
                "reselling_exposed_on": "2012-03-21 18:55:48",
                "daily_volume": "48"
            },
            ...
        ],
        "count": 13984,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### View all content categories exposed for resale

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/inventory-source?type=content_category&category_type=standard'
{
    "response": {
        "status": "OK",
        "inventory-resold": [
            {
                "id": 537,
                "name": "Fun & Trivia",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 538,
                "name": "Autos & Vehicles",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 539,
                "name": "Beauty & Personal Care",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 540,
                "name": "Business & Industry",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 541,
                "name": "Computers & Electronics",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 542,
                "name": "Arts & Entertainment",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            {
                "id": 543,
                "name": "Finance",
                "description": null,
                "member_id": 95,
                "member_name": "Matomy Media (formerly Xtend Media)",
                "type": "content_category",
                "daily_volume": null
            },
            ...
        ],
        "count": 1145,
        "start_element": 0,
        "num_elements": 100
    }
}
```
