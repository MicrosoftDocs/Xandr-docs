---
title: External Inventory Code Service
description: The External Inventory Code service allows sellers to register their own codes for granular inventory breakdown and report on them during ad calls.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# External Inventory Code service

Some sellers use their own codes to break out their inventory more granularly than by Publisher \> Site \> Placement. The External Inventory Code Service allows you to register such codes with Xandr so that you can pass them on ad calls and then report on them.

Here's how it works:

1. You must make a `POST` call to this service to register an external inventory code with Xandr prior to steps 2 and 3.
1. You pass the code as `ext_inv_code` in the [query string of tag-based](../monetize/placement-tag-parameters.md) ad calls (see example below), or by defining an `extInvCode` value via [AST's defineTag API](../seller-tag/define-tag.md) or the [Mobile SDK's API](../mobile-sdk/support-for-external-inventory-code-and-traffic-source-code-on-android.md).
1. You can then report on external inventory ID/name (mapped from the external inventory code via the API service outlined on this page) in any of the following reports/feeds (that you have access to):  
    - [Network Analytics Report](../monetize/network-analytics-report.md) in the Reporting UI
    - [Network Analytics](./network-analytics.md) via Reporting API
    - [Publisher Analytics Report](../monetize/publisher-analytics.md) in the Reporting UI
    - [Network Publisher Analytics](./network-publisher-analytics.md) via Reporting API
    - [Network Analytics Feed](./network-analytics-feed.md) via Bulk Reporting API
    - [Log-Level Standard Feed](../log-level-data/standard-feed.md) via LLD

## Example placement tag with external inventory code

```
<script src="https://ib.adnxs.com/ttj?id=1234&ext_inv_code=ABC" type="text/javascript"></script>
```

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/external-inv-code` | View all of your external inventory codes. |
| `GET` | `https://api.appnexus.com/external-inv-code?publisher_id=PUBLISHER_ID` | View all external inventory codes for a specific publisher. |
| `GET` | `https://api.appnexus.com/external-inv-code?id=ID` | View a specific external inventory code. |
| `GET` | `https://api.appnexus.com/external-inv-code?code=CODE` | View a specific external inventory code. |
| `POST` | `https://api.appnexus.com/external-inv-code` | Add a new external inventory code. |
| `PUT` | `https://api.appnexus.com/external-inv-code?id=ID` | Modify an external inventory code. |
| `DELETE` | `https://api.appnexus.com/external-inv-code?id=ID` | Delete an external inventory code. |

## JSON fields

> [!TIP]
> Each combination of `publisher_id` and `code` must be unique.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `code` | string (100) | The value that will be passed as `ext_inv_code` in the query string of tag-based ad calls or the request body of AST/SDK-based ut/v3 ad calls.<br><br>**Required On**: `POST` |
| `id` | int | The ID for the external inventory code.<br><br>**Default**: auto-generated number<br>**Required On**: `PUT` and `DELETE` |
| `name` | string (100) | The name for the external inventory code. This name can be included in the (first four) Network/Publisher Analytics UI/API reports listed above.<br><br>**Required On**: `POST` |
| `publisher_id` | int | The ID of the publisher for which the external inventory code is used. If `0`, the code is used across multiple publishers.<br><br>**Default**: `0` |

## Examples

### Adding an external inventory code for a specific publisher

```
$ cat ext_inv_code.json
{
   "external_inv_code": {
      "publisher_id": 103764,
      "code":"55",
      "name":"Code 55"
   }
}
$ curl -b cookies -c cookies -X POST -d @ext_inv_code.json 'https://api.appnexus.com/external-inv-code'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 102,
        "start_element": 0,
        "num_elements": 100,
        "external_inv_code": {
            "member_id": 1066,
            "id": 102,
            "publisher_id": 103764,
            "name": "55",
            "code": "Code 55"
        }
        }
    }
}
```

### Adding an external inventory code for use across multiple publishers

```
$ cat ext_inv_code.json
{
   "external_inv_code": {
      "publisher_id": 0,
      "code":"74",
      "name":"Code 74"
   }
}
$ curl -b cookies -c cookies -X POST -d @ext_inv_code.json 'https://api.appnexus.com/external-inv-code'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 102,
        "start_element": 0,
        "num_elements": 100,
        "external_inv_code": {
            "member_id": 1066,
            "id": 103,
            "publisher_id": 0,
            "name": "74",
            "code": "Code 74"
        }
    }
}
```

### Updating an external inventory code

```
$ cat ext_inv_code_update
{
   "external_inv_code": {
      "name":"Fresh new name"
   }
}
$ curl -b cookies -c cookies -X PUT -d @ext_inv_code_update.json 'https://api.appnexus.com/external-inv-code?id=102'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "102",
        "start_element": 0,
        "num_elements": 100,
        "external_inv_code": {
            "member_id": 1066,
            "id": 102,
            "publisher_id": 103764,
            "name": "Fresh new name",
            "code": "Code 5"
        }
    }
}
```

### Deleting an external inventory code

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/external-inv-code?id=102'
{
    "response": {
        "status": "OK"
    }
}
```
