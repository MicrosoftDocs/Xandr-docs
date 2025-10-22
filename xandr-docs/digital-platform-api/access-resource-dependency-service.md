---
title: Access Resource Dependency Service
description: In this article, learn about the Access Resource Dependency service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Resource Dependency service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-resource-dependency** service retrieves a list of resource IDs for all parents, children, and dependencies associated with a resource. Use this service to manage dependencies within the system that are under access control.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-resource-dependency](https://api.appnexus.com/access-resource-dependency) | View all resources and their dependencies. |
| `POST` | [https://api.appnexus.com/access-resource-dependency?resource_id=ID](https://api.appnexus.com/access-resource-dependency?resource_id=ID) | Create dependencies to a resource. |
| `DELETE` | [https://api.appnexus.com/access-resource-dependency?resource_id=ID](https://api.appnexus.com/access-resource-dependency?resource_id=ID) | Delete a resource. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `children` | array of ints | An array of resource IDs for the children of the resource. |
| `dependencies` | array of dependency objects | An array of dependency objects containing direct parent/child relationships. |
| `parents` | array of ints | An array of resource IDs for the parents of the resource. |
| `resource_id` | int | The ID of the resource.<br>**Required On:** `POST` and `DELETE`. |

### Dependencies

Resource values can be retrieved by calling the access-resource service. For more information on retrieving resources, see [View System Resources using the API](view-system-resources-using-the-api.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `parent_id` | int | The ID of the parent resource in the parent/child relationship. |
| `child_id` | int | The ID of the child resource in the parent/child relationship. |

## Examples

### View all resource dependencies

```
$ curl -b cookies 'https://api.appnexus.com/access-resource-dependency'
"access-resource-dependency": [
    {
        "resource_id": 22,
        "parents": [
            123,
            134
        ],
        "children": [
            11
        ],
        "dependencies": [
            {
                "parent_id": 15,
                "child_id": 789
            },
            {
                "parent_id": 2,
                "child_id": 15
            }
        ]
    },
        ...
```

### View resource dependencies for a single resource

```
$ curl -b cookies 'https://api.appnexus.com/access-resource-dependency?resource_id=22'
"access-resource-dependency": [
    {
        "resource_id": 22,
        "parents": [
            123,
            134
        ],
        "children": [
            11
        ],
        "dependencies": [
            {
                "parent_id": 15,
                "child_id": 789
            },
            {
                "parent_id": 2,
                "child_id": 15
            }
        ]
    }
]
 
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
