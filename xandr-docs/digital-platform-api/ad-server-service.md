---
title: Digital Platform API - Ad Server Service
description: Ad Server service allows access to information about ad servers for third-party creatives delivery or data collection during content delivery.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Ad Server service

This read-only service allows you to view information about ad servers that can deliver third-party creatives or that can be called for data collection purposes during the delivery of Xandr-hosted or third-party creatives.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/adserver` | View all ad servers |
| `GET` |`https://api.appnexus.com/adserver?id=ADSERVER_ID` | View information about a specific ad server |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `declare_to_adx` | boolean | If true, the ad server is identified when bidding on Google Ad Manager inventory. Identification is required to be in full compliance with [Google Ad Manager creative policies](https://support.google.com/adwordspolicy/answer/94230?hl=en&rd=1). |
| `description` | string | The description of the ad server. |
| `hostnames` | array of objects | A list of host names that can be associated with the ad server. This field can be edited only by an administrator. |
| `id` | int | The internal ID associated with the ad server. |
| `last_modified` | timestamp | The date and time (in the form YYYY-MM-DD HH:MM:SS) when the ad server configuration was last updated in our system. |
| `name` | string | The name of the ad server. |

## Examples

### View all ad servers (output is truncated)

```
curl -b cookies -c cookies 'https://api.appnexus.com/adserver'
{
    "response": {
        "status": "OK",
        "adservers": [
            {
                "id": 0,
                "name": "Other/Unlisted",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2011-07-14 13:54:01",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 1,
                "name": "24/7 Real Media",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-04-15 21:43:30",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 2,
                "name": "Ad Manager",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-04-01 19:56:43",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 3,
                "name": "AdCentric",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-05-20 18:33:47",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 4,
                "name": "Adconian",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-04-01 19:56:43",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 5,
                "name": "AdDynamix",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-04-01 19:56:43",
                "is_hidden": false,
                "hostnames": null
            },
            {
                "id": 6,
                "name": "AdECN",
                "description": null,
                "type": "adserver",
                "is_appnexus_approved": false,
                "declare_to_adx": false,
                "last_modified": "2010-04-01 19:56:43",
                "is_hidden": false,
                "hostnames": "hostname1.com","hostname2.net"
            },
            ...
        ],
        "count": 202,
        "start_element": null,
        "num_elements": null,
        "dbg_info": {
            ...
        }
    }
}
```

### View information about ad server `5`

```
curl -b cookies -c cookies 'https://api.appnexus.com/adserver?id=5'
{
    "response": {
        "status": "OK",
        "adserver": {
            "id": 5,
            "name": "AdDynamix",
            "description": null,
            "type": "adserver",
            "is_appnexus_approved": false,
            "declare_to_adx": false,
            "last_modified": "2010-04-01 19:56:43",
            "is_hidden": false,
            "hostnames": null
        },
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "dbg_info": {
            ...
        }
    }
}
```
