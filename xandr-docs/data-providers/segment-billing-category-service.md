---
title: Segment Billing Category Service
description: In this article, learn about Segment Billing Category Service, their JSON fields, and REST API with a detailed set of examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Segment billing category service

The Segment Billing Category Service allows you to **map** your segments to your Data Marketplace pricing taxonomy. Here's how it works:

1. You create a mapping record for a segment that you activate in the Data Marketplace.
1. In the mapping record, you specify which pricing category the segment should be assigned to. Clients that you've shared your segment with can now target that segment in campaigns and Xandr will clear the cost of usage.

> [!NOTE]
>
> - This service allows you to map to existing categories. To create a new category, reach out to your Xandr representative.
> - When you remove a segment from a mapping record, the member can continue to use the segment in a campaign but Xandr will stop tracking the cost of data usage.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/data-provider](https://api.appnexus.com/data-provider) | View all of your pricing taxonomy. |
| `GET` |  [https://api.appnexus.com/segment-billing-category](https://api.appnexus.com/segment-billing-category)  | View all of your mapping records. |
| `POST` |  [https://api.appnexus.com/segment-billing-category](https://api.appnexus.com/segment-billing-category) (mapping JSON)<br><br>**Note:** Only one segment can be mapped at a time. | Add a mapping record. |
| `PUT` | [https://api.appnexus.com/segment-billing-category](https://api.appnexus.com/segment-billing-category) (mapping JSON) | Modify a mapping record. |
| `DELETE` | [https://api.appnexus.com/segment-billing-category?id=RECORD_ID](https://api.appnexus.com/segment-billing-category?id=RECORD_ID) | Delete a mapping record. |

> [!TIP]
> **JSON structure:**
>
> When adding or updating a mapping record, you should structure the JSON as a single object called "`segment-billing-category`". For exact formatting, see the [examples](#examples) below.
>
> The Segment Billing Category service works on BOTH the platform API as well as the impression bus API. Although only `api.adnxs.com` is used below, it may be replaced with `api.appnexus.com` for those clients who have access to the platform API. Only members who are on will have access to the platform API. The majority of data providers can only access the impression bus API.

## JSON fields

| Field | Type (Length) | Description | Default | Required On |
|:---|:---|:---|:---|:---|
| `id` | int | The unique ID created when a Xandr segment ID is mapped to a billing category. It can be referred as the mapping ID per record. | Auto-generated number | `PUT` (in JSON)<br>`DELETE` (in query string) |
| `segment_id` | int | The Xandr segment ID that is being mapped. |  | `POST`/`PUT` |
| `data_provider_id` | int | The data provider ID assigned to you by the Data Marketplace. <br>**Note:** The `POST`/`CALL` call will fail if you submit an ID that is not owned by your account. |  | `POST`/`PUT` |
| `data_category_id` | int | The pricing category ID created on Xandr. <br>**Note:** The `POST`/`PUT` calls will fail if you submit an ID that is not owned by your account. |  | `POST`/`PUT` |
| `active` | boolean | The status of the mapping record. If set to `true`, mapping record is active. |  | `POST` |
| `member_id` | int | **Read-only.** Your member ID. |  |  |
| `is_public` | boolean | The setting to mark the segment as public or **private**. If set to `true`, then the segment is shared with all Data Marketplace buyers immediately. | `false` | `PUT` |
| `data_segment_type_id` | string | The type of segment. This makes it easy for buyers to search for specific types of segments. For Brand Safety and Fraud Detection segment types, ensure that the `recommend_include` field (see below) is set to the proper value for the type of segment.<br>Valid options are:<br> - unassigned<br> - Audience<br> - Brand Safety<br> - Fraud Detection<br> - Viewability<br> - Contextual<br> - Geolocation<br> - B2B<br> - Purchase<br> - Interest<br> - Demo<br> - In-Market | unassigned |  |
| `recommend_include` | boolean | Determines if a segment is intended for inclusion (`true`) or exclusion (`false`). By default, it is set to `false` which is an exclusion; set to `true` if the segment is intended for inclusion. Ensure that this field is set to the proper value for the type of segment. | `false` |  |

## Pagination

You can paginate results by specifying `start_element` and `num_elements` in the query string of the `GET` request. For example, the following request would return 25 items starting from element 26:

```
curl -b cookies -c cookies 'https://api.appnexus.com/segment-billing-category?start_element=26&num_elements=25'
```

| Field | Type | Description |
|---|---|---|
| `count` | int | Total number of results. |
| `start_element` | int | Element number at which to start result set. |
| `num_elements` | int | Number of elements to return, max = 100, default = 25. |

## Examples

### View your pricing taxonomy

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/data-provider'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 25,
    "dbg_info": {
      "instance": "01.data-clearing-api.prod.nym2",
      "db": "",
      "warnings": [],
      "start_microtime": 1459912197.525,
      "time": 14,
      "version": "",
      "output_term": "data-providers"
    },
    "data-providers": [
      {
        "id": 1,
        "node_name": "Sample Data Provider Name",
        "member_id": 958,
        "data_revshare_pct": 0.01,
        "active": true,
        "data_publishers": [
          {
            "id": 1,
            "node_name": "Sample Data Publisher Name",
            "level_index": 0,
            "data_provider_id": 958,
            "active": true,
            "member_id": 958,
            "data_categories": [
              {
                "id": 1001,
                "node_name": "Sample Data Category Name",
                "level_index": 0,
                "data_publisher_id": 1,
                "data_provider_id": 958,
                "active": true,
                "member_id": 958
              }
            ]
          }
        ]
      }
    ]
  }
}
```

### Create a mapping record

```
$ cat create_segment_mapping
{
        "segment-billing-category": {
                "active": true, 
                "data_provider_id": 958,
                "data_category_id": 1001,
                "segment_id": 111111,
                "is_public": true,
                "data_segment_type_id": "Audience"
        }
}
$ curl -b cookies -c cookies -X POST -d @create_segment_mapping 'https://api.appnexus.com/segment-billing-category?member_id=958'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 25,
    "segment_billing_categories": [
      {
        "id": 22286,
        "segment_id": 111111,
        "data_provider_id": 958,
        "data_category_id": 1001,
        "active": true,
        "member_id": 958,
                "is_public": true,
                "data_segment_type_id" : "Audience"
      }
    ]
  }
}
```

### Update a mapping record

```
$ cat update_segment_mapping
{
        "segment-billing-category": {
                "id": 22286,
                "active": false,
                "is_public": true,
                "data_provider_id": 958,
        "data_category_id": 1001,
                "data_segment_type_id": "Contextual"
        }
}
$ curl -b cookies -c cookies -X PUT -d @update_segment_mapping 'https://api.appnexus.com/segment-billing-category?member_id=958'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 25,
    "segment_billing_categories": [
      {
        "id": 22286,
        "segment_id": 111111,
        "data_provider_id": 958,
        "data_category_id": 1001,
        "active": false,
        "member_id": 958,
                "is_public": true,
                "data_segment_type_id": "Contextual"
      }
    ]
  }
}
```

### Remove a mapping record

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/segment-billing-category?member_id=958&id=22286'
{
  "response": {
    "status": "OK",
    "count": 0,
    "start_element": 0,
    "num_elements": 0,
    "segment_billing_category": null
  }
}
```

### View all of your mapping records

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/segment-billing-category'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 25,
    "segment_billing_categories": [
      {
        "id": 22286,
        "segment_id": 111111,
        "data_provider_id": 958,
        "data_category_id": 1001,
        "active": true,
        "member_id": 958,
                "is_public": true,
                "data_segment_type_id": "Contextual"
      }
    ]
  }
}
```
