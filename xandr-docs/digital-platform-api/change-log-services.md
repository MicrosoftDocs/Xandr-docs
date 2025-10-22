---
title: Change Log Services
description: In this article, learn about the Change Log services, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Change Log services

## Overview

The read-only Change Log and Change Log Detail Services are used in conjunction with other services (listed below) to retrieve information about changes that have been made to a set of objects. This page describes the use of these two services to retrieve a list of the logged changes in which you are interested. The Change Log service is only available to users with the `"member"`, `"advertiser"`, or `"member_advertiser"` user type.

> [!NOTE]
> The Change Log service has some minor differences from other Xandr API services as mentioned below:
>
> - The `min_last_modified` option used for date filtering is replaced by `min_timestamp`.
> - The `last_modified` option is not supported. Use `created_on` instead.

## REST API for retrieving the ID of a change

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/change-log?service=SERVICE&resource_id=ID](https://api.appnexus.com/change-log?service=SERVICE&resource_id=ID) | Retrieve ID of a change incurred to a resource. |
| `POST` | [https://api.appnexus.com/change-log](https://api.appnexus.com/change-log)<br>(Change log JSON) | Posting an ID of change for a resource. |

## JSON fields for Change Log service

> [!NOTE]
>
> - The Change Log service is read-only; however, some fields can be used in a `POST` call to filter the response. However, all the fields are not used in `POST` calls, so `GET` is recommended.
> - The Change Log service contains at least 6 months of data, if not more, for every service.

### Fields accepted as inputs to the endpoint

| Field | Type | Description |
|:---|:---|:---|
| `service` | string | The service used to make the change. Below are few of the examples of possible values:<br> - `insertion-order`<br> - `line-item`<br> - `campaign`<br> - `profile`<br><br>**Note:** Currently, `budget-splitter` service is in block-list.<br>**Required:** Yes<br>**Filter:** Yes |
| `resource_id` | int | The ID of the object used to make the change.<br>**Required:** Yes<br>**Filter:** Yes |
| `additional_fields` | string<br> - For `GET` requests, this is a group of comma separated strings. For example, `additional_fields = request_source`, `user_id`, `object_json`<br> - For `POST` requests, this is a string array. For example, `"additional_fields":["request_source","user_id","object_json”]` | This field allows the users to add additional data in the response. The  `additional_fields` can include additional return fields. Examples of accepted values are:<br> - `request_source`<br> - `user_id`<br> - `object_json`<br>**Required:** No  <br>**Filter:** No |

### Fields returned in the response from the endpoint

| Field | Type | Description |
|:---|:---|:---|
| `min_timestamp` | timestamp | The date and time of the earliest modification to the object, in `YYYY-MM-DD` or `YYYY-MM-DD` `HH:MM:SS` format. |
| `max_timestamp` | timestamp | The date and time of last modification to the object, in `YYYY-MM-DD` or `YYYY-MM-DD` `HH:MM:SS` format. |
| `start_element` | int | By default, the `change-log` service will return 100 transactions or less. If there are more transactions, use `start_element` to set the offset. Enter in the query string. Can be included in both `GET` and `POST` requests. |
| `num_elements` | int | By default, the `change-log` service will return 100 transactions or less. If there are more transactions, use `num_elements` to retrieve the specified number of transactions. Enter in the query string. Can be included in both `GET` and `POST` requests. |
| `service` | string | The service used to make the change. |
| `resource_id` | int | The ID of the object used to make the change. |
| `additional_fields` | string | This field returns additional data in the response as specified in the input. |
| `transaction_id` | int | The ID of the change transaction accepted as input to the endpoint. |
| `resource_id` | int | The ID of the object used to make the change. |
| `created_on` | timestamp | The date and time of the modification to the object in `YYYY-MM-DD` `HH:MM:SS` format. |
| `sort` | string | A string of the format, `“FIELD.[asc\|desc]”`. For example, `created_on.asc` for ascending sort on `created_on`. Currently, only sorting on `created_on` is permitted. |
| `modified_by_admin` | boolean | Filter by items that are modified by the administrators only.<br><br>**Note:** This request parameter is only usable in `GET` requests. |
| `modified_by_plugin` | boolean | Filter by items that are modified by the plugins only.<br><br>**Note:** This request parameter is only usable in `GET` requests. |
| `transactions_with_changes` | boolean | Filter by items that have changes. |

## REST API for retrieving the details of a change

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/change-log-detail?service=SERVICE&resource_id=ID&transaction_id=ID](https://api.appnexus.com/change-log-detail?service=SERVICE&resource_id=ID&transaction_id=ID) | Fetch the details of a change to resource. |
| `POST` | [https://api.appnexus.com/change-log-detail](https://api.appnexus.com/change-log-detail)<br>(Change log detail JSON) | Post the details of a change to a resource.  |

## JSON fields for Change Log Details service

> [!NOTE]
> The Change Log Details service is read-only; however, some fields can be used in a `POST` call to filter the response.

### Fields accepted as inputs to the endpoint in Change Log Details service

| Field | Type | Description |
|:---|:---|:---|
| `service` | string | The service used to make the change.<br>**Required:** Yes<br>**Filter:** Yes |
| `transaction_id` | int | The ID of the change transaction accepted as input to the endpoint.<br>**Required:** Yes<br>**Filter:** Yes |
| `previous_object` | boolean | When **true**, the difference between queried and previous transaction is displayed. Otherwise the difference between queried and next transaction is shown by default. This input can be passed either in query parameter or in request body.<br>**Default**: false<br>**Required**: No<br>**Filter**: Yes |

### Fields returned in the response from the endpoint in Change Log Details service

| Field | Type | Description |
|:---|:---|:---|
| `created_on` | timestamp | The date and time of the modification to the object in `YYYY-MM-DD` `HH:MM:SS` format. |
| `user_id` | int | The ID of the user who made the modification. |
| `method` | enum | The API method used to make the change. Possible values are:<br> - `"put"`<br> - `"post"`<br> - `"delete"` |
| `url` | string | The URL of the original request. |
| `changes` | array of objects | Details about the changes made to the object returned. Each object in the `changes` array contains [fields](#changes-object). |
| `plugin_id` | int | The ID of the plugin that made the modification. If `null`, a plugin did not make the modification (and a user did). For more information on a plugin, see the [Plugin Service](plugin-service.md). |
| `transaction_id` | int | The ID of the change transaction accepted as input to the endpoint. |
| `member_id` | int | The ID of the member who initiated the change. |
| `num_of_changes` | int | The number of fields changes made to the object. It corresponds to number of `"changes"` fields where the value of `"changed"` is `true`. |
| `modified_by_admin` | boolean | Specifies if the changes are initiated by an administrator. |
| `admin_id` | int | The ID of the administrator who initiated the change. |
| `user_full_name` | string | The name of the user who made the modification. It corresponds to the `"user_id"` field returned in the response. |
| `resource_id` | int | The ID of the object used to make the change. |
| `raw_json` | string | **Read-only.** The full data object JSON before the change transaction. The `raw_json` value for this transaction is compared to the value for the last transaction to deduce what has changed. |
| `session_id` | string | **Read-only.** The authentication token of the user used to access the API. |
| `internal_txn` | boolean | **Read-only.** If `true`, this is an internal transaction (i.e., the API call was triggered by another internal API call). |
| `request_source` | enum | **Read-only.** Where the API request originated. Possible values:<br> - `"hbui"`: Indicates the request is from UI.<br> - `"direct"`: Indicates the request is from direct API calls.<br> - `"LIAA-allocation"`: Indicates that the update was done in the line item edit form<br> - `"bmwBulkEdit"` and `"LIAA-blkupld"`: Indicates that the updates were done in bulk edits and bulk import respectively.<br> - `"bmwInlineEdit"`: Indicates that the user clicked on the pencil icon in the details page that allows to edit individual sections.<br> - `"LIAA-dup"`: Indicates that it was through the duplication process. <br><br>**Note:** that this value will show only in POST calls. |
| `client_ip` | string | **Read-only.** The IP address of the client. |
| `ip_info` | string | **Read-only.** The chain of IP addresses if the request is from proxies. |

#### `changes` object

| Field | Type | Description |
|:---|:---|:---|
| `field_name` | string | **Read-only.** The name of the field changed. |
| `old_value` | Any (int/string/boolean/timestamp etc.) | **Read-only.** The old value of the field. |
| `new_value` | Any (int/string/boolean/timestamp etc.) | **Read-only.** The new value of the field. Data type of `new_value` is same as `old_value`. |
| `changed` | boolean | **Read-only.** If `true`, it implies that the value of the field is change Log Services#Changed. |

## Examples

### Retrieve Change Log Details using `GET`

#### Step 1: Call `/change-log` to get transactions for a desired `resource_id`

`GET` to `/change-log`.

```
$ curl -b cookies 'https://api.appnexus.com/change-log?service=line-item&resource_id=13984849'
{
"response": {
"change_logs": [
{
"transaction_id": "4ba6d032-68ef-544e-9f01-49aa6b36b0b4",
"created_on": "2021-02-12 15:24:27",
"resource_id": 13984849
},
{
"transaction_id": "0ee74310-f580-5001-8007-2f71f84a5454",
"created_on": "2021-02-12 15:14:50",
"resource_id": 13984849
}
],
"start_element": 0,
"num_elements": 100,
"count": 2,
"status": "OK"
}
}
```

`GET` to `/change-log` with `"additional_fields"` parameter.

```
$ curl -b cookies 'https://api.appnexus.com/change-log?service=line-item&resource_id=13984849&additional_fields=request_source,user_id,object_json'
{
"response": {
"change_logs": [
{
"transaction_id": "2b11b163-c8a6-5c8b-b3d2-6e580d41d929",
"object_json": "{\"id\":13984849,\"code\":null,...}",
"created_on": "2021-03-03 17:05:53",
"user_id": [redacted],
"resource_id": 13984849,
"request_source": "LIAA-blkupld"
},
...
],
"start_element": 0,
"num_elements": 1,
"count": 1,
"status": "OK"
}
}
```

#### Step 2: Call `/change-log-detail` with the `transaction_id`

`GET` to `/change-log-detail`.

```
$ curl -b cookies 'https://api.appnexus.com/change-log-detail?service=line-item&transaction_id=0ee74310-f580-5001-8007-2f71f84a5454'
{
"response": {
"change_log_details": [
{
"transaction_id": "0ee74310-f580-5001-8007-2f71f84a5454",
"member_id": 364,
"raw_json": "{\"line-item\":{\"advertiser_id\":4143132,\"currency\":\"GBP\",...}",
"plugin_id": "",
"method": "PUT",
"changes": [
{
"field_name": "advertiser_id",
"old_value": 4143132,
"new_value": 4143132,
"changed": false
},
...
],
"session_id": "authn:234473:42824ee8a5453:nym2",
"internal_txn": false,
"url": "https://hbapi-proxy-production/line-item?id=13984849&advertiser_id=4143132",
"request_source": "LIAA-blkupld",
"num_of_changes": 2,
"created_on": "2021-03-03 17:05:53",
"user_id": [redacted int value],
"modified_by_admin": true,
"admin_id": 0,
"user_full_name": "Test User",
"resource_id": 13984849,
"client_ip": "[redacted]",
"ip_info": "[redacted]"
}
],
"start_element": 0,
"num_elements": 1,
"count": 1,
"status": "OK"
}
}
```

### Retrieve Change Log Details using `POST`

> [!NOTE]
> The code samples in the steps below show how a user retrieves changes made to advertiser 5260730 between 17:00:00 on March 3, 2021 and 18:00:00 on March 3, 2021.

#### Step 1: Create a JSON-formatted change log request

The JSON file should include the `service` and `resource_id` of the change logs you want to view, as well as the `min_timestamp` and `max_timestamp` to limit change logs to a specific time period. You can also use `start_element` or `num_elements` in the query string.

Create `change-log` JSON.

```
$ cat change-log.json
{
"change-log" : {
"service" : "advertiser",
"resource_id": "5260730",
"min_timestamp" : "2021-03-03 17:00:00",
"max_timestamp" : "2021-03-03 18:00:00"
}
}
```

#### Step 2: `POST` the request to the Change Log Service

`POST` the JSON request to get back basic change log information, including the `transaction_id`.

`POST` to `/change-log`.

```
$ curl -b cookies -X POST -d @change-log.json 'https://api.appnexus.com/change-log'
{
"response": {
"change_logs": [
{
"transaction_id": "016ac252-aa30-5d10-a7a0-b5b3d88df832",
"created_on": "2021-03-03 17:16:07",
"resource_id": 5260730
}
],
"start_element": 0,
"num_elements": 100,
"count": 1,
"status": "OK"
}
}
```

#### Step 3: Create a JSON-formatted change log detail request

The JSON file should include the `service` and `transaction_id` of the change log for which details you want to view.

Create `change-log-detail` JSON.

```
$ cat change-log-detail.json
{
"change-log-detail" : {
"service" : "advertiser",
"transaction_id": "016ac252-aa30-5d10-a7a0-b5b3d88df832",
"previous_object": "true"
}
}
```

#### Step 4: `POST` the request to the Change Log Detail Service

`POST` the JSON request to get back a detailed change log for the change corresponding to the `transaction_id`.

`POST` to `/change-log-detail`.

```
$ curl -b cookies -X POST -d @change-log-detail.json 'https://api.appnexus.com/change-log-detail'
{
"response": {
"change_log_details": [
{
"transaction_id": "016ac252-aa30-5d10-a7a0-b5b3d88df832",
"member_id": 7823,
"raw_json":"{\"advertiser\":{\"id\":0,\"code\":\"0080459398\",...}",
"plugin_id": "",
"method": "POST",
"changes": [
{
"field_name": "allow_safety_pacing",
"old_value": null,
"new_value": null,
"changed": false
},
{
"field_name": "billing_address1",
"old_value": null,
"new_value": "New Address",
"changed": true
},
...
],
"session_id": "authn:206221:8d1c33b7fadc3:ams3",
"internal_txn": false,
"url": "https://api.appnexus.com/advertiser",
"request_source": "direct",
"num_of_changes": 25,
"created_on": "2021-03-03 17:16:07",
"user_id": [redacted],
"modified_by_admin": true,
"admin_id": 0,
"user_full_name": "Test",
"resource_id": 5260730,
"client_ip": "[redacted]",
"ip_info": "[redacted]"
}
],
"start_element": 0,
"num_elements": 1,
"count": 1,
"status": "OK"
}
}
```
