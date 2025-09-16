---
title: Segment Service
description: Use the Segment service to create segment IDs for inventory page placement and store them in the server-side cookie store.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Segment service

The Segment Service lets you create segment IDs, which are then used to create segment pixels for placement on inventory pages. If you are working with third-party data providers through the Xandr platform, it will show you a list of segments for those providers.

- Segments are associated with members and can optionally be associated with a particular advertiser.
- All segment data will be stored in the server-side cookie store and passed to the bidder associated with the owning member on every bid request.
- An advertiser association is for reference and use in our Console user interface.

> [!NOTE]
> The shared `"birthday cookie"` segment has an ID of `1` and is available to all platform members.
> [!TIP]
> Once you have a segment ID, the basic format of a segment pixel is `<img src="media/seg?add=123" width="1" height="1"/>`, where `123`
> is the segment ID. For more information about segment pixels, see [Working with Segments](../invest/working-with-segments.md) in the UI documentation.
> [!NOTE]
> Be sure to wait approximately 20 minutes before trying to add users to any newly created segments to allow these segments to be propagated to all servers. As a best practice, try to minimize the creation of new segments, re-uses existing segments where possible or use segment `"values"` to further sub-divide users within existing segments. These practices will ensure successful user uploads to segments.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/segment?member_id=MEMBER_ID`<br><br>`https://api.appnexus.com/segment` <br>(segment JSON) | Add a new segment. |
| `POST` | `https://api.appnexus.com/segment?advertiser_id=ADVERTISER_ID`<br><br>`https://api.appnexus.com/segment?advertiser_code=ADVERTISER_CODE`<br>(segment JSON) | Add a new advertiser segment. |
| `PUT` | `https://api.appnexus.com/segment?id=SEGMENT_ID`<br><br>`https://api.appnexus.com/segment?code=SEGMENT_CODE`<br>(segment JSON) | Modify an existing segment. |
| `PUT` | `https://api.appnexus.com/segment?id=SEGMENT_ID&advertiser_id=ADVERTISER_ID`<br><br>`https://api.appnexus.com/segment?code=SEGMENT_CODE&advertiser_code=ADVERTISER_CODE`<br>(segment JSON) <br><br>**Tip**: To change a segment from advertiser-owned to network-owned. Make a `PUT` call, passing the segment ID and member ID ithe query string and setting `advertiser_id` to `null` in the JSON file. See [Examples](#examples) for more information. | Modify an existing advertiser segment. |
| `GET` | `https://api.appnexus.com/segment` | View all segments. |
| `GET` | `https://api.appnexus.com/segment?id=1,2,3` | View multiple segments by ID using a comma-separated list. |
| `GET` | `https://api.appnexus.com/segment?id=SEGMENT_ID`<br><br>`https://api.appnexus.com/segment?code=SEGMENT_CODE` | View a particular segment. |
| `GET` | `https://api.appnexus.com/segment?include_shared=0` | View non-shared first party segments. |
| `GET` | `https://api.appnexus.com/segment?search=SEARCH_TERM` | Search for segments with IDs, short names, or codes containing certain characters. |
| `DELETE` | `https://api.appnexus.com/segment?id=SEGMENT_ID` | Delete an existing segment. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `code`  | string(50) | The user-defined code for calling the segment.<br><br>**Note**: The value of the `code` field is not case-sensitive (e.g., `"Test"` is the same as `"test"`), so each code must be unique regardless of case. However, when referring to the code in query string targeting, case-sensitivity matters (e.g., if the value of the `code` field is `"Test"`, the parameter in a query string referring to it must also be `"Test"`). |
| `id`  | int | The Xandr ID assigned by the API to reference the segment. When switching a segment from advertiser-owned to network-owned, you must pass this information in the query-string.<br><br>**Required On**: `PUT`, in query-string |
| `state` | enum | The state of the segment. This determines whether the segment can be used. Possible values: `active` or `inactive`.<br><br>**Default**: `active` |
| `short_name` | string(255) | The short name used to describe the segment. |
| `description` | string | The optional description for this segment. Maximum 500 characters. Restricted characters: `'` `\` |
| `member_id` | int | The ID of the member that owns this segment.<br><br>**Note**: When switching a segment from advertiser-owned to network-owned, you must pass this information in the query string. See [Examples](#examples) for more details. |
| `category` | string | **Deprecated**. This field is read-only. |
| `expire_minutes` | int | The number of minutes the user is kept in the segment. Segments with no expiration time will be expired from the Xandr server-side data store within 90 days. If you want to add the user to the segment only for the duration of the ad call, set to `0`. Changing this value does not retroactively affect users already in the segment. Also, if a user is re-added, the expiration window resets.<br><br>**Note**: To keep users in the segment for the 180-day maximum, set this to `null`. |
| `enable_rm_piggyback` | boolean | If `true`, piggybacking RM pixels is enabled. |
| `max_usersync_pixels` | int | The maximum number of third-party user sync pixels to piggyback onto the segment pixel. Set to `0` to block all third-party user sync pixels. If blank (`null`), the segment defaults to `0`.<br><br>**Note**: Invalid, if `querystring_mapping_key_value` object is also included.<br><br>**Default**: `0` |
| `last_modified` | timestamp | The date and time when the segment was last modified. |
| `provider_id` | int | The ID of the data provider that owns the segment. It is read-only and can be used for filtering segments.<br><br>**Default**: `null` |
| `advertiser_id` | int | The ID of the advertiser using the segment if the segment should be on the Advertiser level rather than the Network level. If `null`, the segment will be usable by all advertisers for that member. This information is for reference in Console.<br><br>**Default**: `null` |
| `piggyback_pixels` | array | The URLs of the pixels you want us to fire when the segment pixel fires. See [Piggyback Pixels](#piggyback-pixels) below for more details. |
| `price` | double | **Deprecated**. This field is currently not operational.<br><br>**Default**: `0` |
| `parent_segment_id` | int | The ID of the parent segment. If the parent segment is targeted in a [profile](./profile-service.md), the direct child segments are targeted as well.<br><br>**Note**: <br> - The `parent_segment_id` field will be deprecated on January 1, 2019.<br> - The parent-child logic extends only one level deep. Example: Segment A is the parent of segment B and segment C, and segment C is the parent of segment D. When segment A is targeted, segment B and segment C are targeted as well, but segment D is not. |
| `querystring_mapping` | object | A query string that allows you to assign a set of parameters and values to a segment. See [About Query Strings](#about-query-strings) for a general description of query strings and [Query String Mapping](#query-string-mapping) for more details. |
| `querystring_mapping_key_value` | object | A query string that allows you to reuse a key and assign a single key-value pair to a segment. See [About Query Strings](#about-query-strings) for a general description of query strings and [Query String Mapping Key Value](#query-string-mapping-key-value) for more details. <br><br>**Note**: <br> - Invalid, if a `querystring_mapping` object is also included.<br> - The value of the `querystring_mapping_key_value` field is case-insensitive when it is looked up in an auction. |
| `object_type` | string | An optional field for customers to indicate that a segment onboarded by a DMP, or through another of their members, is a first-party segment to them. Segments with `object_type = ‘default’` can be updated to `object_type = ‘first-party’`. This makes a shared segment eligible to be used with Modeled Audiences.<br> **NOTE**: - By setting the `object_type to 'first_party'`, you are attesting that your company or a direct client of your company has collected this segment data directly from an individual, or alternatively, your company has licensed this data from a party that collected such data directly from an individual and the terms of your license allow for such data to be used for this look-alike modeling purpose. <br> - Shared segments with `object_type = ‘universal_pixel’` are automatically eligible for Modeled Audiences. <br> - To be eligible for Modeled Audiences, segments must also be composed of Xandr user IDs or MAIDs. Segments targeting URLs or IPs are currently not supported. |

### Piggyback pixels

When adding piggyback pixels, please keep the following in mind:

- Image pixels can only piggyback off other image pixels, and JavaScript pixels can only piggyback other JavaScript pixels.
- Image pixels can only have one piggyback pixel. If you need to piggyback multiple pixels, be sure to use a JavaScript pixel.
- There are no character limits to piggybacked pixels in Xandr, but browser/server URL limits may apply.

Each object in the `piggyback_pixels` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | The URL of the pixel to piggyback. |
| `pixel_type` | enum | The type of pixel to piggyback. Possible values: `"js"` or `"img"`. |

### About query strings

Xandr provides two methods of query string mapping to allow publishers to pass inventory-specific or user-specific information in the query strings of their placement tags:

- **query string mapping** - in which a set of parameter values assigned to the segment.
- **query string mapping key value** - which allows you to assign one key/value pair to a segment and then reuse the same key with a different value in another segment.

For both types of mapped query strings:

- Whenever an ad call is made with a mapped query string, the associated user will automatically be added to the segment.
- You can target the query string in a campaign (via the `segment_targets` or `segment_group_targets` fields of the [Profile Service](./profile-service.md)).

Note that you can choose how long the user will be kept in the segment. If you want to keep the user in the segment for retargeting purposes, set `expire_minutes` to the correct number of minutes (`null` will set to system maximum value 180 days). If you want to add the user to the segment only for the duration of the ad call, set `expire_minutes` to `0`.

See [Examples](#examples) below for various scenarios and formatting.

### Query string mapping

Query string mapping allows you to assign a parameter to a segment using the `querystring_mapping` field. Multiple values can be added to a parameter. This method is useful in cases where only one value makes sense for a user. For example, a user's age, salary range, or experience. If a user is in `beginner` segment but later gains more experience, the user can be moved to the `advanced` segment and is automatically removed from the `beginner` segment. See [Examples](#examples) for more details.

In this type of query string, the parameter can be provided with no values. For example, `{"param": "car_model", "value_type": "none"}`. This allows any value for that parameter to be provided.

| Field | Type | Description |
|:---|:---|:---|
| `param` | string | The query string parameter. |
| `value_type` | enum | The type of value accompanying the parameter. Possible values: `"text"`, `"numeric"`, or `"none"`. |
| `values` | array | The strings that can accompany the parameter when value_type is `"text"`. If `value_type` is `"numeric"` or `"none"`, this field cannot be used.<br><br>**Tip**: <br>**Need the Value IDs?**<br>If you need the IDs of the values, pass the query string parameters `show_querystring_ids=true`, and values will instead be an array of objects with the keys `"value"` (string) and `"id"` (int). |
| `allow_empty_text` | Boolean | When `true`, the values array may be `null`. May only be used when the `value_type` is `"text"`.<br><br>**Default**: `false` |
| `publishers` | array | The publishers from which you expect the query string. Users associated with these publishers' placements will be added to the segment. |
| `sites` | array | The placement groups (sites) from which you expect the query string. Users associated with these placements will be added to the segment. <br><br>**Note**: This field overrides publishers. If you specify a site that doesn't belong to one of the specified publishers, users associated with the placements in a placement group will nonetheless be added to the segment. |
| `placements` | array | The placements in which you expect the query string. Users associated with these placements will be added to the segment. <br><br>**Note**: This field overrides placement groups and publishers. That is, if you specify a placement that doesn't belong to one of the specified placement groups or publishers, users associated with the placement will still be added to the segment. |
| `include_shared` | Boolean | Set this value to `false` to avoid retrieving shared segments. |

### Query string mapping key value

Query string key/value mapping allows you to assign a single key-value pair to a segment using the `querystring_mapping_key_value` object. This type of query string allows a user to exist in multiple segments and is useful in cases where more than one value for a parameter makes sense. For example, a user's musical preferences. If a user is in `rock` segment but also likes `funk`, he or she can exist in both segments simultaneously. See [Examples](#examples) for more details.

In this type of query string, each `qs_key` must have at least one corresponding `qs_value`.

| Field | Type | Description |
|:---|:---|:---|
| `qs_key` | string | The query string parameter. |
| `qs_value` | string | A value for the query string key. The value can be empty or `null`. Multiple values can be added using the same key. A `qs_value` must be provided if a `qs_key` is used. |

## Examples

### Create a segment

```
$ cat segment

{
    "segment":{
        "member_id":25,
        "short_name":"remarketing - Warner Media user",
        "code":"WM08"
    }
}

$ curl -b cookies -c cookies -X POST -d @segment 'https://api.appnexus.com/segment?member_id=25'
                                            Or
$ curl -b cookies -c cookies -X POST -d @segment 'https://api.appnexus.com/segment'

{
   "response" : {
      "id" : 102,
      "count" : 1,
      "dbg_info" : {
         ...
      },
      "start_element" : 0,
      "num_elements" : 100,
      "segment" : {
         "object_type" : "default",
         "advertiser_id" : null,
         "enable_rm_piggyback" : true,
         "querystring_mapping_key_value" : null,
         "member_id" : 25,
         "expire_minutes" : null,
         "category" : null,
         "provider" : null,
         "parent_segment_id" : null,
         "querystring_mapping" : null,
         "short_name" : "yuichi-test",
         "max_usersync_pixels" : null,
         "code" : "yuichi-test-seg-02",
         "state" : "active",
         "description" : null,
         "id" : 102,
         "piggyback_pixels" : null,
         "last_modified" : "2019-08-14 17:26:29"
      },
      "status" : "OK"
   }
}
```

### View a segment

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/segment?id=11836'

{
    "response": {
        "status": "OK",
        "segments": [
            {
                "id": 11836,
                "code": null,
                "state": "active",
                "short_name": "March 10",
                "description": null,
                "member_id": 185,
                "category": null,
                "price": "0",
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": 0,
                "last_modified": "2010-03-10 23:23:48",
                "provider": null,
                "parent_segment_id": null,
                "advertiser_id": 51,
                "piggyback_pixels": null
            }
        ]
    }
}
```

### View non-shared first party segments

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/segment?include_shared=0'

{
    "response": {
        "status": "OK",
        "segments": [
            {
                "id": 11836,
                "code": null,
                "state": "active",
                "short_name": "March 10",
                "description": null,
                "member_id": 185,
                "category": null,
                "price": "0",
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": 0,
                "last_modified": "2010-03-10 23:23:48",
                "provider": null,
                "parent_segment_id": null,
                "advertiser_id": 51,
                "piggyback_pixels": null
            }
        ]
    }
}
```

### Change a segment from advertiser-owned to network-owned

To change an advertiser-level segment into a network-level segment, you make a `PUT` call passing the segment ID and member ID in the query string and setting `advertiser_id` to `null` in the JSON file.

```
$ cat segment_update

{
    "segment": {
        "advertiser_id": null
    }
}

$ curl -b cookies -c cookies -X PUT -d @segment_update 'https://api.appnexus.com/segment?id=175196&member_id=1066'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "175196",
        "start_element": 0,
        "num_elements": 100,
        "segment": {
            "id": 175196,
            "code": null,
            "state": "active",
            "short_name": "Users who have purchased software",
            "description": null,
            "member_id": 1066,
            "category": null,
            "price": 0,
            "expire_minutes": null,
            "enable_rm_piggyback": true,
            "max_usersync_pixels": null,
            "advertiser_id": null,
            "last_modified": "2013-10-18 20:34:27",
            "provider": null,
            "parent_segment_id": null,
            "piggyback_pixels": null,
            "querystring_mapping": null
        }
    }
}
```

### Add text query string mapping to a segment

**Scenario**: Publisher `6` tells you to expect one of the following values in the query string of placement 596411: "`experience_level=beginner`", "`experience_level=intermediate`", or "`experience_level=advanced`". When this placement comes in with the "`experience_level`" parameter, you want to add the associated user to segment `25` with the ability to distinguish between the values of beginner, intermediate, and advanced in campaign targeting. In this case, you would create the following JSON and make a `PUT` call to update the segment.

```
$ cat segment_update

 {
    "segments": [
        {
            "id": 25,
            "member_id": 20,
            "querystring_mapping": {
                "param": "experience_level",
                "value_type": "text",
                "values": [
                    "beginner",
                    "intermediate",
                    "advanced"
                ],
                "publishers": [
                    {
                        "id": 6
                    }
                ],
                "placements": [
                    {
                        "id": 596411
                    }
                ]
            }
        }
    ]
}

 $ curl -b cookies -c cookies -X PUT -d @segment_update 'https://api.appnexus.com/segment?id=25'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "25",
        "start_element": null,
        "num_elements": null,
        "segment": {
            "id": 25,
            "code": null,
            "state": "active",
            "short_name": "test",
            "description": null,
            "member_id": 49,
            "category": null,
            "price": 23,
            "expire_minutes": 20,
            "enable_rm_piggyback": true,
            "max_usersync_pixels": null,
            "last_modified": "2012-01-24 20:15:18",
            "provider": null,
            "parent_segment_id": null,
            "advertiser_id": null,
            "piggyback_pixels": null,
            "querystring_mapping": {
                "param": "experience_level",
                "value_type": "text",
                "values": [
                    "beginner",
                    "intermediate",
                    "advanced"
                ],
                "publishers": [
                    {
                        "id": 6,
                        "name": "Publisher 6"
                    }
                ],
                "sites": null,
                "placements": [
                    {
                        "id": 596411,
                        "name": "Placement 596411"
                    }
                ]
            }
        }
    }
}
```

### Add numeric query string mapping to a segment

**Scenario**: Auto publisher `30` tells you to expect the "`car_year`" parameter followed by a year in the query strings of its placements. When a placement from this publisher comes in with `"car_year=YYYY"` in its query string, you can add the associated user to segment `26`. In this case, you would create the following JSON and make a `PUT` call to update the segment.

```
$ cat segment_update

