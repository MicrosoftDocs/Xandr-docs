---
title: Member Data Sharing Service
description: In this article, learn about Member Data Sharing Service, their JSON fields, and REST API with a detailed set of examples.
ms.custom: data-providers
ms.date: 10/28/2023
---

# Member data sharing service

The Member Data Sharing Service allows you to share your segments with other platform members. Here's how it works:

1. You ask the buyer to enable you (the data provider) in Microsoft Invest. The setting they must use to do this is located in the Microsoft Invest **Segment Manager**, under **Manage Data Providers**.
1. You create a sharing record for a member that you want to share segments with.
1. In the sharing record, you specify whether you want to share all of your segments or a specific list of segments.
1. The member that you've shared your segments with can then target your segments in campaigns (or in the case of bidders, they will be sent the segment data with each bid request).

> [!NOTE]
> When you remove a segment from a sharing record, the member cannot add the segment to the targeting profile of any new or existing campaign. If the member is already targeting the segment in an existing campaign, however, the campaign will continue to target the segment until the member manually removes it from the campaign's targeting profile. Once the segment has been removed, the member will not be able to add it to the campaign's targeting profile again.
>
> - Advertiser-level segments cannot be shared. Only member/network-level segments can be shared. To move segments from the advertiser to network level, you may set `advertiser_id` to `NULL` via the [Segment Service](../digital-platform-api/segment-service.md).
> - You can not share segments with buyer members who belong to externally integrated DSPs.
> - The Member Data Sharing service now works on BOTH Xandr's API (api.appnexus.com) as well as the impression bus API (api.adnxs.com). Although only api.adnxs.com is used below, it may be replaced with api.appnexus.com for those clients who have access to Xandr's API. Only members who are on Xandr will have access to the API. The majority of data providers can only access the impression bus API.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.adnxs.com/member-data-sharing` | View all of your existing sharing records. |
| `GET` | `https://api.adnxs.com/member-data-sharing?id=RECORD_ID` | View a specific sharing record. |
| `GET` | `https://api.adnxs.com/member-data-sharing?data_member_id=MEMBER_ID&buyer_member_id=CLIENT_MEMBER_ID`<br>where `data_member_id` = your member ID, and `buyer_member_id` = the recipient's member ID | Retrieve the sharing record ID using member ID's. |
| `POST` | `https://api.adnxs.com/member-data-sharing?data_member_id=MEMBER_ID` <br>(sharing JSON)<br><br>**Note:** The member-data-sharing object cannot be an array if singular. | Create one sharing record to share segments with one member. |
| `POST` | `https://api.adnxs.com/member-data-sharings?data_member_id=MEMBER_ID`<br>(sharing JSON)<br><br>**Note:** The member-data-sharings (plural) object must be an array if plural. | Create multiple sharing records to share segments with multiple members. |
| `PUT` | `https://api.adnxs.com/member-data-sharing?id=RECORD_ID`<br><br>**Note:**<br> - This method removes all existing segments, replacing the segments with only the newly specified list.<br> - To remove one or more segments from a list, you must replace the entire list with your intended segments. | Replace the list of segments shared within a sharing record. |
| `PUT` | `https://api.adnxs.com/member-data-sharing?id=RECORD_ID&append=true`<br><br>**Note:** Segments can only be added to the list using the "append" flag, and not deleted. | Appending segments from shared segment list within a sharing record. |
| `DELETE` | `https://api.adnxs.com/member-data-sharing?id=RECORD_ID` | Delete a sharing record. |

