---
title: Report Member Access Service
description: Explore the Report Member Access service, allowing users to modify access permissions for restricted reports.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Report Member Access service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

It updates the data stored in `bidder.rpt_report_member_access`.

> [!NOTE]
> Only `GET`, `POST`, and `DELETE` is supported for this service.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/rpt-report-member-access`<br>(template JSON) | Add a new report-member-access setting. |
| `DELETE` | `https://api.appnexus.com/object?id=REPORT_MEMBER_ACCESS_ID`<br><br>**Note:** `REPORT_MEMBER_ACCESS_ID` is a uniquely generated ID for the given setting and can be retrieved via `GET`. | Delete a custom template. |
| `GET` | `https://api.appnexus.com/rpt-report-member-access`| View all report-member-access settings. |
| `GET` | `https://api.appnexus.com/rpt-report-member-access?report_id=REPORT_ID` | View report-member-access settings for a specific report. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the report member access setting.<br>**Default:** Auto-generated number.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `member` | object | An object with an id of the member for which you're adding access.<br>**Default:** `None`<br>**Required On:** `POST` |
| `report` | object | An object with an id of the report for which you're adding access.<br>**Default:** `None`<br>**Required On:** `POST` |

## Examples

### View all members who have access to a specific report

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/rpt-report-member-access?report_id=44'
{
  "response": {
    "status": "OK",
    "count": 28,
    "start_element": 0,
    "num_elements": 100,
    "rpt-report-member-accesss": [
      {
        "id": 27,
        "last_modified": "2013-03-01 20:37:01",
        "member": {
          "id": 357,
          "billing_name": "OpenX"
        },
        "report": {
          "id": 44,
          "name": null
        }
      },
      {
        "id": 28,
        "last_modified": "2013-04-09 18:13:25",
        "member": {
          "id": 459,
          "billing_name": "Rubicon"
        },
        "report": {
          "id": 44,
          "name": null
        }
      },
        ...
}
```

### Give a member access to a specific report

```
$ cat rpt_report_member_access

{
    "rpt-report-member-access": {
        "report": {
            "id":44
        },
        "member": {
            "id": 123
        }
}
```

```
$ curl -b cookies -c cookies -X POST -d @rpt-report-member-access 'https://api.appnexus.com/rpt-report-member-access'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "rpt-report-member-access": {
        "id": 77,
        "last_modified": "2015-01-15 20:37:01",
        "member": {
          "id": 123,
          "billing_name": "MemberName"
        },
        "report": {
          "id": 44,
          "name": null
        }
      }
        }
...
}
```
