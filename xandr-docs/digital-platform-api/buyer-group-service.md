---
title: Buyer Group Service
description: In this article, find information about the Buyer Group Service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Buyer group service

You can create groups of buyers in order to apply similar yield management settings to them as a whole.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `https://api.appnexus.com/buyer-group?id=ID` | View a specific buyer group |
| `GET` | `https://api.appnexus.com/buyer-group` | View all buyer groups |
| `GET` | `https://api.appnexus.com/buyer-group/meta` | Find out which fields you can filter and sort by |
| `POST` | `https://api.appneuxs.com/buyer-group` | Add a buyer group |
| `PUT` | `https://api.appnexus.com/buyer-group?id=ID` <br> (edit-group-member JSON) | Update an existing buyer group |

> [!NOTE]
> This service does not allow the user to add or delete members to or from a group. You must create a JSON file containing all members that should be in the list and execute a `PUT` call. Members that are not in the JSON file are added, while members that are not in the JSON are excluded.

## JSON fields

| Field | Type (Length) | Description |
|---|---|---|
| `buyer_members` | array of objects | This list of members that belong to that buyer group. Refer to the Buyer Members section. <br> **Default**: `null` |
| `code` | string (100) | Allows clients to use AppNexus systems while referring to their own unique object ID values. <br> **Default**: `null` |
| `description` | string (100) | Text that describes the buyer group. <br> **Default**: `null` |
| `id` | int | The identification number of the buyer group. <br> **Default**: Auto-generated number <br> **Required on**: `PUT` or `DELETE` in query string |
| `last_modified` | datetime | The date and time that the buyer group was last updated. <br> **Default**: `null` |
| `name` | string (100) | The name of the buyer group. <br> **Default**: `null` <br> **Required on**: `POST` |

### Buyer members

The `buyer_members` array contains all members that belong to the group.

| Field | Type (Length) | Description |
|---|---|---|
| `id` | int | The identification number of a member in the group. |

## Examples

### Update members in a list

```
$ cat edit-group-member

{
 "buyer-group":{

            "buyer_members":[
                {   "id":2175},
                {   "id":2176},
                {   "id":2177},
                {   "id":2179}
            ]
        }
}

$ curl -b cookies -c cookies -X PUT -d @edit-group-member.json 'https://api.appnexus.com/buyer-group?id=237'

{
    "response":{
        "status":"OK",
        "dbg_info":{
            ...
        }
    }
}
```

### View a specific buyer group

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/buyer-group?id=237'

{
    "response":{
        "status":"OK",
        "buyer-group":{
            "id":237,
            "code":null,
            "name":"Positive Bias Group",
            "description":null,
            "last_modified":"2012-11-22 22:15:37",
            "buyer_members":[
                {
                    "id":2175
                },
                {
                    "id":2176
                },
                {
                    "id":2177
                },
                {
                    "id":2179
                }
            ]
        },
        "dbg_info":{
            ...
        }
    }
}
```

### View all buyer groups

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/buyer-group'

{
    "response":{
        "status":"OK",
        "buyer-groups":[
            {
                "id":41,
                "code":"TPANs",
                "name":"Third Party Ad Networks",
                "description":null,
                "last_modified":"2011-02-07 01:15:19",
                "buyer_members":[
                    {
                        "id":771
                    },
                    {
                        "id":772
                    }
                ]
            },
            {
                "id":50,
                "code":null,
                "name":"Test Buyer Group #1",
                "description":null,
                "last_modified":"2011-02-07 21:07:56",
                "buyer_members":[
                    {
                        "id":273
                    },
                    {
                        "id":405
                    },
                    {
                        "id":650
                    },
                    {
                        "id":681
                    }
                ]
            },
            {
                "id":51,
                "code":null,
                "name":"Buyer Group #2",
                "description":null,
                "last_modified":"2011-02-07 21:11:47",
                "buyer_members":[
                    {
                        "id":273
                    },
                    {
                        "id":324
                    },
                    {
                        "id":405
                    }
                ]
            },
            {
                "id":52,
                "code":null,
                "name":"Buyer Group #3",
                "description":null,
                "last_modified":"2011-02-07 21:11:53",
                "buyer_members":[
                    {
                        "id":324
                    },
                    {
                        "id":654
                    }
                ]
            },
        ],
        "count":79,
        "start_element":null,
        "num_elements":null,
        "dbg_info":{
            ...
        }
    }
}
```

### Create a buyer group

```
$ cat add-buyer-group

{    
    "buyer-group":
    {   "name": "JMSTest"   }
} 


$ curl -b cookies -c cookies -X POST -d @add-buyer-group.json 'https://api.appnexus.com/buyer-group?member_id=126'

{
    "response":{
        "status":"OK",
        "id":253,
        "dbg_info":{
            ...
        }
    }
```

## Related topics

- [Yield Management Profile Service](yield-management-profile-service.md)
- [Yield Management Floor Service](yield-management-floor-service.md)
