---
title: Digital Platform API - Technical Attribute Service
description: Use the Technical Attribute service to view the list of technical attributes that you can target in the ad profile service via ID.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Technical Attribute service

This is a read-only service that shows you the list of technical attributes that you can target in the [Ad Profile Service](./ad-profile-service.md) via technical attribute ID.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/technical-attribute` | View all technical attributes. |
| `GET` | `https://api.appnexus.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID` | View a specific technical attribute. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The internal identifier for the technical attribute. |
| `last_activity` | date | The date/time at which the technical attribute was last modified. |
| `name` | string | The name of the technical attribute. |

## Examples

### To see all technical attributes available for targeting

```
$ curl -b cookies -c cookies  https://api.appnexus.com/technical-attribute
{
  "response": {
    "status": "OK",
    "count": 29,
    "start_element": 0,
    "num_elements": 100,
    "technical-attributes": [
      {
        "id": 1,
        "name": "Image",
        "last_modified": "2010-05-21 21:05:28"
      },
      {
        "id": 2,
        "name": "Flash",
        "last_modified": "2010-05-21 21:05:28"
      },
      {
        "id": 3,
        "name": "Text",
        "last_modified": "2010-05-21 21:05:28"
      },
      {
        "id": 4,
        "name": "Video",
        "last_modified": "2010-05-21 21:05:28"
      },
      {
        "id": 5,
        "name": "DHTML",
        "last_modified": "2012-03-23 14:25:40"
      },
      {
        "id": 6,
        "name": "Expandable",
        "last_modified": "2010-05-21 21:05:28"
      },
      {
        "id": 7,
        "name": "Audio: user-initiated",
        "last_modified": "2010-06-24 18:04:00"
      },
      {
        "id": 8,
        "name": "Audio: auto-initiated",
        "last_modified": "2010-06-24 18:04:02"
      },
      {
        "id": 9,
        "name": "Initial Load > 40kb",
        "last_modified": "2011-02-06 20:24:56"
      },
      {
        "id": 10,
        "name": "Full Page Pop",
        "last_modified": "2011-06-08 22:19:05"
      },
      {
        "id": 16,
        "name": "Animated: between 15 and 30 seconds",
        "last_modified": "2013-06-27 14:13:26"
      },
      {
        "id": 17,
        "name": "Animated: more than 30 seconds",
        "last_modified": "2013-06-27 14:13:26"
      },
      {
        "id": 18,
        "name": "Expandable: Standard Expansion",
        "last_modified": "2012-04-05 19:23:14"
      },
      {
        "id": 19,
        "name": "Expandable: Large Expansion",
        "last_modified": "2012-04-05 19:23:14"
      },
      {
        "id": 20,
        "name": "Expandable: Click To Expand",
        "last_modified": "2012-04-05 19:23:14"
      },
      {
        "id": 21,
        "name": "Expandable: Mouseover To Expand",
        "last_modified": "2012-04-05 19:23:14"
      },
      {
        "id": 22,
        "name": "Expandable: Auto-Expand",
        "last_modified": "2012-04-05 19:23:14"
      },
      {
        "id": 23,
        "name": "Interstitial",
        "last_modified": "2012-03-16 19:39:59"
      },
      {
        "id": 25,
        "name": "Animated: between 0 - 15 seconds",
        "last_modified": "2013-06-27 14:13:26"
      },
      {
        "id": 26,
        "name": "Pop up",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 27,
        "name": "Pop under",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 28,
        "name": "Site under",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 29,
        "name": "Layer: Banderole",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 30,
        "name": "Layer: Footer",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 31,
        "name": "Layer: Skin",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 32,
        "name": "Layer: Slide-in",
        "last_modified": "2012-09-18 23:34:15"
      },
      {
        "id": 34,
        "name": "Mobile Targeted Landing Page",
        "last_modified": "2013-08-19 13:50:28"
      },
      {
        "id": 35,
        "name": "Mobile Optimized Creative",
        "last_modified": "2013-08-19 13:52:50"
      },
      {
        "id": 36,
        "name": "MRAID",
        "last_modified": "2013-08-19 16:04:51"
      }
    ],
  }
}
```