> [!TIP]
> JSON Structure:
>
> When adding or updating a single sharing record, you should structure the JSON as a single object called `"member_data_sharing"`. When adding `POST` multiple sharing records, you should structure the JSON as an array of objects called `"member_data_sharings"` (note the plural) and place the sharing data in an array. You cannot update (`PUT`) multiple sharing records at the same time. For exact formatting, see the [examples](#examples) below.

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the sharing record.<br>**Default:** Auto-generated number<br>**Required On:** `PUT`/`DELETE`, in query string |
| `data_member_id` | int | **Read-only.** Your member ID. |
| `buyer_member_id` | int | The ID of the member with whom you are sharing segments.<br>**Required On:** `POST` |
| `segment_exposure` | enum | Whether you share all of your segments or a list of specific segments with the member. Possible values: `"all"` or `"list"`.  If you choose `"all"`, any newly created segments will automatically be shared with the buyer member. If you create custom segments that should only be accessible to certain buyers, you should use `"list"` exposure.<br>**Required On:** `POST`<br><br>**Note:** Data Providers in Data Market Place should not create sharing records by choosing `segment_exposure` value as `"all"`. If there is any such record exists, update the value to `"list"` and include the appropriate segment list.|
| `segments` | array of objects | If `segment_exposure` is `"list"`, the list of segments that you are sharing with the member. See the first example below for formatting.<br>**Required On:** `POST`/`PUT`, if `segment_exposure` is `"list"`. |

## Examples

### Share segments with members 103 and 104

```
$ cat data_share_multiple
{
    "member_data_sharings": [
        {
            "buyer_member_id": 103,
            "segment_exposure": "all"
        },
        {
            "buyer_member_id": 104,
            "segment_exposure": "list",
            "segments": [
                {
                    "id": 121175
                },
                {
                    "id": 121176
                },
                {
                    "id": 121177
                },
                {
                    "id": 121178
                }
            ]
        }
    ]
}
$ curl -b cookies -c cookies -X POST -d @data_share_multiple 'https://api.adnxs.com/member-data-sharing?data_member_id=1432'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": null,
        "num_elements": null,
        "id": [
            54,
            55
        ],
        "member_data_sharings": {
            "54": {
                "id": 54,
                "data_member_id": 1432,
                "buyer_member_id": 103,
                "segment_exposure": "all",
                "segments": null
            },
            "55": {
                "id": 55,
                "data_member_id": 1432,
                "buyer_member_id": 104,
                "segment_exposure": "list",
                "segments": [
                    {
                        "id": 121175,
                        "name": "Segment share 1"
                    },
                    {
                        "id": 121176,
                        "name": "Segment share 2"
                    },
                    {
                        "id": 121177,
                        "name": "Segment share 3"
                    },
                    {
                        "id": 121178,
                        "name": "Segment share 4"
                    }
                ]
            }
        },
        "dbg": {
        ...
        }
    }
}
```

### Share segments with member 105

```
$ cat data_share_single
{
    "member_data_sharing": {
        "buyer_member_id": 105,
        "segment_exposure": "all"
    }
}
$ curl -b cookies -c cookies -X POST -d @data_share_single 'https://api.adnxs.com/member-data-sharing?data_member_id=1432'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "id": "56",
        "member_data_sharing": {
            "id": 56,
            "data_member_id": 1432,
            "buyer_member_id": 105,
            "segment_exposure": "all",
            "segments": null
        },
        "dbg": {
            ...
        }
    }
    }
```

### Update the sharing record for member 104

In this example, the `PUT` request adds segment 121179 to sharing record 55 (the sharing record for member 104).

```
$ cat data_share_update
{
    "member_data_sharing": {
        "segments": [
            {
                "id": 121175
            },
            {
                "id": 121176
            },
            {
                "id": 121177
            },
            {
                "id": 121178
            },
            {
                "id": 121179
            }
        ]
    }
}
$ curl -b cookies -c cookies -X PUT -d @data_share_update 'https://api.adnxs.com/member-data-sharing?id=55'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "id": 55,
        "member_data_sharing": {
            "id": 55,
            "data_member_id": 1432,
            "buyer_member_id": 104,
            "segment_exposure": "list",
            "segments": [
                {
                    "id": 121175,
                    "name": "test for sharing"
                },
                {
                    "id": 121176,
                    "name": "test for sharing2"
                },
                {
                    "id": 121177,
                    "name": "test for sharing3"
                },
                {
                    "id": 121178,
                    "name": "test for sharing4"
                },
                {
                    "id": 121179,
                    "name": "test for sharing4"
                }
            ]
        },
        "dbg": {
            ...
        }
    }
}       
```

### View all of your sharing records

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/member-data-sharing'
{
    "response": {
        "status": "OK",
        "count": 5,
        "start_element": null,
        "num_elements": null,
        "member_data_sharings": [
            {
                "id": 46,
                "data_member_id": 1432,
                "buyer_member_id": 100,
                "segment_exposure": "all",
                "segments": null
            },
            {
                "id": 52,
                "data_member_id": 1432,
                "buyer_member_id": 101,
                "segment_exposure": "all",
                "segments": null
            },
            {
                "id": 53,
                "data_member_id": 1432,
                "buyer_member_id": 102,
                "segment_exposure": "all",
                "segments": null
            },
            {
                "id": 54,
                "data_member_id": 1432,
                "buyer_member_id": 103,
                "segment_exposure": "all",
                "segments": null
            },
            {
                "id": 55,
                "data_member_id": 1432,
                "buyer_member_id": 104,
                "segment_exposure": "list",
                "segments": [
                    {
                        "id": 121175,
                        "name": "Segment share 1"
                    },
                    {
                        "id": 121176,
                        "name": "Segment share 2"
                    },
                    {
                        "id": 121177,
                        "name": "Segment share 3"
                    },
                    {
                        "id": 121178,
                        "name": "Segment share 4"
                    },
                    {
                        "id": 121179,
                        "name": "Segment share 5"
                    }
                ]
            },
            {
                "id": 56,
                "data_member_id": 1432,
                "buyer_member_id": 105,
                "segment_exposure": "all",
                "segments": null
            }
        ],
        "dbg": {
            ...
        }
    }
}    
```

### View sharing record 55

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/member-data-sharing?id=55'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null,
        "member_data_sharing": {
            "id": 55,
            "data_member_id": 1432,
            "buyer_member_id": 104,
            "segment_exposure": "list",
            "segments": [
                {
                    "id": 121175,
                    "name": "Segment share 1"
                },
                {
                    "id": 121176,
                    "name": "Segment share 2"
                },
                {
                    "id": 121177,
                    "name": "Segment share 3"
                },
                {
                    "id": 121178,
                    "name": "Segment share 4"
                },
                {
                    "id": 121179,
                    "name": "Segment share 5"
                }
            ]
        },
        "dbg": {
            ...
        }
    }
}  
```
