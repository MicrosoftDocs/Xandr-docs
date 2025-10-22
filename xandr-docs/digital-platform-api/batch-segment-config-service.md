---
title: Batch Segment Config Service
description: In this article, find information on the Batch Segment Config service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Batch Segment Config service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.
> [!WARNING]
> If you need to make any changes to the `num_line` or `byte` limits of a member's batch segment configuration, please file a ticket under EPIC: DMP-376, following the directions in the info section of the page. You will need to receive approval from Ewa Maciukiewicz in order to proceed with the changes.

The Batch Segment Config Service is an internal, admin-only API used to add and modify per-client settings related to their use of the [Batch Segment Service](batch-segment-service.md). You can configure the client's preferred file format as well as the strictness of our error checking against that format. You can also set usage limits and define which other members' segment data the client has access to.

> [!NOTE]
> For more information about the specifics of the file format, see [Initial BSS Account Setup](../bidders/initial-bss-account-setup.md).

## Client access to other members' data

A client who wants access to another member's data will have to ask that member to file a support request via our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com). For example, if client A wants access to client B's data, client B must send in a support request authorizing client A's access.

## JSON fields

| Field | Type | Description |
|---|---|---|
| `created_on` | string | The time at which this object was created. <br><br> **Filter by**: Yes <br> **Sort by**: Yes |
| `daily_byte_limit` | int | The maximum number of bytes per day the client may upload. General guide: 10G (roughly 280M lines gzipped with verbose format) <br><br>  **Note**: Clients who want to raise this should confirm that they are using their data limits properly, i.e. they are sending us a diff file instead of a complete database dump every day. Clients who do not use data smartly must refactor their upload process to minimize data send. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `daily_num_lines_limit` | int | The maximum number of lines per day the client may upload. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `default_domain` | string | The internal database domain to add the user ID to. The default is set to 'userdata'. Usually not used, since almost all clients are in one domain at this time. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `default_expiration` | int | The amount of time, in minutes, after which this client would like their segments to expire. This is overridden by any expiration settings in the segment data file. A value of `0` denotes that the segment should never expire; `-1` denotes that this user will be removed from this segment. <br><br> **Note**: If for whatever reason, `POST` requests are rejecting 0 as a valid input, `POST` with a non-zero value and then `PUT` the same file again with 0 as the value and it should work. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `external_member_uid` | int | If "`use_external_uids`" is `true`, then indicate the member ID whose user IDs the client will be using. A value of `null` means to use the client's own `member_id`. Only valid for members using mapUID usersyncing (HINT: Very few clients use this). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `hourly_byte_limit` | int | The maximum number of bytes per hour the client may upload. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `hourly_num_lines_limit` | int | The maximum number of lines per hour the client may upload. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `id` | int | The unique identifier of this object. <br><br> **Filter by**: Yes <br> **Sort by**: Yes |
| `last_modified` | string | The time at which this object was last modified. <br><br> **Filter by**: Yes <br> **Sort by**: Yes |
| `max_concurrent_uploads` | int | The maximum number of uploads the client may perform at once. General guide: 1 <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `member_id` | int | The member ID of the client whose configuration you're editing. <br><br> **Required On**: `PUT`, `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `member_segment_access` | array of objects | The member IDs whose segments the client has access to. (Use this if you're adding users to segments on behalf of someone). For more information, see the [Member Segment Access Array](#member-segment-access-array) section below. <br><br> **Required On**: `POST` <br> **Filter by**: No <br> **Sort by**: No |
| `num_error_log_lines` | int | The number of lines that will show in the error log. General guide: less than 200 <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `num_invalid_before_error` | int | The number of invalid lines to accept before signalling an error. When this limit is reached, the job is killed, but everything added before the first error will go in. General guide: 50% of a client's file. When in doubt, set this very high. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `segment_fields` | array | A list of segments correlated to the `SEG` block of the file format. For more information, see [Batch Segment Service](batch-segment-service.md). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `separator_1` | string | A character or string of characters used as a separator by the [Batch Segment Service](batch-segment-service.md). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `separator_2` | string | A character or string of characters used as a separator by the [Batch Segment Service](batch-segment-service.md). |
| `separator_3` | string | A character or string of characters used as a separator by the [Batch Segment Service](batch-segment-service.md). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `separator_4` | string | A character or string of characters used as a separator by the [Batch Segment Service](batch-segment-service.md). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `separator_5` | string | A character or string of characters used as a separator by the [Batch Segment Service](batch-segment-service.md). <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `use_external_uids` | bool | Whether the client would like to use external user IDs for mapping from one name to another. Set this field to `true` in order to use an `external_member_uid`. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |
| `use_specific_geo` | string | Set to `NULL` by default. <br><br> This field is no longer needed to do improvements made to Batch Segment in 2013. The system will check all geos. If the user is in multiple geos, they will be added to the appropriate segments in each geo they exist in. <br><br> **Required On**: `POST` <br> **Filter by**: Yes <br> **Sort by**: Yes |

### Member segment access array

| Field | Type | Description |
|---|---|---|
| `segment_owner_member_id` | int | The member ID of the segment owner. <br><br> **Filter by**: No <br> **Sort by**: No |

## Examples

### See the configuration for a given member

```
$ curl -b cookies "https://api.appnexus.com/batch-segment-config?member_id=1226"
{
  "response": {
    "status": "OK",
    "count": null,
    "start_element": 0,
    "num_elements": 100,
    "batch_segment_upload_config": {
      "member_id": 1226,
      "id": 2,
      "hourly_byte_limit": 3500000000,
      "daily_byte_limit": 3500000000,
      "max_concurrent_uploads": 1,
      "num_error_log_lines": 50,
      "num_invalid_before_error": 1000000000,
      "separator_1": ";",
      "separator_2": ",",
      "separator_3": ":",
      "separator_4": "\t",
      "separator_5": "^",
      "default_domain": "userdata",
      "use_specific_geo": null,
      "segment_fields": "[SEG_ID,EXPIRATION,VALUE]",
      "last_modified": "2012-06-01 15:10:20",
      "created_on": "0000-00-00 00:00:00",
      "default_expiration": 0,
      "use_external_uids": false,
      "external_member_uid": null,
      "member_segment_access": [
        {
          "segment_owner_member_id": 23
        }
      ]
    }
  }
  }
```