{
   "segment": {
      "member_id": 20,
      "querystring_mapping": {
         "param": "car_year",
         "value_type": "numeric",
         "publishers": [
            {
               "id": 30
            }
         ]
      }
   }
}

$ curl -b cookies -c cookies -X PUT -d @segment 'https://api.appnexus.com/segment?id=26'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "26",
        "start_element": null,
        "num_elements": null,
        "segment": {
            "id": 26,
            "code": null,
            "state": "active",
            "short_name": "test",
            "description": null,
            "member_id": 20,
            "category": null,
            "price": 23,
            "expire_minutes": 20,
            "enable_rm_piggyback": true,
            "max_usersync_pixels": null,
            "last_modified": "2012-01-24 20:15:18",
            "provider": null,
            "parent_segment_id": null,
            "advertiser_id": null,
            "piggyback_pixels": null,
            "querystring_mapping": {
                "param": "car_year",
                "value_type": "numeric",
                "values": null,
                "publishers": [
                    {
                        "id": 30,
                        "name": "Publisher 30"
                    }
                ],
                "sites": null,
                "placements": null
            }
        }
    }
}
```

### Add query string mapping without values to a segment

**Scenario**: Both publishers `10` and `30` tell you to expect the parameter "`car_model`" (without values) in their placements. When a placement from either of these publishers comes in with "`car_model`" in its query string, you can add the associated user to segment `2`. In this case, you would create the following JSON and make a `PUT` call to update the segment.

```
$ cat segment_update

