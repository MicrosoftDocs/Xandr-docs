---
title: Bidders - Creative Format Service
description: Learn how Xandr categorizes creatives by format, media type, and media subtype. This page also provides examples for viewing all creatives and specific creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Bidders - Creative format service

Xandr categorizes creatives by format, media type, and media subtype. Format defines the resource type of creatives (flash, image, etc.); media type defines the general display style of creatives (banner, expandable, video, etc.); and media subtype defines the specific display style of creatives (standard banner, MediaMind expandable, or Standard VAST).

This read-only service allows you to view all of the supported creative formats.

## REST API

| HTTP method | End point | Description |
|--|--|--|
| GET | [https://api.adnxs.com/creative-format](https://api.adnxs.com/creative-format) | View all creative formats |
| GET | [https://api.appnexus.com/creative-format?id=CREATIVE_FORMAT_ID](https://api.appnexus.com/creative-format?id=CREATIVE_FORMAT_ID) | View a specific creative format |

## JSON fields

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the creative format. |
| `last_modified` | timestamp | The date and time when Xandr last modified the creative format. |
| `name` | string | The name of the creative format, for example, "flash", "image", "url-html", or "url-xml". |

## Examples

**View all creative formats**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative-format'
{
    "response": {
        "status": "OK",
        "count": 12,
        "start_element": 0,
        "num_elements": 100,
        "creative-formats": [
            {
                "id": 1,
                "name": "url-html",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 2,
                "name": "url-js",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 3,
                "name": "flash",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 4,
                "name": "image",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 5,
                "name": "raw-js",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 6,
                "name": "raw-html",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 7,
                "name": "iframe-html",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 8,
                "name": "url-vast",
                "last_modified": "2011-06-03 13:29:18"
            },
            {
                "id": 9,
                "name": "text",
                "last_modified": "2011-06-03 13:29:19"
            },
            {
                "id": 10,
                "name": "url-xml",
                "last_modified": "2012-01-27 16:14:43"
            },
            {
                "id": 11,
                "name": "url-file",
                "last_modified": "2012-01-27 16:14:43"
            },
            {
                "id": 12,
                "name": "native",
                "last_modified": "2015-02-26 23:40:28"
            }
        ]
    }
}
```

**View a specific creative format**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative-format?id=5'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "creative-format": {
            "id": 5,
            "name": "raw-js",
            "last_modified": "2012-01-17 18:50:25"
        },
        "dbg_info": {
            ...
        }
    }
}
```
