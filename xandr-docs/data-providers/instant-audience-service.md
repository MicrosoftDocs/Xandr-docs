---
title: Data Providers - Instant Audience Service
description: In this page, learn what Instant Audience Service is and how you can configure it. This module also discusses how to Add/Remove users from segments.
ms.custom: data-providers
ms.date: 11/30/2023
---

# Data Providers - Instant audience service

> [!NOTE]
> Alpha-Beta Notice: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.

The Instant Audience Service is a server-side method that uses a streaming architecture to add individual or small groups of users to segments, via the Digital Platform API. Rather than aggregating and periodically sending large batches of data using the Batch Segment Service, the Instant Audience Service associates' users to segments in close to real-time. Our target SLA for adding users to segments with this service is 2 minutes. This is useful if you have real-time audience remodeling requirements.

## Configure the service

If you're already using the Batch Segment Service, you can skip this part and proceed to [Authenticate](#authenticate). If you're a brand-new client and wish to start using the Instant Audience Service, you will need to open a ticket with and provide the following information:

1. Are you using external user IDs (i.e., you use mapUID to store the mapping with Xandr)? If you use another member's external user IDs, include their `member_id` as well.
1. Do you need to populate segments belonging to other members? If so, provide the associated `member_ids`.
1. When you would like your segments to expire by default (e.g., never expire, expire 60 days from now, etc.)? Note that if you include EXPIRATION in your seg block, your default expiration will not be used.
1. The following questions are for our internal capacity planning:
    - What is the number of unique user IDs per post?
    - What is the number of expected posts per day?
    - What is the number of unique segments per post?

## Authenticate

Refer to the [Authentication Service](../digital-platform-api/authentication-service.md) for a general overview on how to make calls to the Xandr API. Just like any other service, you'll authenticate against `https://api.appnexus.com`. However, subsequent calls will be made to the Instant Audience Service at `https://streaming-data.appnexus.com`.

> [!NOTE]
> In the authentication response, make note of the token as it will be needed for subsequent calls to the Instant Audience Service.

Example response from the Authentication Service:

``` 
{
    "response": {
        "status": "OK",
        "token": "hbapi:123456:9876abcd54321:nym2",
        "dbg_info": {
            ...
        }
    }
}                     
```

The token returned in the response must be included in subsequent calls to the Instant Audience Service in the authorization header or as an `access_token` query string parameter, as shown in the following examples:

**Authorization header**

`curl -X POST -H "Authorization: hbapi:123456:9876abcd54321:nym2" https://streaming-data.``appnexus``.com/rt-segment`

**Query string**

`curl -X POST https://streaming-data.``appnexus``.com/rt-segment?access_token=hbapi:123456:9876abcd54321:nym2`

## Add/Remove users from segments

After authenticating, you're now ready to add/remove a user to/from a segment, via a JSON file.

> [!NOTE]
> Wait approximately 20 minutes before trying to add users to any newly created segments (to allow these segments to be propagated to all servers). As a best practice, try to:
>
> - Minimize the creation of new segments.
> - Wherever possible, re-use existing segments.
> - Use segment `values` to further sub-divide users within existing segments.
>
> These practices will ensure successful user add/remove to/from segments. For details on creating segment `values`, see [Segment Pixels: Advanced](../invest/segment-pixels-advanced.md) and [Segment Targeting](../monetize/segment-targeting.md) in Xandr documentation.

The following example demonstrates how to assign a user to two segments. In this example, the member is adding user ID 12345678900987654321 (this is a Xandr user id) to segments 10001 and 10002, setting both associations with value = 1 and expiration within 1440 minutes.

### Assign a user to two segments example

| API Call | JSON Payload | Response |
|--|--|--|
| `curl -X POST -H "Authorization: hbapi:123456:9876abcd54321:nym2" -d @json/segment.json "https://streaming-data.appnexus.com/rt-segment"` | `{ "rt_segment": [ { "user_id": "12345678900987654321", "seg_block": [ { "seg_id": 10001, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null }, { "seg_id": 10002, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null } ], "domain": null } ] }` | `{ "response": { "status": "OK", "message": { "users_in_request": 1, "segments_in_request": 2 }, "warnings": [ ] }` |