{
   "segment": {
      "member_id": 20,
      "querystring_mapping": {
         "param": "car_model",
         "value_type": "none",
         "publishers": [
            {
               "id": 10,
               "id": 30
            }
         ]
      }
   }
}

$ curl -b cookies -c cookies -X PUT -d @segment_update 'https://api.appnexus.com/segment?id=2'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "2",
        "start_element": null,
        "num_elements": null,
        "segment": {
            "id": 2,
            "code": null,
            "state": "active",
            "short_name": "test",
            "description": null,
            "member_id": 20,
            "category": null,
            "price": 23,
            "expire_minutes": 20,
            "enable_rm_piggyback": true,
            "max_usersync_pixels": null,
            "last_modified": "2012-01-24 20:15:18",
            "provider": null,
            "parent_segment_id": null,
            "advertiser_id": null,
            "piggyback_pixels": null,
            "querystring_mapping": {
                "param": "car_model",
                "value_type": "none",
                "values": null,
                "publishers": [
                    {
                        "id": 10,
                        "name": "Publisher 10"
                    },
                    {
                        "id": 30
                        "name": "Publisher 30"
                    }
                ],
                "sites": null,
                "placements": null
            }
        }
    }
}
```

### Use query string key-value mapping to reuse a key with multiple values

**Scenario**: Publishers want to add users to segments based on their musical preferences. You want to use the same key, "`music_genre`" and offer multiple values: "`rock`", "`pop`", "`hard rock`", and "`funk`", assigning them to different segments and allow users to be placed in one or more of the segments. This reflects the fact that users may have diverse musical choices.

In this case, you would create the following JSON and make a `PUT` call to update the segments.

```
$ cat segment_update
{
    "segments": [
        {
            "id": 501,
            "querystring_mapping_key_value": {
                "qs_key": "music_genre",
                "qs_value": "rock"
            }
        },
        {
            "id": 502,
            "querystring_mapping_key_value": {
                "qs_key": "music_genre",
                "qs_value": "pop"
            }
        },
        {
            "id": 503,
            "querystring_mapping_key_value": {
                "qs_key": "music_genre",
                "qs_value": "hard rock"
            }
        },
        {
            "id": 504,
            "querystring_mapping_key_value": {
                "qs_key": "music_genre",
                "qs_value": "funk"
            }
        }
    ]
}

