---
title: Digital Platform API - Creative Format Service
description: In this article, learn about the Creative Format service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Creative Format service

The Xandr platform categorizes creatives by format, media type, and media subtype. Format defines the resource type of creatives (flash, image, etc.); media type defines the general display style of creatives (banner, expandable, video, etc.); and media subtype defines the specific display style of creatives (standard banner, MediaMind expandable, or Standard VAST).

This read-only service allows you to view all of the supported creative formats.

> [!NOTE]
> To view all supported media types and media subtypes, you can use the [Media Type Service](media-type-service.md) and the [Media Subtype Service](media-subtype-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/creative-format](https://api.appnexus.com/creative-format) | View all creative formats. |
| `GET` | [https://api.appnexus.com/creative-format?id=CREATIVE_FORMAT_ID](https://api.appnexus.com/creative-format?id=CREATIVE_FORMAT_ID) | View a specific creative format. |

## JSON Fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative format. |
| `name` | string  | The name of the creative format. For example, `"flash"`, `"image"`, `"url-html"`, or `"url-xml"`. |
| `last_modified` | timestamp | The date and time when Xandr last modified the creative format. |

## Examples

### View all creative formats

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-format'
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

### View a specific creative format

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-format?id=5'
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
        }
    }
}
```
