---
title: Access Policy Group Service
description: In this article, learn about the Access Policy Group service, their JSON fields, and REST API with a thorough example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Policy Group service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-policy-group** service allows you to retrieve the elements that make up a role or a team. For a role this service returns a list of tokens that define user permissions. For teams, this service returns the IDs of the advertisers, insertion orders, publishers, sites, and placements that make up the team.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-policy-group](https://api.appnexus.com/access-policy-group) | View all groups. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `group_id` | int | The ID of the group.<br>**Default:** Auto-generated number. |
| `group_type` | string | The type of group. Value will be either `role` or `team`. |
| `resources` | object | The ID and name of each resource in the group. |

### Resources

Resource values can be retrieved by calling the access-resource service. For more information on retrieving resources, see [View System Resources using the API](view-system-resources-using-the-api.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `token` | string | For roles, a unique string identifier for the resource. |
| `entity_ids` | array of int | For teams, a list of resource IDs. |

## Example

### View all groups

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-group'
{
    "group_id": 10,
    "group_type": "role",
    "resources": [
        {
            "token": "hbapi:/report:get"
        },
        {
            "token": "hbapi:/adjustment:PUT"
        },
        {
            "token": "ui:/buyside/advertiser/select:GET"
        },
        {
            "token": "ui:/buyside/advertiser:GET"
        },
        {
            "token": "hbapi:/segment:DELETE"
        },
        {
            "token": "hbapi:/segment:GET"
        },
        {
            "token": "hbapi:/publisher:GET"
        },
                ...
    ]
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
