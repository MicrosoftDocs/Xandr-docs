---
title: Digital Platform API - Browser Service
description: In this article, find information about the Browser Service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Browser service

The read-only Browser Service allows you to see what browsers are registered in our system. You can use this service to retrieve the IDs of browsers for targeting in campaigns via the [Profile Service](profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `https://api.appnexus.com/browser` | View all browsers available for targeting |
| `GET` | `https://api.appnexus.com/browser?search=SEARCH_TERM` | View all browsers with IDs or names containing certain characters |
| `GET` | `https://api.appnexus.com/browser?id=BROWSER_ID` | View a specific browser |
| `GET` | `https://api.appnexus.com/browser/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `id` | int | The ID of the browser. |
| `is_aggregated` | boolean | If true, Xandr aggregates data for the browser in reporting. If false, the carrier will appear as "Other Browser" in reporting. |
| `last_modified` | string | The date and time when the browser entry was last modified. |
| `name` | string | The name of the browser. |

## Examples

### View all browsers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/browser'
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "browsers": [
            {
                "id": 0,
                "name": "Unknown",
                "last_modified": "2012-11-27 15:32:33",
                "is_aggregated": true
            },
            {
                "id": 1,
                "name": "Internet Explorer 8",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            },
            {
                "id": 2,
                "name": "Internet Explorer 7",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            },
            {
                "id": 3,
                "name": "Internet Explorer 6",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            },
                        ...
                ]
        } 
}
```

### View a specific browser

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/browser?id=8'
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "browser": {
            "id": 8,
            "name": "Chrome (all versions)",
            "last_modified": "2012-11-27 15:32:43",
            "is_aggregated": true
        }
    }
}
```

### Search for a browser

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/browser?search=firefox'
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "browsers": [
            {
                "id": 5,
                "name": "Firefox 4",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            },
            {
                "id": 6,
                "name": "Firefox 3",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            },
            {
                "id": 7,
                "name": "Firefox (other versions)",
                "last_modified": "2012-11-27 15:32:43",
                "is_aggregated": true
            }
        ]
    }
}
```