## JSON fields

### `rt_segment array`

| Field | Type | Description |
|--|--|--|
| `user_id` | string | This is either the Xandr `user_id` or an ID based on the domain, such as "AEBE52E7-03EE-455A-B3C4-E57283966239", as an example of a device identifier.<br>**Required**: At least one. |
| `seg_block` | array | Array of segment blocks for segments to associate with the user (see segment block structure below).<br>**Required**: At least one. |
| `domain` | string | Type of identifier being used in the request, such as Xandr user ID (represented with `null`) or device identifier (`idfa`, `sh1udid`, `md5udid`, `openudid`, and `aaid`).<br>**Note**: Do not use `sha1mac`, which was deprecated in 2019. |

### `seg_block array`

| Field | Type | Description |
|--|--|--|
| `seg_id` | int | The Xandr segment ID.<br>**Required**: If not using `seg_code` and `member_id` to identify segment. |
| `seg_code` | string | A user-defined name for the segment.<br>**Note**: You may either include `SEG_CODE` and `member_id` or `SEG_ID`, but not both.<br>**Required**: If not using `seg_ID` to identify segment. |
| `value` | int | A numeric value you would like to assign to a segment. |
| `expiration` | int | The lifetime of the user-segment association in minutes, starting from when we read it. A value of `0` means that the segment will never expire; `-1` means that the user will be removed from this segment. |
| `member_id` | int | The member ID of the segment owner for the seg_block.<br>**Required**: If using `seg_code`. |

### `Response`

| Field | Type | Description |
|--|--|--|
| `status` | string | Describes whether the add/remove went through or resulted in an error. |
| `users_in_request` | int | The number of users read in the request.<br>**Note**: This will simply show the number of users initially detected in the request regardless of whether they are valid. |
| `segments_in_request` | int | The number of segments read in the request.<br>**Note**: This will simply show the number of segments initially detected in the request regardless of whether they are valid in our system, and without regard to what users they are being associated with in the call. |

## Additional POST scenarios

### Device ID (IDFA)

| REST API call | JSON Payload | Response |
|--|--|--|
| `curl -X POST -H "Authorization: hbapi:123456:9876abcd54321:nym2" -d @json/segment.json "https://streaming-data.appnexus.com/rt-segment"` | `{ "rt_segment": [ { "user_id": "1ba98a6c-d1a5-49ef-ad1c-2d9230ebcd13", "seg_block": [ { "seg_id": 12, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null }, { "seg_id": 23784, "seg_code": null, "value": 1, "expiration": 0, "member_id": null } ], "domain": "idfa" } ] }` | `{ "response": { "status": "OK", "message": { "users_in_request": 1, "segments_in_request": 2 }, "warnings": [ ] } }` |

### Codes for other members

| REST API call | JSON Payload | Response |
|--|--|--|
| `curl -X POST -H "Authorization: hbapi:123456:9876abcd54321:nym2" -d @json/segment.json "https://streaming-data.appnexus.com/rt-segment"` | `{ "rt_segment": [ { "user_id": "12345678900987654321", "seg_block": [ { "seg_code": "abcd", "value": 1, "expiration": 1440, "member_id": 1661 }, { "seg_code": "zywx", "value": 1, "expiration": 1440, "member_id": 1262 } ], "domain": null } ] }` | `{ "response": { "status":"OK", “users_in_request”: 1, "segments_in_request": 2 } }` |

## Service limits

> [!NOTE]
> Service limits may change during alpha and beta testing of this service.

In order to adhere to a maximum of 2 minutes activation time, the Instant Audience Service currently has the following limits:

|  |  |  |
|---|---|---|
| **Call Rate** | - Up to 100 POST calls per second (per member) and up to 1000 GET calls per second (per member). If you exceed this rate limit, the following message will be returned: "Rate limit exceeded. You have exceeded your request limit of 1000 reads per 1 seconds to rt-segment-processed, please wait and try again or contact Xandr for higher limits". |  |
| **Objects** | - Up to 1000 users per second.<br> - Up to 100 segments per user per call. |  |
| **Payload Size** | - The JSON payload should not exceed 1MB. |  |

## Example error scenarios

### Add/Remove over 1000 users

|  |  |
|---|---|
| **API Call** | `curl -X POST -H "Authorization: hbapi:123456:9876abcd54321:nym2" -d @json/1002_users.json "https://streaming-data.appnexus.com/rt-segment"` |

|  |  |
|---|---|
| **JSON Payload** | `{ "rt_segment": [ { "user_id": "12345678900987654321", "seg_block": [ { "seg_id": 10001, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null }, { "seg_id": 10002, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null } ], "domain": "domain" }, #... assume there are additional 1000 users in this array (1002 in total) ] }` |

|  |  |
|---|---|
| **Response** | `{ "response": { "status": "OK", "message": { "users_in_request": 1000, "segments_in_request": 2000 }, "warnings": [ { "message": "Too many user_ids in request.", "entity": { "user_id": "23456789009876543211", "seg_block": [ { "seg_id": 10001, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null }, { "seg_id": 10002, "seg_code": null, "value": 1, "expiration": 1440, "member_id": null } ] } }, #... similar error will be sent for each user over 1000 ] } }` |

## seg_id or  seg_code and  member_id are not provided

|  |  |
|---|---|
| **JSON Payload** | `{ "rt_segment": [ { "user_id": "1", "seg_block": [ { "seg_id": null, "seg_code": "abc", "value": 1, "expiration": 1, "member_id": null } ] } ] }` |

|  |  |
|---|---|
| **Response** | `{ "status": "OK", "message": { "users_in_request": 0, "segments_in_request": 0 }, "warnings": [ { "message": "'seg_id' or 'seg_code' and 'member_id' are required", "entity": { "seg_code": "abc", "value": 1, "expiration": 1 } }, { "message": "No valid segments for user_id: 1.", "entity": { "user_id": "1", "seg_block": [ { "seg_code": "abc", "value": 1, "expiration": 1 } ] } }, { "message": "No valid rt_segment in request.", "entity": { "rt_segment": [ { "user_id": "1", "seg_block": [ { "seg_code": "abc", "value": 1, "expiration": 1 } ] } ] } } ] }` |

### `seg_block` not provided

|  |  |
|--|--|
| **JSON Payload** |`{ "rt_segment": [{"user_id": "asdf"}], "domain": "domain"}` |

|  |  |
|---|---|
| **Response** | `{ "status": "OK", "message": { "users_in_request": 0, "segments_in_request": 0 }, "warnings": [ { "message": "'seg_block' is required", "entity": { "user_id": "asdf" } }, { "message": "No valid rt_segment in request.", "entity": { "rt_segment": [ { "user_id": "asdf" } ] } } ] }` |

### `user_id` empty

|  |  |
|---|---|
| **JSON Payload** | `{ "rt_segment": [ { "seg_block": [ { "seg_id": 1, "seg_code": null, "value": 1, "expiration": 1, "member_id": null } ] } ], "domain": "domain" }` |

|  |  |
|---|---|
| **Response** | `{ "status": "OK", "message": { "users_in_request": 0, "segments_in_request": 0 }, "warnings": [ { "message": "'user_id' is required and cannot be empty", "entity": { "seg_block": [ { "seg_id": 1, "seg_code": null, "value": 1, "expiration": 1 } ] } }, { "message": "No valid rt_segment in request.", "entity": { "rt_segment": [ { "seg_block": [ { "seg_id": 1, "seg_code": null, "value": 1, "expiration": 1 } ] } ] } } ] }` |

## Related topics

- [Streaming Server-Side Segmentation](streaming-server-side-segmentation.md)
- [Check usage statistics](check-usage-statistics.md)