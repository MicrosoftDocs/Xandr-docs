---
title: Bidders - Ad Server Service
description: In this article, learn about the Ad Server service along with a list of supported JSON fields and an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Ad server service

This read-only service allows you to view information about ad servers that can deliver third-party creatives or that can be called for data collection purposes during the delivery of Xandr-hosted or third-party creatives.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `https://api.adnexus.com/ad-server` | To view all ad servers. |
| GET | `https://api.adnexus.com/ad-server?id=ADSERVER_ID` | To view information about a specific ad server. |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `declare_to_adx` | boolean | If true, the ad server is identified when bidding on Google Ad Exchange inventory. Identification is required to be in full compliance with Google Ad Exchange creative policies. |
| `description` | string | The description of the ad server. |
| `hostnames` | array of objects | A comma-separated list of host names that can be associated with the ad server. This field can be edited only by an administrator. |
| `id` | int | The internal ID associated with the ad server. |
| `last_activity` | timestamp | The date and time (in the form YYYY-MM-DD HH:MM:SS) when the ad server configuration was last updated in Xandr's system. |
| `name` | string | The name of the ad server. |

## Example

### View all ad servers (output is truncated)

```
curl -b cookies -c cookies 'https://api.adnexus.com/ad-server'
{
    "response": {
        "status": "OK"
        "adservers": [
            {
                "id": 1,
                "name": "24/7 Real Media",
                "description":"null",
                "declare_to_adx": false,
                "last_modified":"2010-06-20 15:45:00"
            },
            {
                "id": 2,
                "name": "Ad Manager",
                "description":"null",
                "declare_to_adx": false,
                "last_modified":"2010-04-05 21:43:30"
            },
            {
                "id": 3,
                "name": "AdCentric",
                "description":"null",
                "declare_to_adx: false,
                "last_modified":"2011-07-02 19:56:44"
            }
            ...
        ],
        "status": "OK"
    }
}
```
