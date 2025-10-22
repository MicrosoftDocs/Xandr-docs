---
title: Seller Creative Review Service
description: Use the Seller Creative Review service report to get an insight into how seller members audit the creatives.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Seller Creative Review service

> [!NOTE]
> This service currently is in **Beta**. It is still under development and may be subject to change without notice. Contact your Xandr Account Representative to get enabled.

The Seller Creative Review Service is designed to give you an insight into how seller members audit the creatives.

Xandr works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. Buyers must submit creatives to Xandr so that they can be audited before running on Xandr real-time inventory. Creatives that fail the Xandr platform audit will not run. For more information, see [Auditing Creatives](../monetize/auditing-creatives.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/seller-creative-review?member_id=MEMBER_ID&creative_id=CREATIVE_ID` | Create a seller-creative review |
| `GET` | `https://api.appnexus.com/seller-creative-review?member_id=MEMBER_ID&creative_id=CREATIVE_ID` | View the details of a seller-creative review |
| `PUT` | `https://api.appnexus.comseller-creative-review?member_id=MEMBER_ID&creative_id=CREATIVE_ID` | Update a seller-creative review |
| `DELETE` | `https://api.appnexus.com/seller-creative-review?member_id=MEMBER_ID&creative_id=CREATIVE_ID` | Delete a seller-creative review |

## JSON fields

The seller-creative-review object includes the following JSON fields:

| Field | Type | Description |
|:---|:---|:---|
| `audit_feedback` | string | Consists of a brief description of the `audit_status` field. |
| `audit_status` | enum | The audit status could consist of one of the following parameters:<br> - `no_audit`<br> - `rejected`<br> - `approved`<br> - `pending`<br><br>**Required on**: `PUT` and `POST` |
| `brand_id` | integer | ID of an undeleted brand. This field cannot be `null`.<br>It is recommended to use the existing values for this field, instead of setting the values to default (i.e. `brand_id=1` or `language_id=0`).<br><br>**Required on**: `PUT` and `POST` |
| `created_on` | string | **Read-only**. The date and time at which the object was created. |
| `creative_id` | integer | If (`creative_id`, `member_id`) record is deleted, it can be recreated using the `POST` method. There can be multiple entries for one `creative_id` from different members. |
| `deleted` | boolean | **Read-only**. An indicator that refers if the object was deleted or not. |
| `id` | integer | **Read-only**. The ID of the object. |
| `language_id` | integer | The language ID of the creative. For more information, see [Language Service](./language-service.md).<br>It is recommended to use the existing values for this field, instead of setting the values to default (i.e. `brand_id=1` or `language_id=0`).<br><br>**Required on**: `PUT` and `POST` |
| `last_modified` | string | **Read-only**. The date and time at which the object was last modified. |
| `member_id` | integer | The ID of the member that is creating or modifying the object.<br><br>**Required on**: `PUT` and `POST` |
| `deal_audit_statuses` | array of objects | Deal specific audit statuses indicate a creative’s approval/rejection status for a specific deal. |

### Deal audit statuses

| Field | Type | Description |
|:---|:---|:---|
| `deal_id` | integer | The ID of an existing deal. |
| `audit_status` | enum | The audit status could consist of one of the following parameters:<br> - `no_audit`<br> - `rejected`<br>- `approved`<br> - `pending` |
| `audit_feedback` | string | Consists of a brief description of the `audit_status` field. |

## Examples

### Create a seller creative review

```
curl -X POST 'https://api.appnexus.com/seller-creative-review?member_id=2715&creative_id=55' -H 'Authorization: authn:3190:10e35ec51ee63:nym2' -d '{"seller-creative-review": {"audit_status": "rejected", "audit_feedback": "Does not meet standards", "language_id": 23,"brand_id": 306}}'
```

The payload returned:

```
{ 
 "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "dbg_info": {
      "output_term": "seller-creative-review",
      "warnings": null,
      "version": "1.18"
    },
    "seller-creative-review": {
      "audit_feedback": "Does not meet standards",
      "audit_status": "rejected",
      "brand_id": 306,
      "created_on": "2022-02-02 17:08:01",
      "creative_id": 55,
      "deleted": false,
      "id": 32,
      "language_id": 23,
      "last_modified": "2022-02-04 21:21:11",
      "member_id": 2715,
      "deal_audit_statuses": null      
    }
  }
}
```

### Create a seller creative review with deal audit statuses

```
curl -X POST 'https://api.appnexus.com/seller-creative-review?member_id=2715&creative_id=55' -H 'Authorization: authn:3190:10e35ec51ee63:nym2' -d '{"seller-creative-review": {"audit_status": "approved", "audit_feedback": "Meets standards", "language_id": 23,"brand_id": 306,"deal_audit_statuses": [{"deal_id": 1,"audit_status": "rejected","audit_feedback": "Deal audit feedback"}]}}'
```

The payload returned:

```
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "dbg_info": {
      "output_term": "seller-creative-review",
      "warnings": null,
      "version": "1.18"
    },
    "seller-creative-review": {
      "audit_feedback": "Meets standard",
      "audit_status": "approved",
      "brand_id": 306,
      "created_on": "2022-02-02 17:08:01",
      "creative_id": 55,
      "deleted": false,
      "id": 32,
      "language_id": 23,
      "last_modified": "2022-02-04 21:22:59",
      "member_id": 2715,
      "deal_audit_statuses": [
        {
            "deal_id": 1,
            "audit_status": "rejected",
            "audit_feedback”: "Deal audit feedback"
        }
      ]
    }
  }
}
```

### View the details of a seller creative review

```
curl -X GET 'https://api.appnexus.com/seller-creative-review?member_id=2715&creative_id=55' -H 'Authorization: authn:3190:10e35ec51ee63:nym2'
```

The payload returned:

```
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "dbg_info": {
      "output_term": "seller-creative-reviews",
      "warnings": null,
      "version": "1.18"
    },
    "seller-creative-reviews": [
      {
        "audit_feedback": "Does not meet standards",
        "audit_status": "rejected",
        "brand_id": 306,
        "created_on": "2022-02-02 17:08:01",
        "creative_id": 55,
        "deleted": false,
        "id": 32,
        "language_id": 23,
        "last_modified": "2022-02-04 21:21:11",
        "member_id": 2715,
        "deal_audit_statuses": null
      }
    ]
  }
}
```

### Update a seller creative review

```
curl -X PUT 'https://api.appnexus.comseller-creative-review?member_id=2715&creative_id=55' -H 'Authorization: authn:3190:10e35ec51ee63:nym2' -d '{"seller-creative-review": {"audit_status": "approved", "audit_feedback": "Meets standards", "language_id": 23,"brand_id": 306}}' 
```

The payload returned:

```
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "dbg_info": {
      "output_term": "seller-creative-review",
      "warnings": null,
      "version": "1.18"
    },
    "seller-creative-review": {
      "audit_feedback": "Meets standards",
      "audit_status": "approved",
      "brand_id": 306,
      "created_on": "2022-02-02 17:08:01",
      "creative_id": 55,
      "deleted": false,
      "id": 32,
      "language_id": 23,
      "last_modified": "2022-02-04 21:22:59",
      "member_id": 2715,
      "deal_audit_statuses": null
    }
  }
}
```

### Delete a seller creative review

```
curl -X DELETE 'https://api.appnexus.com/seller-creative-review?member_id=2715&creative_id=55' -H 'Authorization: authn:3190:10e35ec51ee63:nym2'
```

The payload returned:

```
{
  "response": {
    "status": "OK",
    "count": 0,
    "start_element": 0,
    "num_elements": 0,
    "dbg_info": {
      "output_term": "not_found",
      "warnings": null,
      "version": "1.18"
    }
  }
}    
```