$ curl -b cookies -c cookies -X PUT -d @segment_update 'https://api.appnexus.com/segment?member_id=201'

{
    "response": {
        "status": "OK",
        "count": 2,
        "id": [
            501,
            502,
            503,
            504
        ],
        "start_element": 0,
        "num_elements": 100,
        "ids": [
            501,
            502,
            503,
            504
        ],
        "segments": {
            "501": {
                "id": 501,
                "code": null,
                "state": "active",
                "short_name": "rock",
                "description": null,
                "member_id": 201,
                "category": null,
                "price": 0,
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": null,
                "advertiser_id": null,
                "last_modified": "2015-06-02 16:39:40",
                "provider": null,
                "parent_segment_id": null,
                "piggyback_pixels": null,
                "querystring_mapping": null,
                "querystring_mapping_key_value": {
                    "qs_key": "music_genre",
                    "qs_value": "rock"
                }
            },
            "502": {
                "id": 502,
                "code": null,
                "state": "active",
                "short_name": "rock",
                "description": null,
                "member_id": 201,
                "category": null,
                "price": 0,
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": null,
                "advertiser_id": null,
                "last_modified": "2015-06-02 16:39:40",
                "provider": null,
                "parent_segment_id": null,
                "piggyback_pixels": null,
                "querystring_mapping": null,
                "querystring_mapping_key_value": {
                    "qs_key": "music_genre",
                    "qs_value": "pop"
                }
            },
            "503": {
                "id": 503,
                "code": null,
                "state": "active",
                "short_name": "rock",
                "description": null,
                "member_id": 201,
                "category": null,
                "price": 0,
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": null,
                "advertiser_id": null,
                "last_modified": "2015-06-02 16:39:40",
                "provider": null,
                "parent_segment_id": null,
                "piggyback_pixels": null,
                "querystring_mapping": null,
                "querystring_mapping_key_value": {
                    "qs_key": "music_genre",
                    "qs_value": "hard rock"
                }
            },
            "504": {
                "id": 504,
                "code": null,
                "state": "active",
                "short_name": null,
                "description": null,
                "member_id": 958,
                "category": null,
                "price": 0,
                "expire_minutes": null,
                "enable_rm_piggyback": true,
                "max_usersync_pixels": null,
                "advertiser_id": null,
                "last_modified": "2015-06-02 16:39:40",
                "provider": null,
                "parent_segment_id": null,
                "piggyback_pixels": null,
                "querystring_mapping": null,
                "querystring_mapping_key_value": {
                    "qs_key": "music_genre",
                    "qs_value": "funk"
                }
            }
        }
    }
}
```
